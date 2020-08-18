# PingDataConsole

Remember to add the repo before installing the chart
```shell
helm repo add pingidentity-pc https://patrickcping.github.io/ping-identity-helm-charts-repo/
```

## Running

```shell
helm install \
pingdataconsole --debug \
pingidentity-pc/pingdataconsole
```

## Chart Configuration

| Parameter | Description | Default |
|--|--|--|
| TODO | TODO | TODO |

## PingDataConsole Configuration Profile

By default this chart loads sample PingDataConsole configuration on startup.  These are layered as:

| Configuration Layer | Server Profile |
|--|--|
| 1 | https://github.com/pingidentity/pingidentity-server-profiles/tree/master/baseline/pingdataconsole |

You can add additional layers or change to your own configuration repository by modifying the `SERVER_PROFILE_*` environment variables in `pingdataconsole.envs` of the chart configuration

## Injecting Ping Environment Variables

You can inject your own environment variables to modify the behaviour of the Ping Docker image, or when using environment variables in your own server profiles.  For this, you can create your own values.yaml file and insert any environment variables you wish under `pingdataconsole.envs` of the chart configuration.  For example:

`
pingdataconsole:
  envs:
    SERVER_PROFILE_URL: https://github.com/myuser/mycustomrepo.git 
    SERVER_PROFILE_PATH: my/path/to/pingdataconsole
    SERVER_PROFILE_BRANCH: master
    MY_SERVER_PROFILE_VAR: "your value here"
`

For available image environment variables, see [Ping Identity documentation](https://pingidentity-devops.gitbook.io/devops/dockerimagesref/pingdataconsole#environment-variables)