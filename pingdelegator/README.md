# PingDelegator

Remember to add the repo before installing the chart
```shell
helm repo add pingidentity-pc https://patrickcping.github.io/ping-identity-helm-charts-repo/
```

## Running
In a development or sandbox environment, the helm chart can be run with a valid registered devops license key (https://pingidentity-devops.gitbook.io/devops/getstarted/devopsregistration).  Make sure the `PING_IDENTITY_DEVOPS_USER` and `PING_IDENTITY_DEVOPS_KEY` environment variables are set

Requires [PingDirectory](../pingdirectory) and a token provider such as [PingFederate]](../pingfederate) to use.  Example commands for all components:

### PingDirectory
```shell
helm install \
pingdelegator-pingdirectory --debug \
--set license.useDevOpsKey=true \
--set license.devOpsKey.user=${PING_IDENTITY_DEVOPS_USER} \
--set license.devOpsKey.key=${PING_IDENTITY_DEVOPS_KEY} \
--set license.acceptEULA=yes \
--set pingdirectory.envs.SERVER_PROFILE_PATH=baseline/pingdirectory \
--set persistentvolume.enabled=false \
pingidentity-pc/pingdirectory
```

### PingFederate
```shell
helm install \
pingdelegator-pingfederate --debug \
--set license.useDevOpsKey=true \
--set license.devOpsKey.user=${PING_IDENTITY_DEVOPS_USER} \
--set license.devOpsKey.key=${PING_IDENTITY_DEVOPS_KEY} \
--set license.acceptEULA=yes \
--set pingfederate.envs.SERVER_PROFILE_PATH=baseline/pingfederate \
pingidentity-pc/pingfederate
```

### PingDelegator
```shell
helm install \
pingdelegator --debug \
--set pingdelegator.publicHostname=localhost \
--set pingdelegator.tokenProvider.hostname=localhost \
--set pingdelegator.tokenProvider.port=9031 \
pingidentity-pc/pingdelegator
```

## Chart Configuration

| Parameter | Description | Default |
|--|--|--|
| TODO | TODO | TODO |

## PingDelegator Configuration Profile

By default this chart loads sample PingDelegator configuration on startup.  These are layered as:

| Configuration Layer | Server Profile |
|--|--|
| 1 | https://github.com/pingidentity/pingidentity-server-profiles/tree/master/baseline/pingdelegator |

You can add additional layers or change to your own configuration repository by modifying the `SERVER_PROFILE_*` environment variables in `pingdelegator.envs` of the chart configuration

## Injecting Ping Environment Variables

You can inject your own environment variables to modify the behaviour of the Ping Docker image, or when using environment variables in your own server profiles.  For this, you can create your own values.yaml file and insert any environment variables you wish under `pingdelegator.envs` of the chart configuration.  For example:

```
pingdelegator:
  envs:
    SERVER_PROFILE_URL: https://github.com/myuser/mycustomrepo.git 
    SERVER_PROFILE_PATH: my/path/to/pingdelegator
    SERVER_PROFILE_BRANCH: master
    MY_SERVER_PROFILE_VAR: "your value here"
```

For available image environment variables, see [Ping Identity documentation](https://pingidentity-devops.gitbook.io/devops/dockerimagesref/pingdelegator#environment-variables)
