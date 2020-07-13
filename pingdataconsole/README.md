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