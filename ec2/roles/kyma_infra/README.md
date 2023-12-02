Role Name
=========

Installs java11 and java8 on a Fedora server that can be used with Quarkus and EAP app deployment respectively.

Requirements
------------

Provision the fedora server using ./create_infra.sh. Please refer to the [readme](../README.md)

How to Run
----------

* cd ../
* Run `./setup_kyma_infra.sh`

Background
-------------

* Infra setup:
  * Server: fedora 38
  * docker-ce
  * EAP 7.4 using java 8
  * EAP running on port 8080
  * Quarkus using java 11
  * Quarkus running on port 8085
  * Java versions and quarkus installations are managed by sdkman
  * manual maven install
  * uses roles from migtools/playpen repo to create ec2 instance and configure eap
  * note: eap should use standalonefull config
  * created a new role called kyma_infra - https://github.com/migtools/playpen/pull/5
  * run the role using the script ./setup_kyma_infra.sh
  * Manual run down : https://hackmd.io/H04eYLdSS82wt8Ryh8UOSQ

Todo:
------
* refactor java installation
  * Take input of java versions and install that using sdkman
* Run quarkus in prod mode
* Note: wildfly role overrides java8 installed by sdkman. Refactor wildfly role to not install java, it is installed already
* 