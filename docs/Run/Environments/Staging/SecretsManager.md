# **AWS Secrets Manager**

### **Below are the securely available secret keys in staging environment and the respective keys used in k8s secret manifest**

|Secret Config Key                 |Description       |   
|----------------------------------|------------------|
|POSTGRES_USER                     |postgres username |
|POSTGRES_PASSWORD                 |postgres password |
|MONGO_URL                         |mongo url         |
|MONGO_USER                        |mongo username    |
|MONGO_PASSWORD                    |mongo password    |
|RABBIT_USER                       |rabbitmq username |
|RABBIT_PASSWORD                   |rabbitmq password |
|MFU_USER_ID                       |mfu userid        |
|MFU_PASSWORD                      |mfu password      |
|MFU_SECRET_KEY                    |mfu secretkey     |
|MFU_ENTITY_ID                     |mfu entityid      |
|CAMS_PUBLIC_KEY/CAMS_PRIVATE_KEY  |CAMS keys         |
                                                      

### **Sample kubernetes secrets creation using manifest**

apiVersion: v1  
kind: Secret  
metadata:  
    name: sample-secret  
    namespace: sample  
type: Opaque  
data:  
   #Base64-encoded values  
    POSTGRES_USER: ********  
    POSTGRES_PASSWORD: *******  
  
