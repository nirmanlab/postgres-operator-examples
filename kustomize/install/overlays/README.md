# How to upgrade the pgo 

##### Reference
https://access.crunchydata.com/documentation/postgres-operator/latest/upgrade/kustomize/


* before doing anything, trigger full database sync to s3, because we will have to restore it back once we upgrade the pgo
* remove the existing installation by deleting deployment, service account and crds 
* once we remove the stuff, it'll also delete running databases,
* once database is removed, we need to restore it back from s3 by creating postgres-restore.yaml file and then updating kustomization.yaml file with it. 
* once restore operation is over, it'll start the database automatically. 
* next step is to update below service's environment file to update it with newly created secret variables.
  * authserver
  * laravel
  * coreservice
  * availability
  * temporal
* after then restart each service and it'll be good to go