# Building Block View

## Level 1

Overall system

```plantuml
@startuml
!include <C4/C4_Container>

Person(user, "IAH user")
System_Ext(partner, "Technical user", "e.g. ServiceNow")

Person(developer, "IAH developer")

Boundary(cloud, "Industrial Asset Hub - cloud") {
  System_Ext(xfGW, "XF gateway")
  System(cdm, "Asset Hub - cloud backend")
  System(datadog, "Operational logging and monitoring")
}

Boundary(onsite, "Asset Gateway - field") {
  System(assetGW, "Asset gateway")
  System_Ext(assetLink, "Asset link", "e.g. SAT, SNMP")
  System_Ext(asset, "OT asset")
}


Rel(user, xfGW, "")
Rel(partner, xfGW, "Northbound API")
Rel(developer, xfGW, "")
Rel(developer, datadog, "")
Rel_R(xfGW, cdm, "")
Rel_L(datadog, cdm, "")
Rel_U(assetGW, xfGW, "Southbound API")
Rel_U(assetGW, cdm, "")
BiRel(assetLink, assetGW, "Asset link API")
Rel(assetLink, asset, "")
Rel(assetGW, asset, "")

Lay_U(assetLink, assetGW)

@enduml
```

### Components

### Interfaces

| Name           | Responsibility                                                              |
| -------------- | --------------------------------------------------------------------------- |
| Northbound API | REST API to integrate IAH with other third party applications and use cases |
| Southbound API | REST API to integrate custom gateways to interact with IAH                  |
| Asset link API | Protobuf API to integrate Asset links with the Asset Gateway                |

## Level 2

### XF gateway

```plantuml
@startuml
!include <C4/C4_Container>

Person(developer, "IAH developer")
Person(user, "IAH user")
System_Ext(partner, "Technical user", "e.g. ServiceNow")

System_Boundary(xfGw, "XF gateway") {
    Container_Ext(dev, "Developer console")
    Container_Ext(admin, "Admin console")
    Container_Ext(apiGw, "API gateway")
}
System(cdm, "Industrial Asset Hub - cloud")

System(assetGateway, "Asset gateway")

Rel(developer, dev, "")
Rel(user, admin, "")
Rel(user, apiGw, "")
Rel(partner, apiGw, "")

Rel_R(apiGw, cdm, "")

Rel_Back(apiGw, assetGateway, "")
Rel_R(assetGateway, cdm, "")

@enduml
```

### Asset Hub - Cloud Backend

```plantuml
@startuml
skinparam style strictuml

!include <C4/C4_Container>

System_Ext(xfGW, "XF gateway")

System_Boundary(cloud, "Asset Hub - cloud backend") {
  Container(kong, "Kong")
  System(inventory, "Inventory")
  Container(ui, "User interface")
  Container(docs, "User documentation")
  System(userConfig, "User configuration")
  System(onboarding, "Gateway onboarding")
  System(assetAuthentication, "Asset authentication")
  System(authorization, "Authorization")
  System(featureFlags, "Feature Flags")
  Container(discovery, "Discovery service")
  System(remoteConnect, "Remote access service")
  System(credentialManagement, "Credential management")
  System(jobManagement, "Job Management Service")
  System(fileImport, "File Import Service")
  System(contexthierarchy, "Context Hierarchy service")
  System(wfx, "Workflow engine")
  Container(datadogAgent, "Datadog agent")
}

System(datadog, "Operational logging and monitoring")

Rel(xfGW, kong, "")
Rel(xfGW, inventory, "")
Rel(xfGW, credentialManagement, "")
Rel(kong, ui, "")
Rel(kong, docs, "")
Rel(kong, userConfig, "")
Rel(kong, authorization, "")
Rel(kong, featureFlags, "")
Rel(kong, onboarding, "")
Rel(onboarding, assetAuthentication, "")
Rel(kong, assetAuthentication, "")
Rel(kong, discovery, "")
Rel(kong, remoteConnect, "")
Rel(kong, jobManagement, "")
Rel(kong, fileImport, "")
Rel(kong, wfx, "")
Rel(kong, contexthierarchy, "")
Rel(discovery, wfx, "")
Rel(remoteConnect, wfx, "")
Rel(remoteConnect, authorization, "")
Rel(contexthierarchy, authorization, "")
Rel(wfx, inventory, "")
Rel(onboarding, inventory, "")
Rel(remoteConnect, inventory, "")
Rel(credentialManagement, authorization, "")
Rel(discovery, inventory, "")
Rel(jobManagement, discovery, "")
Rel(jobManagement, remoteConnect, "")
Rel(fileImport, wfx, "")
Rel(fileImport, assetAuthentication, "")
Rel(fileImport, onboarding, "")
Rel(fileImport, inventory, "")
Rel(fileImport, authorization, "")
Rel(datadogAgent, datadog, "")

Lay_D(ui, docs)
Lay_D(docs, userConfig)
Lay_D(onboarding, assetAuthentication)
Lay_D(assetAuthentication, inventory)

@enduml
```

### Asset gateway

```plantuml
@startuml
!include <C4/C4_Container>

System_Ext(xfGW, "XF gateway")

System_Boundary(assetGW, "Asset gateway") {
  Container(authProxy, "Auth proxy agent")
  Container(discovery, "Discovery agent")
  Container(remoteConnect, "Remote access agent")
  Container(registry, "grpc registry")
  Container(genericAL, "Asset Link",  "Default IP Scanner")
}

System_Ext(assetLink, "Asset link", "e.g. SAT, SNMP")
System_Ext(asset, "OT asset")

Rel_U(authProxy, xfGW, "")
Rel_U(discovery, authProxy, "")
Rel_U(remoteConnect, authProxy, "")
Rel_L(discovery, registry, "")
Rel_D(discovery, assetLink, "")
Rel_D(discovery, genericAL, "")
Rel_U(assetLink, registry, "")
Rel_D(assetLink, asset, "")
Rel_D(remoteConnect, asset, "")
Rel_U(genericAL, registry, "")
@enduml
```

## Level 3

### Inventory

```plantuml
@startuml
!include <C4/C4_Container>

System_Ext(xfGW, "XF gateway")
System_Ext(cdmCloud, "Asset Hub - cloud backend")

System_Boundary(inventory, "Inventory") {
  Container(apigw, "Inventory API", "AWS API Gateway")

  Container(inventoryFunctions, "Inventory Functions")
  ContainerDb(db, "things")
}

Rel(xfGW, apigw, "")
Rel(cdmCloud, apigw, "")
Rel(apigw, inventoryFunctions, "")
Rel(inventoryFunctions, db, "")
@enduml
```

**Purpose/Responsibility:**

- provide API to manage asset descriptions
- deduplication check for each new asset to find existing occurrences
- provide API to manage custom properties and its values

**Quality-/Performance characteristics:**

- handle at least 20 tenants with each ~3000 assets
- get assets request should respond within 500ms, response can also be limited through pagination

**Fulfilled requirements:**

- tbd.

### Asset authentication

```plantuml
@startuml
!include <C4/C4_Container>

System_Boundary(xfGw, "XF gateway") {
  Container(apiGw, "API gateway")
}

System_Boundary(cloud, "Asset Hub - cloud backend") {
  System_Boundary(assetAuthentication, "Asset authentication") {
    Container(assetIam, "Asset IAM service")
    Container(challenge, "Challenge service")
    Container(s3, "S3 bucket")

    Rel_U(assetIam, s3, "")
    Rel_R(assetIam, challenge, "")
    Rel_L(assetIam, apiGw, "")
  }

  Container(kong, "Kong")

  Rel_U(kong, assetIam, "")
  Rel_R(apiGw, kong, "")
}

System_Boundary(assetGateway, "Asset gateway") {
  Container(authProxy, "Auth proxy agent")
}

Rel_U(authProxy, apiGw, "")
Rel_U(authProxy, kong, "")

@enduml
```

**Purpose/Responsibility:**

- provide API to manage root certificates
- provide API to issue an registration token
- provide API to exchange a valid leaf certificate for a token

**Quality-/Performance characteristics:**

- tbd.

**Fulfilled requirements:**

- tbd.

**Open issues/problems/risks:**

- hand over to XO FDS as contribution
- limit scope of technical user tokens
- (optional) link each asset to an individual server user

### Workflow Engine

```plantuml
@startuml
!include <C4/C4_Container>

Container(kong, "Kong")

System_Boundary(system, "Workflow engine") {
  Container(wfxGatekeeper, "WFX gatekeeper service")
  Container(wfx, "WFX service")
  ContainerDb(db, "WFX OSS")
}

Rel(kong, wfxGatekeeper, "")
Rel(wfxGatekeeper, wfx, "")
Rel(wfx, db, "")
@enduml
```

**Purpose/Responsibility:**

- multi-tenant workflow executor
- provide API to manage workflows and jobs

**Quality-/Performance characteristics:**

**Fulfilled requirements:**

- jobs can only be triggered for existing gateway assets

**Open issues/problems/risks:**

- tbd.

### Discovery

```plantuml
@startuml
!include <C4/C4_Container>

System_Boundary(cloud, "Asset Hub - cloud backend") {
  Container(discovery, "Discovery service")
  System(wfx, "Workflow engine")
  System(inventory, "Inventory")

  Rel_L(discovery, wfx, "")
  Rel_R(discovery, inventory, "")
}

System_Boundary(assetGateway, "Asset gateway") {
  Container(agent, "Discovery agent")
  Container(registry, "grpc registry")

  Rel_L(agent, registry, "")
}

System_Ext(al, "Asset link")

Rel_U(agent, wfx, "")
Rel_U(agent, inventory, "")
Rel_D(agent, al, "")
Rel_U(al, registry, "")

footer the diagram is focusing on the discovery and therefore ommiting the auth-proxy-agent, kong and  XF gateway which are in place between the agent and cloud services
@enduml
```

**Purpose/Responsibility:**

- managing discovery jobs according to the defined workflow
- forwarding discovered asset data to inventory

**Interface(s):**

- [Discovery REST API](https://code.siemens.com/common-device-management/discovery/discovery-service/-/blob/main/api/openapi-spec/v1-earlyaccess/discovery.openapi.yaml?ref_type=heads)
- [Discovery Asset Link gRPC API](https://industrial-assets.io/stable/developers/device-builder/specs/iah_discover.proto)

**Quality-/Performance characteristics:**

- tbd.

**directory/file location:**

- [Discovery service](https://code.siemens.com/common-device-management/discovery/discovery-service)
- [Discovery agent](https://code.siemens.com/common-device-management/discovery/discovery-agent)
- [Discovery workflow](https://code.siemens.com/common-device-management/documentation/apis/-/blob/main/workflows/discovery/workflow.json?ref_type=heads)

**Fulfilled requirements:**

- tbd.

**Open issues/problems/risks:**

- tbd.

### Remote Connect

**Documentation:**
<https://code.siemens.com/common-device-management/remote-access/remote-access-service/-/blob/main/README.md?ref_type=heads>

**Purpose/Responsibility:**

- provide API to manage remote connections.
- provides proxy for loading the remote connection based on authentication, authorization.

**Interface(s):**

- [Remote Access service - API](https://code.siemens.com/common-device-management/remote-access/remote-access-service/-/blob/main/api/openapi-spec/v1-earlyaccess/remote-access.openapi.yaml)

**Quality-/Performance characteristics:**

- 1000 concurrent connections across all tenants are supported.
- 100 concurrent connections per gateway are supported.

**Precondition:**

- The asset must have a gateway associated and IP address.

**directory/file location:**

- [Remote Access service](https://code.siemens.com/common-device-management/remote-access/remote-access-service)
- [Remote Access Agent](https://code.siemens.com/common-device-management/remote-access/remote-access-agent)

**Fulfilled requirements:**

- tbd.

**Open issues/problems/risks:**

### Gateway Onboarding

```plantuml
@startuml
!include <C4/C4_Container>

System_Boundary(xfGw, "XF gateway") {
  Container(apiGw, "API gateway")
}

System_Boundary(cloud, "Asset Hub - cloud backend") {
  System_Boundary(assetAuthentication, "Asset authentication")
  Container(kong, "Kong")
  Container(onboarding, "Gateway Onboarding")
  Container(inventory, "Inventory")

  Rel_U(kong, onboarding, "")
  Rel_U(onboarding, assetAuthentication, "")
  Rel_U(onboarding, inventory, "")
  Rel_R(apiGw, kong, "")
}

System_Boundary(assetGateway, "Asset gateway") {
  Container(authProxy, "Auth proxy agent")
}

Rel_U(authProxy, apiGw, "")
Rel_U(authProxy, kong, "")

@enduml
```

**Purpose/Responsibility:**

- provide API to manage onboarding/offboarding of Asset Gateways

**Interface(s):**

- [Onboarding REST API](https://code.siemens.com/common-device-management/onboarding/onboarding-service/-/blob/main/api/openapi-spec/v1-earlyaccess/gateway-onboarding.openapi.yaml?ref_type=heads)

**directory/file location:**

- [Onboarding service](https://code.siemens.com/common-device-management/onboarding/onboarding-service)

**Open issues/problems/risks:**

- tbd.

### Authorization

```plantuml
@startuml
!include <C4/C4_Container>

System_Boundary(xfGw, "XF gateway") {
  Container(apiGw, "API gateway")
  Container(xfUsers, "XF Identity Management")
  Container(xfEvents, "XF Event Notification")
}

System_Boundary(cloud, "Asset Hub - cloud backend") {
  System_Boundary(authorizationSystem, "Authorization") {

    Container(authorization, "Authorization API")
    Container(openfga, "OpenFga")
    ContainerDb(dbAuthz, "Authorization DB")
    ContainerDb(dbOpenfga, "OpenFGA DB")
  }
  Container(iahService, "IAH Service") {
    iahService ..> ["CDM Authorizer"] : uses
  }

  Container(kong, "Kong")

  Rel_D(openfga, dbOpenfga, "")
  Rel_D(authorization, dbAuthz, "")
  Rel_D(kong, authorization, "")
  Rel_U(iahService, authorization, "")
  Rel_D(authorization, openfga, "")
  Rel_L(apiGw, kong, "")
  Rel_D(xfEvents, authorization, "notify about user deletion")
  Rel_D(authorization, xfUsers, "fetch xf users")
}

@enduml
```

**Purpose/Responsibility:**

- provide API to manage authorization of IAH users

**Interface(s):**

- [Authorization REST API](https://code.siemens.com/common-device-management/iam/authorization-service/-/blob/main/api/openapi-spec/v1/authorization.openapi.yaml)

**directory/file location:**

- [Authorization service](https://code.siemens.com/common-device-management/IAM/authorization-service)
- [OpenFGA](https://code.siemens.com/common-device-management/IAM/openfga)

**Open issues/problems/risks:**

- tbd.

### Feature Flags

```plantuml
@startuml
!include <C4/C4_Container>

System_Boundary(cloud, "Asset Hub - cloud backend") {
  Container(iahService, "golang service") {
    iahService ..>  [unleash-client-go] : uses
  }
  Container(unleash, "Unleash Proxy")

}

package "Browser on client PC" {
  [IAH UI]
}

System_Boundary(code, "code.siemens.com") {
  [Unleash API]
  [Feature Flag Dev]
  note top of [Feature Flag Dev]
    Gitlab Repositories: (dev, system, perf)
  end note

  [IAH Feature Flag]
  note top of [IAH Feature Flag]
    Gitlab Repositories: (demo, prod)
  end note
}


Rel_U(iahService, [Unleash API], "feature flags")
Rel_L(unleash, [Unleash API], "feature flags")
Rel_U([IAH UI], unleash, "")

Rel_L([Unleash API], [Feature Flag Dev], "")
Rel_L([Unleash API], [IAH Feature Flag], "")

@enduml
```

**Purpose/Responsibility:**

- provide functionalities to manage feature flags

**Interface(s):**

**directory/file location:**

**Open issues/problems/risks:**

- tbd.

### Job Management Service

**Documentation:**
<https://code.siemens.com/common-device-management/workflows/job-management-service/-/blob/main/README.md>

**Purpose/Responsibility:**

- Provide API to retrieve all IAH job since a specified date.

**Interface(s):**

- [Job Management Service - API](https://code.siemens.com/common-device-management/workflows/job-management-service/-/blob/main/api/openapi-spec/v1-earlyaccess/job-management.openapi.yaml)

**Quality-/Performance characteristics:**

- TBD

**Precondition:**

- All the services should have harmonized Job Management APIs

**Directory/File location:**

- [Job Management Service](https://code.siemens.com/common-device-management/workflows/job-management-service)

**Fulfilled requirements:**

- TBD

**Open issues/problems/risks:**

- TBD

### Job Scheduling Service

**Documentation:**
<https://code.siemens.com/common-device-management/workflows/job-scheduling-service/-/blob/main/README.md>

**Purpose/Responsibility:**

- Provide APIs to schedule tasks in IAH to be executed at sepcified schedule. APIs are intended to be consumed by other services like discovery service to schedule discovery scans.

**Interface(s):**

- [Job Scheduling Service - API](https://code.siemens.com/common-device-management/workflows/job-scheduling-service/-/blob/main/api/openapi-spec/v1-earlyaccess/job-scheduling.openapi.yaml)

**Quality-/Performance characteristics:**

- TBD

**Precondition:**

- None

**Directory/File location:**

**Fulfilled requirements:**

- TBD

**Open issues/problems/risks:**

- TBD

### Generic IP Scanner

**Purpose/Responsibility:**

- Acts as a default asset link for asset gateway.
- This uses underline nmap for doing a ICMP Ping scan with UDP and MAC Identification.

**Quality-/Performance characteristics:**

- tbd

**Precondition:**

- The IP range should be provided for the scan.

**directory/file location:**

**Fulfilled requirements:**

- tbd.

**Open issues/problems/risks:**

- tbd

### User interface

```plantuml
@startuml
!include <C4/C4_Container>

System_Ext(xfGW, "XF gateway")

System_Boundary(cloud, "Asset Hub - cloud backend") {
  Container(inventory, "Inventory service")
  Container(discovery, "Discovery service")
  Container(remoteConnect, "Remote connect")
  Container(gatewayOnboarding, "Gateway onboarding")
  Container(featureFlags, "Feature flags")
  Container(authorization, "Authorization")
  Container(userConfig, "User configuration")
}

Container(ui, "User interface")

Rel(xfGW, ui, "")

Rel(ui, inventory, "")
Rel(ui, discovery, "")
Rel(ui, remoteConnect, "")
Rel(ui, gatewayOnboarding, "")
Rel(ui, featureFlags, "")
Rel(ui, authorization, "")
Rel(ui, userConfig, "")

@enduml
```

**Purpose/Responsibility:**

- display information collected from cloud backend in user's browser
- CRUD operations for configuration settings per user

**Quality-/Performance characteristics:**

- 3000 assets per list
- maximum respond time 500ms
- maximum memory consumption 500MB

### Credential Management

```plantuml
@startuml
!include <C4/C4_Container>

System_Ext(xfGW, "XF gateway")
System_Ext(cdmCloud, "Asset Hub - cloud backend")

System_Boundary(credentialManagement, "Credential Management") {
  Container(apigw, "Credential Management API", "AWS API Gateway")

  Container(CredentialManagementCRUD, "Credential Management operations")
  ContainerDb(db, "schema and instances")
}

Rel(xfGW, apigw, "")
Rel(cdmCloud, apigw, "")
Rel(apigw, CredentialManagementCRUD, "")
Rel(CredentialManagementCRUD, db, "")
@enduml
```

**Purpose/Responsibility:**

- provide API to manage schemas
- provide API to manage instances for the schemas
- maintain assets to instance mapping

**Interface(s):**

**Quality-/Performance characteristics:**

- Credentials stored for 20 tenants 3000 assets
- 1000 credentials can stored for scanning process

**directory/file location:**

**Fulfilled requirements:**

- tbd.

**Open issues/problems/risks:**

### File Import Service

**Purpose/Responsibility:**

- Provide APIs to import excel template file with asset data in IAH.
- Providee APIs to manage file import jobs.

**Interface(s):**

**Quality-/Performance characteristics:**

- TBD

**Precondition:**

- None

**Directory/File location:**

**Fulfilled requirements:**

- TBD

**Open issues/problems/risks:**

- TBD

### Context Hierarchy Service

**Documentation:**

**Purpose/Responsibility:**

- provide API to manage user context based hierarchies.

**Interface(s):**

**Quality-/Performance characteristics:**

- 10 context based hierarchies are supported per tenant.
- 1000 nodes per hierarchy is supported.

**directory/file location:**

**Fulfilled requirements:**

- tbd.

**Open issues/problems/risks:**

- tbd.
