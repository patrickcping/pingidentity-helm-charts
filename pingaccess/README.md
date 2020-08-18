# PingAccess

Remember to add the repo before installing the chart
```shell
helm repo add pingidentity-pc https://patrickcping.github.io/ping-identity-helm-charts-repo/
```

## Use Devops Key
In a development or sandbox environment, the helm chart can be run with a valid registered devops license key (https://pingidentity-devops.gitbook.io/devops/getstarted/devopsregistration).  Make sure the `PING_IDENTITY_DEVOPS_USER` and `PING_IDENTITY_DEVOPS_KEY` environment variables are set

```shell
helm install \
pingaccess --debug \
--set license.useDevOpsKey=true \
--set license.devOpsKey.user=${PING_IDENTITY_DEVOPS_USER} \
--set license.devOpsKey.key=${PING_IDENTITY_DEVOPS_KEY} \
--set license.acceptEULA=yes \
pingidentity-pc/pingaccess
```

## Use provided License file
In a controlled environment, the helm chart can be run with a valid license file.  Add the license file as a secret as shown:
```shell

kubectl create secret generic pingaccess-license --from-file ./pingaccess.lic

helm install \
pingaccess --debug \
--set license.licenseSecretName=pingaccess-license \
--set license.acceptEULA=yes \
pingidentity-pc/pingaccess
```

## Chart Configuration

| Parameter | Description | Default |
|--|--|--|
| TODO | TODO | TODO |

## PingAccess Configuration Profile

By default this chart loads sample PingAccess configuration on startup.  These are layered as:

| Configuration Layer | Server Profile |
|--|--|
| 1 | https://github.com/pingidentity/pingidentity-server-profiles/tree/master/getting-started/pingaccess |

You can add additional layers or change to your own configuration repository by modifying the `SERVER_PROFILE_*` environment variables in `pingaccess.envs` of the chart configuration

## Injecting Ping Environment Variables

You can inject your own environment variables to modify the behaviour of the Ping Docker image, or when using environment variables in your own server profiles.  For this, you can create your own values.yaml file and insert any environment variables you wish under `pingaccess.envs` of the chart configuration.  For example:

```
pingaccess:
  envs:
    SERVER_PROFILE_URL: https://github.com/myuser/mycustomrepo.git 
    SERVER_PROFILE_PATH: my/path/to/pingaccess
    SERVER_PROFILE_BRANCH: master
    MY_SERVER_PROFILE_VAR: "your value here"
```

For available image environment variables, see [Ping Identity documentation](https://pingidentity-devops.gitbook.io/devops/dockerimagesref/pingaccess#environment-variables)

## Clustering Example

### Admin Console
```shell
TBC
```

### Engines:
```shell
TBC
```
