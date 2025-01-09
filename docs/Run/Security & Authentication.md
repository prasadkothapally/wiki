# Security & Authentication

### Version Control System

We are hosting the source code repositories in Techwave hosted GitLab under the Fintrust Group.

[GitLab URL](https://gitlabnew.techwave.net)

We are providing the access to the team with an expiration period of 3 months


### Development Infrastructure Access

Access ( Login Credentials ) to the 3 servers ( Build , Data and Compute) is with DevOps team and won't be shared with anyone unless there is a necessity.

### Staging Infrastructure Access

Staging environment is being hosted in AWS Cloud.

Console access to the AWS account is restricted to DevOps team and team is responsible for providing the cloud access for rest of them if necessary.

Developers are having individual ssh keys to connect to the databases (Postgres, Mongo) of staging environment.


### K8s secrets in DEV & Staging

We created a k8s secret to pull the docker image from GitLab container registry and access token used in this secret will expire for every 3 months.

We need to recreate this secret for every 3 months, so that k8s can happily pull the images from GitLab container registry.

Otherwise status of the all application pods will be "imagepullbackoff" state.

Below are the instructions to recreate the k8s secret.

```
kubectl create secret docker-registry regcred --docker-server=gitlabnew.techwave.net:5050 --docker-username=mshivaram --docker-password=your-gitlab-group-access-token --docker-email=shivaram.mantripragada@techwave.net
```

In the above command, gitlab-group-access-token can be retrieved from GitLab UI -> Settings -> Access Tokens -> Add new access token

To expose the secret as k8s manifest:

```
kubectl get secret regcred --output=yaml
```
store the cleaned output as a k8s manifest, see helm/templates/secrets.yaml for an gitlab docker registry secret stored as a k8s manifest.

Update both allfunds and accounting helm charts, commit the changes and rollout the deployment via pipeline in both the environments.

