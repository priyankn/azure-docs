---
title: Delegate access governance to catalog creators in Azure AD entitlement management - Azure Active Directory
description: Learn how to delegate access governance from IT administrators to catalog creators and project managers so that they can manage access themselves.
services: active-directory
documentationCenter: ''
author: owinfreyatl
manager: karenhoran
editor: markwahl-msft
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: how-to
ms.subservice: compliance
ms.date: 07/6/2021
ms.author: owinfreyatl
ms.reviewer: mwahl
ms.collection: M365-identity-device-management


#Customer intent: As an administrator, I want to delegate access governance from IT administrators to department managers and project managers so that they can manage access themselves.

---

# Delegate access governance to catalog creators in Azure AD entitlement management

A catalog is a container of resources and access packages. You create a catalog when you want to group related resources and access packages. By default, a Global administrator or an Identity governance administrator can [create a catalog](entitlement-management-catalog-create.md), and can add additional users as catalog owners.

To delegate to users who aren't administrators, so that they can create their own catalogs, you can add those users to the Azure AD entitlement management-defined catalog creator role. You can add individual users, or you can add a group, whose members are then able to create catalogs.  After creating a catalog, they can subsequently add resources they own to their catalog.

## As an IT administrator, delegate to a catalog creator

Follow these steps to assign a user to the catalog creator role.

**Prerequisite role:** Global administrator, Identity Governance administrator or User administrator

1. In the Azure portal, click **Azure Active Directory** and then click **Identity Governance**.

1. In the left menu, in the **Entitlement management** section, click **Settings**.

1. Click **Edit**.

    ![Settings to add catalog creators](./media/entitlement-management-delegate-catalog/settings-delegate.png)

1. In the **Delegate entitlement management** section, click **Add catalog creators** to select the users or groups that you want to delegate this entitlement management role to.

1. Click **Select**.

1. Click **Save**.

## Allow delegated roles to access the Azure portal

To allow delegated roles, such as catalog creators and access package managers, to access the Azure portal to manage access packages, you should check the administration portal setting.

**Prerequisite role:** Global administrator or User administrator

1. In the Azure portal, click **Azure Active Directory** and then click **Users**.

1. In the left menu, click **User settings**.

1. Make sure **Restrict access to Azure AD administration portal** is set to **No**.

    ![Azure AD user settings - Administration portal](./media/entitlement-management-delegate-catalog/user-settings.png)

## Manage role assignments programmatically (preview)

You can also view and update catalog creators and entitlement management catalog-specific role assignments using Microsoft Graph.  A user in an appropriate role with an application that has the delegated `EntitlementManagement.ReadWrite.All` permission can call the Graph API to [list the role definitions](/graph/api/rbacapplication-list-roledefinitions) of entitlement management, and [list role assignments](/graph/api/rbacapplication-list-roleassignments) to those role definitions.

To retrieve a list of the users and groups assigned to the catalog creators role, the role with definition id `ba92d953-d8e0-4e39-a797-0cbedb0a89e8`, use the Graph query

```http
GET https://graph.microsoft.com/beta/roleManagement/entitlementManagement/roleAssignments?$filter=roleDefinitionId eq 'ba92d953-d8e0-4e39-a797-0cbedb0a89e8'&$expand=principal
```


## Next steps

- [Create and manage a catalog of resources](entitlement-management-catalog-create.md)
- [Delegate access governance to access package managers](entitlement-management-delegate-managers.md)
- [Delegate access governance to resource owners](entitlement-management-delegate.md)

