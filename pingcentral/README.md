|![](https://upload.wikimedia.org/wikipedia/commons/thumb/1/17/Warning.svg/156px-Warning.svg.png) | This project is now deprecated.
|---|---|

# PingCentral

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
pingcentral --debug \
--set license.useDevOpsKey=true \
--set license.devOpsKey.user=${PING_IDENTITY_DEVOPS_USER} \
--set license.devOpsKey.key=${PING_IDENTITY_DEVOPS_KEY} \
--set license.acceptEULA=yes \
pingidentity-pc/pingcentral
```

## Use provided License file
In a controlled environment, the helm chart can be run with a valid license file.  Add the license file as a secret as shown:
```shell

kubectl create secret generic pingcentral-license --from-file ./pingcentral.lic

helm install \
pingcentral --debug \
--set license.licenseSecretName=pingcentral-license \
--set license.acceptEULA=yes \
pingidentity-pc/pingcentral
```

## Chart Configuration

| Parameter | Description | Default |
|--|--|--|
| TODO | TODO | TODO |

## PingCentral Configuration Profile

By default this chart loads sample PingCentral configuration on startup.  These are layered as:

| Configuration Layer | Server Profile |
|--|--|
| 1 | https://github.com/pingidentity/pingidentity-server-profiles/tree/master/baseline/pingcentral/external-mysql-db |
| 2 | https://github.com/pingidentity/pingidentity-server-profiles/tree/master/baseline/pingcentral/logging |

You can add additional layers or change to your own configuration repository by modifying the `SERVER_PROFILE_*` environment variables in `pingcentral.envs` of the chart configuration

## Injecting Ping Environment Variables

You can inject your own environment variables to modify the behaviour of the Ping Docker image, or when using environment variables in your own server profiles.  For this, you can create your own values.yaml file and insert any environment variables you wish under `pingcentral.envs` of the chart configuration.  For example:

```
pingcentral:
  envs:
    SERVER_PROFILE_URL: https://github.com/myuser/mycustomrepo.git 
    SERVER_PROFILE_PATH: my/path/to/pingcentral
    SERVER_PROFILE_BRANCH: master
    MY_SERVER_PROFILE_VAR: "your value here"
```

For available image environment variables, see [Ping Identity documentation](https://pingidentity-devops.gitbook.io/devops/dockerimagesref/pingcentral#environment-variables)

## Chart Dependencies

This chart uses the [Bitnami MySQL](https://hub.helm.sh/charts/bitnami/mysql) chart to store application data