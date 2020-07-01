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
| PingCentral | Product | Delegated Application Management UI | In development | N/a |
| [PingDataConsole](pingdataconsole/) | Product | PingData Admin Console | Available (Beta) | Not required |
| PingDataGovernance | Product | Fine-grain Authorisation PDP | Not available | N/a |
| PingDataGovernance PAP | Product | Fine-grain Authz PAP | Not available | N/a |
| PingDataSync | Product | Data Synchronisation Engine | Not available | N/a |
| PingDirectoryProxy | Product | Directory Proxy | Not available | N/a |
