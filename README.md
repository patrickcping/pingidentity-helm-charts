# Sample Ping Identity Helm Charts

This repository provides sample Helm charts for Ping Identity products for community use.

These helm charts are not in a finished or production-ready state, but are intended to be a good starting point and can be used and altered as required.

Note: These charts are development / POC quality and originally put together as a learning experience.  Pull requests and issues welcome but don't expect a quick response!

## Charts

| Chart | Type | Capability | Status | Scalable |
|--|--|--|--|--|
| [PingFederate](pingfederate/) | Product | SSO / Authentication Authority | Available (Beta) | Yes |
| [PingAccess](pingaccess/) | Product | Medium/Course grain Authorisation Gateway / PEP | Available (Beta) | No (TBC) |
| [PingDirectory](pingdirectory/) | Product | User/Device/Consent/Organisation Directory | Available (Beta) | Yes |
| [PingDelegator](pingdelegator/) | Product | Delegated User Management UI | Available (Beta) | Yes |
| [PingCentral](pingcentral/) | Product | Delegated Application Management UI | Available (Beta) | Yes |
| [PingDataConsole](pingdataconsole/) | Product | PingData Admin Console | Available (Beta) | Not required |
| PingDataGovernance | Product | Fine-grain Authorisation PDP | Not available | N/a |
| PingDataGovernance PAP | Product | Fine-grain Authz PAP | Not available | N/a |
| PingDataSync | Product | Data Synchronisation Engine | Not available | N/a |
| PingDirectoryProxy | Product | Directory Proxy | Not available | N/a |

## Add the Repository

```shell
helm repo add pingidentity-pc https://patrickcping.github.io/ping-identity-helm-charts-repo/
helm repo update
helm repo list
```

Search for a Ping chart
```shell
helm search repo ping
```

## Injecting Ping Environment Variables

You can inject your own environment variables to modify the behaviour of the Ping Docker image, or when using environment variables in your own server profiles.  For this, you can create your own values.yaml file and insert any environment variables you wish under (for example) `pingfederate.envs` of the chart configuration.  For example:

`
pingfederate:
  envs:
    SERVER_PROFILE_URL: https://github.com/myuser/mycustomrepo.git 
    SERVER_PROFILE_PATH: my/path/to/pingfederate
    SERVER_PROFILE_BRANCH: master
    MY_SERVER_PROFILE_VAR: "your value here"
`

## Waiting for dependent services

For an example of waiting for a dependent service, such as PingDirectory, see the example [here](https://github.com/patrickcping/ping-helm-kustomize-example)