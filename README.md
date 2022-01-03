# deploy GLPI with Kubernetes

# Requirements
## Kubectl client and config file
```kubectl version```
  ``` kubectl config view```
## Cluster Kubernetes my case use Rancher  Provider: RKE1 Kubernetes Version: v1.21.7
    ```kubectl get nodes```
## Mysql Data Base my case use Mysql 8.0.26 Operator 
## Private Key an Certificate (Optional and recomend)
# Deploy
## Clone Repo 
 ```git clone https://github.com/emersonarredondo/glpi-kubernetes.git```
## Create secrets please customize this  Environnment variables
 ```kubectl create secret generic glpi-secret  --namespace default --from-literal=GLPI_DB_HOSTNAME=172.16.10.241 --from-literal=GLPI_DB_USER=root --from-literal=GLPI_DB_PASSWORD=Changemeplease! --from-literal=GLPI_DBNAME=glpidb
```
Check secret 
``` kubectl get secret glpi-secret```
``` kubectl describe  secret glpi-secret```
## Create Persistent volumen 
   ```kubetctl  apply -f pve.yaml```
 Check PVC
  ```kubectl get pvc glpi ```
 ```kubectl describe pvc glpi```
 ## Create Deployment customize options Language, version,Timezone
 ```kubetctl  apply -f deployment.yaml```
 ```kubectl get deployment  glpi```
   ``` kubectl describe deployment glpi``` 
 ## Create service
   ```kubetctl  apply -f service.yaml ``` 
    ```kubectl  get svc glpi```
    ```kubectl  get svc glpi```
 ## Create ingress witch custom cert and private tls
 ``` kubectl create secret tls tls.domain.pe \
    --cert domain.crt --key domain.key``` 
 ## Apply ingress
 ``` kubectl  apply -f ingress.yaml``` 
 ``` kubectl get ingress  glpi-ingress``` 
 ``` kubectl describe ingress glpi-ingress``` 
## Test url ingress or ip loadbalancer  remember change passwords 

# Environnment variables
This Environnment variables can you use deployment.yaml or DockerCompose 
## TIMEZONE

If you need to set timezone for Apache and PHP

## LANG
select your language  code example es_419 latin America [Check you code here ](https://github.com/glpi-project/glpi/blob/0888fee5f55a924653ee9385fbc7431a81d36be1/inc/define.php)

## VERSION_GLPI  
example 9.5.6 Version 10.0.0-beta may not work in this case, use the installation wizard from the web browser
## GLPI_DB_HOSTNAME
 Set your ip o hostname mysql server
## GLPI_DB_USER  
    Set  username with glpi recomend use dedicate username 
## GLPI_DB_PASSWORD
    Set your Password 
## GLPI_DBNAME
    Set your database Name 
#
