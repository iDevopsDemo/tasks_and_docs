# Solution Strategy

Architecture context, goals and guidelines

## Architecture Goals

Target audience: product manager, product owner, architects, teams.

The software consists of two basic components.

- The Industrial Asset Hub is a SaaS offering. It can be experienced as human interactive user via a graphical user interface and/or through a restful APIs by a technical user.

- The Asset Gateway is a field component. It provides an API which allows to integrate Asset Links. Asset Links transcribe the vendor/asset specific interfaces/protocols to a well-defined normalized API.

High Level system Overview

### Offering as SaaS

Industrial Asset Hub is provided as SaaS for V1.0 and exclusively provided and operated by SIEMENS. Even so the future may demand other deployment and operation models these are not considered to be design driving for this iteration.

### Asset agnostic middle ware

The Industrial Asset Hub is built agnostic to the specific asset types and vendors. It provides a lightweight abstraction interface which normalizes the different interfaces and models to an Industrial Asset Hub specification.

### Field components

The heterogenous customer network setups in combination with network cell protection concepts demand the deployment of field components to interact with the shopfloor devices. In case of the Industrial Asset Hub these consist of the so-called Asset Gateway as well as of a bunch of Asset Links.
Field components are provided as

- Industrial Edge Apps which can be accessed via the Industrial Asset Hub.
- Docker compose applications which are provided for operation in 3rd party edge environments.

### Openness

The Industrial Asset Hub is an open ecosystem platform. It provides openness in two dimensions as there are:

- An openness for assets is provided via a well-defined abstraction interface. This allows 3rd parties to integrate with Industrial Asset Hub without the need to change the platform. New asset types can be introduced by device builders. Device builders are supported as participants in the IAH eco system via a device builder kit consisting of documentation, binaries, source code, templates.
- IAH exposes all its functionalities via RESTful APIs. These allow on one hand solution partners to build services on top of IAH and on the other hand an integration with enterprise services on customer side.

### Extensibility

Compliance with standards
The Industrial Asset Hub has no compatibility demands according to existing standards. Non the less it needs to provide extension points and models which allow to integrate with evolving standards like e.g.

- Asset Administration Shell
- OI4.0 Initiative
- Anchor Model
- ….

Restful API of Industrial Asset Hub services
From release V1.0 on it is intended the backend APIs are expected to be kept downward compatible. Since there is still a quick evolvement of the service and the customer penetration will be limited for this release the APIs are still marked as `v1-earlyaccess` which allows in a case-by-case discussion to incompatibly adapt or deprecate the one or other API.

Protobuf device builder interface
From release V1.0 on it is intended to keep the Asset Gateway’s gRPC interface downward compatible. Since there is still a quick evolvement of the service and the customer penetration will be limited for this release the APIs can be incompatibly adapted or deprecate which is to be decided in a case-by-case discussion.

### Security

Industrial Asset Hub is built as a multi-tenant SaaS offering. It implements a multi-layer cloud security concept. The cloud services are developed according to internal regulations and comply with ISO 27001.

### Deployment

Industrial Asset Hub is offered as SaaS. Hence it is deployed and operated by the project organization.
Operation by third parties is not intended as of now.

**Cloud Services**<br>
The cloud services are deployed and operated on AWS using a gitops approach.

**Field Services**<br>
Field services are hosted on edge computing infrastructures. This can be SIEMENS` Industrial Edge but as well be 3rd party infrastructures. The Industrial Asset Hub provides dockerized services for these.

## Reuse and Open-Source Strategy

### OSS Usage

Wherever possible Industrial Asset Hub relies on 3rd party / open-source software components. Some of them mentioned here.

#### WFX - Workflow Execution

The workflow execution engine and model player serves as the central job engine to connect the field services to the cloud. It helps distributing the services from edge to cloud in a reliable way.

- Firewall friendly construction since the agent is exclusively using outgoing communications to connect with the backend workflow executor.
- Reliable and resumable workflows for longer running operations can be modeled.
- The WFX allows to model complex workflows and to interact with them

### OSS Contribution

#### SDK - Software Development Kit

Industrial Asset Hub is a device vendor agnostic platform. For device builder support a software development kit (SDK) consisting of documentation, code and binaries is provided as open source.

## Dependencies

### Xcelerator Operation Foundational Services

Industrial Asset Hub as part of Xcelerator Operations founds its service on the so-called Foundational Services (FDS) /R6/.

### Industrial Edge

Industrial Asset Hub is built as a ready to use offering once using Industrial Edge as a gateway. Hence all gateway services from IAH are provided as Industrial Edge apps. As well asset links from SIEMENS are provided as Industrial Edge apps.
3rd party providers e.g. from Asset Links are actively encouraged to publish their applications for Industrial Edge /R7/.

## Reference Architecture

### Mid-Term Overview

## Architecture guidelines and principles

### Xcelerator Operations (XO) – Well-Architected

If not differently mentioned the product complies with Xcelerator Operations.

#### Adaption of the service Catalog

#### Well-Architected Framework (XO)

#### Compatibility

Customer facing contracts are kept compatible over time.
Industrial Asset Hub provides two programming interfaces.

- RESTful APIs for the backend services
- gRPC interface for the Asset links

Both are to be kept backward compatible over time. Versioning of the APIs allow their life cycle management.
