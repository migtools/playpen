### To create jboss wildfly instance

* Make sure to set the role to `jboss-wildfly` in `my_vars.yml`

Run `./setup_nodes.sh`

### To create jboss EAP instance

* We will be using offline installation for this role.Please [download](https://access.redhat.com/jbossnetwork/restricted/listSoftware.html?downloadType=distributions&product=appplatform&version=7.4) `jboss-eap-7.4.0.zip` from the RH Customer Portal and place it in `../ec2/jboss-eap-7.4.0.zip`. Make sure the file type is `zip`.

* Make sure to set the role to `jboss-eap` in `my_vars.yml`

Run `./setup_nodes.sh`

4. ssh into an instance and use: `ssh -i keys/mykeyname.pem fedora@ec2-example-compute-1.amazonaws.com`
   * note the usage of `fedora` as user name

## Install `Helloworld` application

### In standalone EAP server 
1. Make sure that the variable `app_role: jboss-app-deploy` is set in `my_vars.yml` file 

2. Run `./setup_app.sh`

3. Once deployed, access the app here - `http://<your ec2 instance name>:8080/helloworld/HelloWorld`

_Note: It takes a few seconds for the app to be apployed, hence the added wait time in the play_ 

### Openshift cluster

#### Pre req: 
* OpenShift cluster 4.11 or above
* Export 'Kubeconfig` variable or make sure ~/.kube/config is valid

#### Deploy app
1. Run `./deploy_eap.sh`

