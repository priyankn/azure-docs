---
title: Manage VNet endpoints - Azure CLI - Azure Database for MySQL
description: This article describes how to create and manage Azure Database for MySQL VNet service endpoints and rules using Azure CLI command line.
ms.service: mysql
ms.subservice: single-server
author: mksuni
ms.author: sumuth
ms.devlang: azurecli
ms.topic: how-to
ms.date: 06/20/2022
ms.custom: devx-track-azurecli
---

# Create and manage Azure Database for MySQL VNet service endpoints using Azure CLI

[!INCLUDE[applies-to-mysql-single-server](../includes/applies-to-mysql-single-server.md)]
Virtual Network (VNet) services endpoints and rules extend the private address space of a Virtual Network to your Azure Database for MySQL server. Using convenient Azure CLI commands, you can create, update, delete, list, and show VNet service endpoints and rules to manage your server. For an overview of Azure Database for MySQL VNet service endpoints, including limitations, see [Azure Database for MySQL Server VNet service endpoints](concepts-data-access-and-security-vnet.md). VNet service endpoints are available in all supported regions for Azure Database for MySQL.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [azure-cli-prepare-your-environment.md](../../../includes/azure-cli-prepare-your-environment.md)]

> [!NOTE]
> Support for VNet service endpoints is only for General Purpose and Memory Optimized servers.
> In case of VNet peering, if traffic is flowing through a common VNet Gateway with service endpoints and is supposed to flow to the peer, please create an ACL/VNet rule to allow Azure Virtual Machines in the Gateway VNet to access the Azure Database for MySQL server.

## Configure Vnet service endpoints for Azure Database for MySQL

The [az network vnet](/cli/azure/network/vnet) commands are used to configure Virtual Networks.

If you have multiple subscriptions, choose the appropriate subscription in which the resource should be billed. The account must have the necessary permissions to create a virtual network and service endpoint.
Service endpoints can be configured on virtual networks independently, by a user with write access to the virtual network.

To secure Azure service resources to a VNet, the user must have permission to "Microsoft.Network/virtualNetworks/subnets/joinViaServiceEndpoint/" for the subnets being added. This permission is included in the built-in service administrator roles, by default and can be modified by creating custom roles.

Learn more about [built-in roles](../../role-based-access-control/built-in-roles.md) and assigning specific permissions to [custom roles](../../role-based-access-control/custom-roles.md).

VNets and Azure service resources can be in the same or different subscriptions. If the VNet and Azure service resources are in different subscriptions, the resources should be under the same Active Directory (AD) tenant. Ensure that both the subscriptions have the **Microsoft.Sql** and **Microsoft.DBforMySQL** resource providers registered. For more information refer [resource-manager-registration][resource-manager-portal]

> [!IMPORTANT]
> It is highly recommended to read this article about service endpoint configurations and considerations before running the sample script below, or configuring service endpoints. **Virtual Network service endpoint:** A [Virtual Network service endpoint](../../virtual-network/virtual-network-service-endpoints-overview.md) is a subnet whose property values include one or more formal Azure service type names. VNet services endpoints use the service type name **Microsoft.Sql**, which refers to the Azure service named SQL Database. This service tag also applies to the Azure SQL Database, Azure Database for PostgreSQL and MySQL services. It is important to note when applying the **Microsoft.Sql** service tag to a VNet service endpoint it configures service endpoint traffic for all Azure Database services, including Azure SQL Database, Azure Database for PostgreSQL and Azure Database for MySQL servers on the subnet.

## Sample script

[!INCLUDE [cli-launch-cloud-shell-sign-in.md](../../../includes/cli-launch-cloud-shell-sign-in.md)]

### Run the script

:::code language="azurecli" source="~/azure_cli_scripts/mysql/create-mysql-server-vnet/create-mysql-server.sh" id="FullScript":::

## Clean up resources

[!INCLUDE [cli-clean-up-resources.md](../../../includes/cli-clean-up-resources.md)]

```azurecli
az group delete --name $resourceGroup
```

<!-- Link references, to text, Within this same GitHub repo. -->
[resource-manager-portal]: ../../azure-resource-manager/management/resource-providers-and-types.md
