# PingDelegator

## Running
In a development or sandbox environment, the helm chart can be run with a valid registered devops license key (https://pingidentity-devops.gitbook.io/devops/getstarted/devopsregistration).  Make sure the `PING_IDENTITY_DEVOPS_USER` and `PING_IDENTITY_DEVOPS_KEY` environment variables are set

Requires [PingDirectory](../pingdirectory) and a token provider ([PingFederate]](../pingfederate)) to use.  Example commands for all components:

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
 ./../pingdirectory
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
 ./../pingfederate
```

### PingDelegator
```shell
helm install \
pingdelegator --debug \
--set pingdelegator.publicHostname=localhost \
--set pingdelegator.tokenProvider.hostname=localhost \
--set pingdelegator.tokenProvider.port=9031 \
 ./
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

## Testing

Tested with **PingDelegator 4.2**