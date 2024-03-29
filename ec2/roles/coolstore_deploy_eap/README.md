Role Name
=========

Deploys coolstore EAP app 

Requirements
------------

* Provision the server: Pre-req can be found in [readme](../README.md)
Run `cd.. && ./create_infra.sh`

* We will be using offline installation of Red Hat EAP for this role. Please [download](https://access.redhat.com/jbossnetwork/restricted/listSoftware.html?downloadType=distributions&product=appplatform&version=7.4) `jboss-eap-7.4.0.zip` from the RH Customer Portal and place it in `../ec2/jboss-eap-7.4.0.zip`. Make sure the file type is `zip`.

* We will be using offline installation for keycloak. Download [keycloak-20.0.5.zip](https://github.com/keycloak/keycloak/releases/download/20.0.5/keycloak-20.0.5.zip) and place it under ../ec2
File relative path eg: ec2/keycloak-20.0.5.zip 

Role Variables
--------------
App variables are mentioned here - ec2/kai_deploy_eap/defaults/main.yml

Dependencies
------------

* This role is dependent on the following roles
  - jboss-eap 
  - Wildfly utils 
  - Wildfly driver
  - keycloak

Deploy EAP coolstore app
----------------
* Run `cd.. && ./setup_coolstore_app.sh`

How to access the app
----------------
Once the ansible role succeeds, navigate to - `http://<your_ec2_ip>:8080`

Note: It can take a few min to start and load the app. You might see the default JBoss EAP page until the app is deployed.