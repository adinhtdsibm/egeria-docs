---
hide:
- toc
---

<!-- SPDX-License-Identifier: CC-BY-4.0 -->
<!-- Copyright Contributors to the Egeria project. -->

# Asset

An **asset** is either a digital or physical object/property that provides value to the
organization that owns it. Examples of an asset include:

- Data sources such as databases, files and data feeds.
- IT infrastructure and applications that automate many aspects of an organization's operation.
- APIs that provide access to the services offered by the organization.
- Analytical models and processes that differentiate an organization from its competitors or ensure it is operating legally and ethically.
- Buildings and other locations.
- Physical objects that have a unique identity (eg a serial number).

Much governance is centered around an organization's assets since they
represent tangible value. This involves maintaining information about each asset
and managing events related to the asset in order to keep it
protected and to get the maximum value from it.

Egeria is particularly focused on providing the ability to maintain the
information necessary for managing digital assets and the infrastructure that supports them.
It also has a flexible model to allow
the definition of asset to be expanded to include a broader range of physical assets.

## Open metadata types

The information about an asset that is used to describe its characteristics and how it should be managed
(that is, the asset's metadata) is stored in a sub-graph of open metadata instances (entities and relationships)
with the [Asset](/egeria-docs/types/0/0010-base-model/#asset) entity
at the root. The Asset entity contains a small amount of information that merely captures the
existence of the real asset. Then other entities are linked to it to add more information.
It is likely that this additional information is identified, captured and stored by different
tools. The open metadata services gather this information together and distribute it to provide
the most complete view of the asset's properties.

More information on the types of attachments that can be added to an asset can be found [here](../../../../../open-metadata-publication/website/cataloging-assets/asset-catalog-contents.md).

Inheriting from Asset is a hierarchy of increasingly-specialized definitions
for different types of Assets. Each definition adds more properties
about the Asset:

![Asset hierarchy](asset-hierarchy.png)

**[Area 2](/egeria-docs/types/2)** is where the asset hierarchy is built out.

## Accessing asset content through connectors

Egeria provides an open framework for accessing the content of digital assets and the
information about them.
It is called the [Open Connector Framework (OCF)](/egeria-docs/frameworks/ocf)
and it provides specialized connectors (clients) for accessing specific types of Assets
and the information about them.

The type of connector to use is specified in the [connection](connection.md)
entity that is linked to the Asset.

[Model 0205](/egeria-docs/types/2/0205-connection-linkage)
in the open metadata types shows how
an Asset is associated with a [connection](connection.md) object.
The connection object provides the properties necessary to create a connector to access the asset's contents.

## APIs and events for managing Asset information (metadata)

Egeria's [Open Metadata Access Services (OMAS)](/egeria-docs/services/omas) provide the specialized services for
managing Assets. Each OMAS focuses on a particular part of the asset lifecycle or
person/tool that is working with the Assets.

Some examples:

| OMAS | Description |
|---|---|
| [Analytics Modeling OMAS](/egeria-docs/services/omas/analytics-modeling) | enables business intelligence and data virtualization tools to maintain information about the data views and reporting Assets they are maintaining. |
| [Asset Catalog OMAS](/egeria-docs/services/omas/asset-catalog) | provides a search service for locating Assets. |
| [Asset Consumer OMAS](/egeria-docs/services/omas/asset-consumer) | provides a service for accessing the content of an Asset, extracting additional information that is known about the Asset and providing feedback about the Asset. It is designed for tools that consume assets to support the work of their users. These users can provide feedback on the asset description and the resource that it describes. |
| [Asset Manager OMAS](/egeria-docs/services/omas/asset-manager) | provides a service for exchanging metadata about assets and related information with a third party [asset manager](../server-capabilities/asset-manager.md). This API supports the many-to-many correlation of identifiers used in the third party asset manager and the open metadata ecosystem. |
| [Asset Owner OMAS](/egeria-docs/services/omas/asset-owner) | provides a service for the owner of an Asset to classify and manage the asset, and understand how it is being used by the organization. |
| [Discovery Engine OMAS](/egeria-docs/services/omas/discovery-engine) | provides a service for adding annotations to an asset's information that has been determined by specific analysis of the Asset's contents by a [discovery service](/egeria-docs/frameworks/odf/discovery-service). |
| [Data Manager OMAS](/egeria-docs/services/omas/data-manager) | enables a data manager (such as a database or file system) to maintain information about the assets it stores. |
| [Governance Engine OMAS](/egeria-docs/services/omas/governance-engine) | provides the metadata services for [governance action services](/egeria-docs/frameworks/gaf/governance-action-service) that verify, enhance and correct the properties of assets and their associated elements. |
| [IT Infrastructure OMAS](/egeria-docs/services/omas/it-infrastructure) | provides a service for maintaining information about the IT assets and supporting infrastructure owned or used by an organization. |
| [Data Science OMAS](/egeria-docs/services/omas/data-science) | provides a service for maintaining information about analytical models and related assets such as python notebooks. |

## Sharing information about assets

Egeria's [Open Metadata Repository Services (OMRS)](/egeria-docs/services/omrs) provides the ability to store and extract information about
Assets in a distributed collection of servers called an
[open metadata repository cohort](/egeria-docs/services/omrs/cohort).
The cohort provides both peer-to-peer exchange of metadata via an event bus topic
and federated queries between different members of the cohort.
Egeria provides a [metadata server](/egeria-docs/concepts/metadata-server),
a [metadata access point](/egeria-docs/concepts/metadata-access-point) and a
[repository proxy](/egeria-docs/concepts/repository-proxy) server that are all able to
join a cohort. The repository proxy supports the integration of third party
servers (typically [asset managers](../server-capabilities/asset-manager.md)) into the cohort.
The mapping between the third party server's APIs and the open metadata APIs in this case is
implemented in an [repository connector](/egeria-docs/connectors/repository-connector).

It is also possible to manage the exchange of Asset metadata with other types of third party technologies
using the [Open Metadata Integration Services (OMIS)](/egeria-docs/services/omis) running
in an [integration daemon](/egeria-docs/concepts/integration-daemon).
Using this pattern is simpler to integrate but involves maintaining a copy of the third party technology's
metadata in a [metadata server](/egeria-docs/concepts/metadata-server) that can then
join one or more open metadata repository cohorts to share this metadata more broadly.
The mapping between the third party technology's APIs and the open metadata APIs in this case is
implemented in an [integration connector](/egeria-docs/connectors/integration-connector).

--8<-- "snippets/abbr.md"