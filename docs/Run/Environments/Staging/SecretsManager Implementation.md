# **AWS Secrets Manager Implementation**

## **Manage Kubernetes Secrets using AWS Secrets Manager**

Kubernetes has a built-in feature for secrets management called a Secret. The Secret object is convenient to use, but does not support storing or retrieving secret data from external secret management systems such as AWS Secrets Manager. 
It's often beneficial to use Kubernetes with an external secrets service that handles secret management. 
Due to this limitation, GoDaddy came up with an open source solution called External Secrets Operator. 

## **External Secrets Operator (ESO)**

ESO provides the same ease of use as native Secret object and provides access to secrets stored externally. 
It does this by extending Kubernetes with Custom Resources, which defines where secrets live and how to synchronize them.

In simple terms, ESO makes API calls to retrieve secret data from the external secrets service like AWS Secrets Manager and injects the secret data as Kubernetes Secrets object.

![Kubernetes Cluster  External Secrets Service](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*Xm-EDmrqawSQaGzhCNGRUA.png)


### **Key Concepts**

**External Secrets Controller** — A Kubernetes controller that fetches secrets from an external API and creates Kubernetes secrets. If the secret from the external API changes, the controller reconciles the state in the cluster and updates the secrets.

**ExternalSecret** -  A custom resource definition that specifies what secret data to fetch. It references SecretStore which knows how to access that data. The controller uses the ExternalSecret as a blueprint to create secrets.

**SecretStore** - A custom resource definition that specifies the access needed to fetch the secret from the external API. SecretStore takes care of authentication and access.

And there are two kinds of SecretStore resources:

**ClusterSecretStore** - A global, cluster-wide SecretStore that can be referenced from all namespaces. You can use it to provide a central gateway to your secret provider.

**SecretStore** - A namespaced SecretStore that can only be referenced from a single namespace.

### **Integrating AWS Secrets Manager with Kubernetes**

#### **Install External Secrets Operator using Helm**

    helm repo add external-secrets https://charts.external-secrets.io
    helm repo update

#### **Install ESO in external-secrets namespace**

    helm upgrade --namespace external-secrets --create-namespace --install --wait external-secrets external-secrets/external-secrets

#### **Verify ESO installation**

    kubectl -n external-secrets get all

#### **Create an IAM user and attach the managed policy**

Now, that we have ESO successfully deployed in the cluster. Let’s create a dedicated AWS IAM user, which will be used to authenticate to AWS and access the secret data from the AWS Secrets Manager.

    aws iam create-user --user-name external-secrets

And assign the SecretsManagerReadWrite managed policy to grant the IAM user access to the secrets manager.

For good security hygiene, use the principle of least privilege on production, limiting the permissions for the external-secrets IAM user to only access the needed secrets path and KMS key.

    aws iam attach-user-policy --user-name external-secrets --policy-arn arn:aws:iam::aws:policy/SecretsManagerReadWrite

Now, generate the AWS access and secret key.

    aws iam create-access-key --user-name external-secrets

Place the access key and secret key onto a file and create a secret in default namespace called awssm-secret from the file.

    echo -n "REPLACE_ME_WITH_YOUR_ACCESS_KEY" > access-key
    echo -n "REPLACE_ME_WITH_YOUR_SECRET_KEY" > secret-access-key
    kubectl -n default create secret generic awssm-secret --from-file=./access-key --from-file=./secret-access-key

#### **Create app secret in AWS Secret Manager**

Go ahead and create a demo app secret in ap-south-1 region of the AWS Secrets Manager via AWS CLI or Cosnole, which will be fetched later by External Secrets and exposed to the application Pod via environment variable

And verify the secret from the AWS Secrets Manager console.


#### **Create a cluster-scoped secret store**

As mentioned before, a cluster-scoped secret store allows referencing the secret store from any namespaces, which is convenient to use as a central gateway to the secret provider, rather than creating a secret store per namespace.

Refer the manifest file in bastion server at the path /home/ec2-user/externalsecretsperator/cluster-secret-store.yaml

And apply the manifest

    kubectl apply -f cluster-secret-store.yaml

And, verify the cluster secret store is created successfully and shows the message “store validated”.

    kubectl describe clustersecretstore global-secret-store

#### **Create ExternalSecret to fetch the secret data**

We’re now ready to create the ExternalSecret resource and fetch the app-secret demo secret data from AWS Secrets Manager by referencing the cluster-scoped secret store.

And save the following YAML as allfunds-secret.yaml where ExternalSecret object specification is structured as such:

    * spec.refreshInterval - is set to 1 minute, meaning reconciliation will take place every minute.
    * spec.secretStoreRefis - set to ClusterSecretStore named global-secret-store which we created before.
    * spec.target.name - specifies the name of the secret object that will be created in the same namespace, where ExternalSecret is created.
    * spec.dataFrom - specifies the secret name in the AWS Secrets Manager as key and extracttells it to retrieve all key/value secrets.

Refer the manifest file in bastion server at the path /home/ec2-user/externalsecretsperator/allfunds-secret.yaml

Finally, go ahead and apply the manifest:

    kubectl -n allfunds apply -f allfunds-secret.yaml

If everything went as planned, we should get SecretSynced status for ExternalSecret resource and a new Kubernetes Secret resource called app-secret should be created.

    kubectl -n allfunds get externalsecret
    kubectl -n allfunds get secret allfunds-secret


#### **What just happened?**

    * ExternalSecret was able to authenticate to AWS Secrets Manager using the cluster-scoped secret store.
    * ExternalSecret was able to fetch the secret data and create the Kubernetes Secret object.


#### **Consume the Secret from Pod**

Now, that the ExternalSecret was able to retrieve the secrets from AWS Secrets Manager and on-the-fly create the Kubernetes Secret for us. 
We can reference this secret allfunds-secret as usual from the Pod, without any application modification.
Let’s go ahead and apply the following Pod manifest and see if our container has the secret data in its environment variable.

Refer the manifest file in bastion server at the path /home/ec2-user/externalsecretsperator/deployment.yaml

And apply the manifest:

    kubectl -n allfunds apply -f deployment.yaml
	
Once, applied. The Pod will create a single container and runs env command and exits. 
We can check the Pod log to verify that our secret data was indeed available as an environment variable.


### **Conclusion**

External Secrets Operator is a mature and popular open source project with great community engagement. 
It is well-tested and stable for production workloads with high-availability features for managing and synchronizing large-scale secrets and supports many popular external secrets providers like HashiCorp Vault, Google Secrets Manager, Azure Key Vault, and many more.
Since External Secrets provides the same ease of use as Kubernetes native Secret objects, it doesn’t require any application modifications, and existing application leveraging Secret object works out of the box without any changes.

For more information, please visit [Kubernetes Secrets using AWS Secrets Manager](https://www.giantswarm.io/blog/manage-kubernetes-secrets-using-aws-secrets-manager)