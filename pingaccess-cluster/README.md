# PingAccess Cluster

Remember to add the repo before installing the chart
```shell
helm repo add pingidentity-pc https://patrickcping.github.io/ping-identity-helm-charts-repo/
```

## Use Devops Key
In a development or sandbox environment, the helm chart can be run with a valid registered devops license key (https://pingidentity-devops.gitbook.io/devops/getstarted/devopsregistration).  Make sure the `PING_IDENTITY_DEVOPS_USER` and `PING_IDENTITY_DEVOPS_KEY` environment variables are set

```shell
helm install \
pingaccess-cluster --debug \
--set admin.license.useDevOpsKey=true \
--set admin.license.devOpsKey.user=${PING_IDENTITY_DEVOPS_USER} \
--set admin.license.devOpsKey.key=${PING_IDENTITY_DEVOPS_KEY} \
--set admin.license.acceptEULA=yes \
--set engine.license.useDevOpsKey=true \
--set engine.license.devOpsKey.user=${PING_IDENTITY_DEVOPS_USER} \
--set engine.license.devOpsKey.key=${PING_IDENTITY_DEVOPS_KEY} \
--set engine.license.acceptEULA=yes \
pingidentity-pc/pingaccess-cluster
```

## Use provided License file
In a controlled environment, the helm chart can be run with a valid license file.  Add the license file as a secret as shown:
```shell

kubectl create secret generic pingaccess-license-admin --from-file ./pingaccess.lic
kubectl create secret generic pingaccess-license-engine --from-file ./pingaccess.lic

helm install \
pingaccess-cluster --debug \
--set admin.license.licenseSecretName=pingaccess-license-admin \
--set admin.license.acceptEULA=yes \
--set engine.license.licenseSecretName=pingaccess-license-engine \
--set engine.license.acceptEULA=yes \
pingidentity-pc/pingaccess-cluster
```

## Chart Configuration

| Parameter | Description | Default |
|--|--|--|
| TODO | TODO | TODO |


## PingAccess Cluster Configuration Profile

By default this chart loads sample PingAccess configuration on startup.  These are layered as:

| Configuration Layer | Server Profile |
|--|--|
| 1 | https://github.com/pingidentity/pingidentity-server-profiles/tree/master/pa-clustering/pingaccess |

You can add additional layers or change to your own configuration repository by modifying the `SERVER_PROFILE_*` environment variables in `admin.pingaccess.envs` and `engine.pingaccess.envs` of the chart configuration

## Chart Dependencies

This chart uses the [PingAccess](./../pingaccess) chart for both the Administration and Engine runtimes.  Refer to the [README.md](./../pingaccess/README.md) of that chart for ingress, toleration, resource options etc.