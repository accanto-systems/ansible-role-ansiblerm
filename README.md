# Ansible Role - Ansible RM

Role for installing the [OSSLM Ansible RM](https://github.com/IBM/osslm-ansible-resource-manager) using Helm

## Configure Ansible RM Helm Chart

Installation of Ansible RM requires a path to a valid helm chart, configure the location with either a http/https address or file path (on local machine):

```
arm_chart: https://github.com/IBM/osslm-ansible-resource-manager/releases/download/v1.3.4/osslm-ansible-resource-manager-1.3.4.tgz
```

## Configure Ansible RM Docker Image

Set the Docker image to be used with the following variables:

```
arm_docker_image: accanto/osslm-ansible-rm
arm_docker_version: 1.3.1
```

Alternatively, specify a path to TAR containing the image (result of `docker save`):

```
arm_docker_strategy: from_package
arm_docker_tar: /home/user/ansible-rm-docker.tgz
```

## Refresh Chart and Image

The chart and Docker image TAR are only copied to the target machine if they do not already exist. To force an update of the existing packages, use:

```
arm_force_refresh_packages: True
```

## Uninstall Existing

Installation will only take place in 2 situations:

- there is no existing Ansible RM installed (identified by searching for a helm release named `ansiblerm`)
- the existing ansiblerm does not match the version to be installed by given packages

In the second case, a re-install can be forced using:

```
arm_force_reinstall: True
```

## Onboard in Stratoss&trade; Lifecycle Manager

This role may be configured to onboard the RM to a target Stratoss&trade; Lifecycle Manager. Update the following variables to include valid credentials for your Stratoss LM environment:

```
arm_onboard: True
arm_onboard_addr: http://address_to_lm_api_gateway
arm_onboard_auth: True
arm_onboard_client: MyClient
arm_onboard_client_secret: secret
arm_onboard_name: defaultrm
arm_onboard_type: ansiblerm
## Use the internal address of the ansible-rm (when Stratoss LM is installed in the same Kubernetes cluster). Otherwise use 'external'
arm_onboard_url_type: internal
```
