|![](https://upload.wikimedia.org/wikipedia/commons/thumb/1/17/Warning.svg/156px-Warning.svg.png) | This project is now deprecated.
|---|---|

# PingFederate

Remember to add the repo before installing the chart
```shell
helm repo add pingidentity-pc https://patrickcping.github.io/ping-identity-helm-charts-repo/
```

## ⚠️ Deprecation Notice

This repository is now deprecated and replaced by the offical [Ping Identity Helm charts](https://helm.pingidentity.com/)

## Use Devops Key
In a development or sandbox environment, the helm chart can be run with a valid registered devops license key (https://pingidentity-devops.gitbook.io/devops/getstarted/devopsregistration).  Make sure the `PING_IDENTITY_DEVOPS_USER` and `PING_IDENTITY_DEVOPS_KEY` environment variables are set

```shell
helm install \
pingfederate --debug \
--set license.useDevOpsKey=true \
--set license.devOpsKey.user=${PING_IDENTITY_DEVOPS_USER} \
--set license.devOpsKey.key=${PING_IDENTITY_DEVOPS_KEY} \
--set license.acceptEULA=yes \
pingidentity-pc/pingfederate
```

## Use provided License file
In a controlled environment, the helm chart can be run with a valid license file.  Add the license file as a secret as shown:
```shell

kubectl create secret generic pingfederate-license --from-file ./pingfederate.lic

helm install \
pingfederate --debug \
--set license.licenseSecretName=pingfederate-license \
--set license.acceptEULA=yes \
pingidentity-pc/pingfederate
```

## Chart Configuration

| Parameter | Description | Default |
|--|--|--|
| TODO | TODO | TODO |


## PingFederate Configuration Profile

By default this chart loads sample PingFederate configuration on startup.  These are layered as:

| Configuration Layer | Server Profile |
|--|--|
| 1 | https://github.com/pingidentity/pingidentity-server-profiles/tree/master/getting-started/pingfederate |
| 2 | https://github.com/pingidentity/pingidentity-server-profiles/tree/master/pf-dns-ping-clustering |

You can add additional layers or change to your own configuration repository by modifying the `SERVER_PROFILE_*` environment variables in `pingfederate.envs` of the chart configuration

## Injecting Ping Environment Variables

You can inject your own environment variables to modify the behaviour of the Ping Docker image, or when using environment variables in your own server profiles.  For this, you can create your own values.yaml file and insert any environment variables you wish under `pingfederate.envs` of the chart configuration.  For example:

```
pingfederate:
  envs:
    SERVER_PROFILE_URL: https://github.com/myuser/mycustomrepo.git 
    SERVER_PROFILE_PATH: my/path/to/pingfederate
    SERVER_PROFILE_BRANCH: master
    MY_SERVER_PROFILE_VAR: "your value here"
```

For available image environment variables, see [Ping Identity documentation](https://pingidentity-devops.gitbook.io/devops/dockerimagesref/pingfederate#environment-variables)

## Clustering Example

```shell
helm install \
pingfederate-cluster --debug \
--set pingfederate.logging=DEBUG \
--set pingfederate.clustering.enabled=true \
--set license.useDevOpsKey=true \
--set license.devOpsKey.user=${PING_IDENTITY_DEVOPS_USER} \
--set license.devOpsKey.key=${PING_IDENTITY_DEVOPS_KEY} \
--set license.acceptEULA=yes \
pingidentity-pc/pingfederate
```

## Clustering Example, with autoscaling

```shell
helm install \
pingfederate-cluster --debug \
--set pingfederate.logging=DEBUG \
--set pingfederate.clustering.enabled=true \
--set pingfederate.clustering.autoscaling.enabled=true \
--set pingfederate.clustering.autoscaling.minReplicas=3 \
--set pingfederate.clustering.autoscaling.maxReplicas=5 \
--set license.useDevOpsKey=true \
--set license.devOpsKey.user=${PING_IDENTITY_DEVOPS_USER} \
--set license.devOpsKey.key=${PING_IDENTITY_DEVOPS_KEY} \
--set license.acceptEULA=yes \
pingidentity-pc/pingfederate
```

## Waiting for dependent services

For an example of waiting for a dependent service, such as PingDirectory, see the example [here](https://github.com/patrickcping/ping-helm-kustomize-example)