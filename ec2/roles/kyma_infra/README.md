Role Name
=========

Installs java11 and java8 on a Fedora server that can be used with Quarkus and EAP app deployment respectively.

Requirements
------------

Provision the fedora server using ./create_infra.sh. Please refer to the [readme](../README.md)

Dependencies
------------
* This role is dependent on the following roles
  - jboss-eap 
  - Wildfly utils 
  - Wildfly driver
  - keycloak

How to deploy the apps
-------------
* For setting up the ec2 instance, refer to [ec2 role](https://github.com/migtools/playpen/tree/main/ec2#readme)

* Once its setup, make sure the app you want to install has the [correct configuration](./ec2/roles/kyma_infra/defaults/main.yml)

* Run the role using the script `./setup_kyma_infra.sh`

Once the run is successful you can access the apps in the following URLs,

* Kitchensink - https://github.com/tqvarnst/jboss-eap-quickstarts/tree/quarkus-3.2, https://github.com/windup/jboss-eap-quickstarts/tree/7.4.x/kitchensink/src/main/java/org/jboss/as/quickstarts/kitchensink
  * eap - http://<ec2 url>:8080/kitchensink
  * quarkus - http://<ec2 url>:8085/kitchensink

* helloworld-mdb - https://github.com/savitharaghunathan/helloworld-mdb
  * eap - http://<ec2 url>:8080/helloworld-mdb/HelloWorldMDBServletClient (to send messages to the queue)
  * eap -  http://<ec2 url>:8080/helloworld-mdb/HelloWorldMDBServletClient?topic ( to send messages to the topic)
  * quarkus - http://<ec2 url>:8085/HelloWorldMDBServletClient
  * quarkus - http://<ec2 url>:8085/HelloWorldMDBServletClient?topic

* coolstoredb - https://github.com/mathianasj/eap-coolstore-monolith/tree/quarkus-migration, https://github.com/deewhyweb/eap-coolstore-monolith
  * eap - http://<ec2 url>:8080
  * quarkus - http://<ec2 url>:8085


Additional Information
-------------

Background
-------------

* Infra setup:
  * Server: fedora 38
  * docker-ce
  * EAP 7.4 using java 8
  * EAP running on port 8080
  * Quarkus using java 11/17 depending on the app
  * Quarkus running on port 8085
  * Java versions and quarkus installations are managed by sdkman
  * manual maven install
  * uses roles from migtools/playpen repo to create ec2 instance and configure eap
  * note: eap should use standalone full config for messaging to work
  * created a new role called kyma_infra - https://github.com/migtools/playpen/pull/5
  * run the role using the script ./setup_kyma_infra.sh

Todo:
------
* refactor java installation
  * Take input of java versions and install that using sdkman
* Run apps in prod mode
* Note: wildfly role overrides java8 installed by sdkman. Refactor wildfly role to not install java, it is installed already
* Use mainitained ansible role for maven install and management if possible