# Create an ec2 env for installing JBoss Wildfly 

This directory contains ansible automation to create a single ec2 host and install JBoss Wildfly/EAP for explorations
* Create a Fedora or CentOS instance
* Install JBoss Wildfly/EAP

## Expectations 
* This automation assumes you have ec2 access and your [AWS environment variables are set](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-envvars.html)
* We will create all ec2 resources with a name pattern based on `project_tag` in [my_vars.yml](my_vars.yml) 
* SSH access to instances will be possible using the ssh key in the `./keys` local directory and username `fedora` or `ec2-user` depending on what AMI is launched.
   * Note:  The SSH key will be downloaded *only* if it did not previously exist in the specific AWS region, i.e. the SSH private key is only downloaded when it is created, subsequent runs will use the ssh public key information in AWS.  If you don't save the SSH private key you will *not* be able to access your instances.

# Pre-provisioning Steps
## On MacOS
 * Install rustup to satisfy reqs for python cryptography package building
 * Install 'openssl':  `brew install openssl`


## All Platforms
 * You can run `init.sh` which will execute the below commands
   * Install Virtualenv
      ```
      python3 -m venv env
      ```

   * Activate Virtualenv and install requirements
      ```
      source env/bin/activate
      pip3 install -r requirements.txt
      ```
   
   * Install Ansible collections
     ```
     ansible-galaxy install -r requirements.yml	
     ```

## To Update the requirements
   ```
   pip3 freeze > requirements.txt
   ``` 

# Usage
## Customizations
 * If you want to run this for yourself without stepping on anyone else, then change the below:
   * Copy [sample.my_vars.yml](sample.my_vars.yml) to `my_vars.yml`
   * Edit `my_vars.yml` and change the value of `project_tag` to something unique
   * Update [my_hosts.aws_ec2.yml](my_hosts.aws_ec2.yml) and change this line "`- jwm_playpen*`" to match your new `project_tag` 

## To create the environments
1. `cp sample.my_vars.yml my_vars.yml`
2. `./create_infra.sh`
3. 
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


## To delete the environments
1. `./delete_infra.sh`

