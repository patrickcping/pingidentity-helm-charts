# PingDirectory

Remember to add the repo before installing the chart
```shell
helm repo add pingidentity-pc https://patrickcping.github.io/ping-identity-helm-charts-repo/
```

## Use Devops Key
In a development or sandbox environment, the helm chart can be run with a valid registered devops license key (https://pingidentity-devops.gitbook.io/devops/getstarted/devopsregistration).  Make sure the `PING_IDENTITY_DEVOPS_USER` and `PING_IDENTITY_DEVOPS_KEY` environment variables are set

```shell
helm install \
pingdirectory --debug \
--set license.useDevOpsKey=true \
--set license.devOpsKey.user=${PING_IDENTITY_DEVOPS_USER} \
--set license.devOpsKey.key=${PING_IDENTITY_DEVOPS_KEY} \
--set license.acceptEULA=yes \
--set persistentvolume.enabled=false \
pingidentity-pc/pingdirectory
```

## Use provided License file
In a controlled environment, the helm chart can be run with a valid license file.  Add the license file as a secret as shown:
```shell

kubectl create secret generic pingdirectory-license --from-file ./pingdirectory.lic

helm install \
pingdirectory --debug \
--set license.licenseSecretName=pingdirectory-license \
--set license.acceptEULA=yes \
pingidentity-pc/pingdirectory
```

## Chart Configuration

| Parameter | Description | Default |
|--|--|--|
| TODO | TODO | TODO |

## PingDirectory Configuration Profile

By default this chart loads sample PingDirectory configuration on startup.  These are layered as:

| Configuration Layer | Server Profile |
|--|--|
| 1 | https://github.com/pingidentity/pingidentity-server-profiles/tree/master/getting-started/pingdirectory |

You can add additional layers or change to your own configuration repository by modifying the `SERVER_PROFILE_*` environment variables in `pingdirectory.envs` of the chart configuration
