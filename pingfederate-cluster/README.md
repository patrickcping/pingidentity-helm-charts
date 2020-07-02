# PingFederate Cluster

Remember to add the repo before installing the chart
```shell
helm repo add pingidentity-pc https://patrickcping.github.io/ping-identity-helm-charts-repo/
```

## Use Devops Key
In a development or sandbox environment, the helm chart can be run with a valid registered devops license key (https://pingidentity-devops.gitbook.io/devops/getstarted/devopsregistration).  Make sure the `PING_IDENTITY_DEVOPS_USER` and `PING_IDENTITY_DEVOPS_KEY` environment variables are set

```shell
helm install \
pingfederate-cluster --debug \
--set admin.license.useDevOpsKey=true \
--set admin.license.devOpsKey.user=${PING_IDENTITY_DEVOPS_USER} \
--set admin.license.devOpsKey.key=${PING_IDENTITY_DEVOPS_KEY} \
--set admin.license.acceptEULA=yes \
--set engine.license.useDevOpsKey=true \
--set engine.license.devOpsKey.user=${PING_IDENTITY_DEVOPS_USER} \
--set engine.license.devOpsKey.key=${PING_IDENTITY_DEVOPS_KEY} \
--set engine.license.acceptEULA=yes \
pingidentity-pc/pingfederate-cluster
```

## Use provided License file
In a controlled environment, the helm chart can be run with a valid license file.  Add the license file as a secret as shown:
```shell

kubectl create secret generic pingfederate-license-admin --from-file ./pingfederate.lic
kubectl create secret generic pingfederate-license-engine --from-file ./pingfederate.lic

helm install \
pingfederate-cluster --debug \
--set admin.license.licenseSecretName=pingfederate-license-admin
--set admin.license.acceptEULA=yes \
--set engine.license.licenseSecretName=pingfederate-license-engine
--set engine.license.acceptEULA=yes \
pingidentity-pc/pingfederate-cluster
```

## Chart Configuration

| Parameter | Description | Default |
|--|--|--|
| TODO | TODO | TODO |


## PingFederate Cluster Configuration Profile

By default this chart loads sample PingFederate configuration on startup.  These are layered as:

| Configuration Layer | Server Profile |
|--|--|
| 1 | https://github.com/pingidentity/pingidentity-server-profiles/tree/master/getting-started/pingfederate |
| 2 | https://github.com/pingidentity/pingidentity-server-profiles/tree/master/pf-dns-ping-clustering |

You can add additional layers or change to your own configuration repository by modifying the `SERVER_PROFILE_*` environment variables in `admin.pingfederate.envs` and `engine.pingfederate.envs` of the chart configuration

## Chart Dependencies

This chart uses the [PingFederate](./../pingfederate) chart for both the Administration and Engine runtimes.  Refer to the [README.md](./../pingfederate/README.md) of that chart for ingress, toleration, resource options etc.