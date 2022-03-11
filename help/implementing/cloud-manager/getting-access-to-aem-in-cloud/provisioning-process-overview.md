---
title: Provisioning Process - Overview
description: 預配過程 — 概述
source-git-commit: 2f40b11a20a4ebb3ff7d9d2835bbe56e91ddf96d
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 7%

---


# AEMas a Cloud Service:登機和訪問

此頁列出有關Experience Manageras a Cloud Service的預配過程的自助資源。

## AEM as a Cloud Service Provisioning Process Overview

本節提供下列主題的重要文章：

* 訪問AEMas a Cloud Service
* Adobe Experience Manager as a Cloud Service Onboarding and Provisioning Process
* 幫助和資源


### 訪問AEMas a Cloud Service

Once auto-provisioning is complete:

* 授予的訪問權 — Adobe將在AdobeIdentity Management系統(IMS)內建立一個組織
* 預設情況下，指定管理員將擁有管理員權限
* 管理員可以通過Admin Console為其他團隊成員添加用戶和角色
* 查看用戶基於角色的權限，以確定雲管理器中的權限分配

> ![procesoverview.jpg](./assets/processOverview.jpg)


For more information, please visit [Onboarding to Experience Manager as a Cloud Service on Experience League](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html?lang=en)

### 資源和連結

* [AEM as a Cloud Service 的 IMS 支援](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en)
* [Role Based Permissions in Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/role-based-permissions.html?lang=en#what-is-required)
* [存取 Experience Manager as a Cloud Service ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=en#getting-access)


## Adobe Experience Manager as a Cloud Service登陸進程

### 1. Purchase order Triggers autoprovisioning.

### 2. Onboard Organizations to Adobe Admin Console:

![procesoverview2.jpg](./assets/processOverview2.jpg)

* 系統管理員：
   * 設定AEM計畫和環境。
   * 導航至管理任務的Admin Console。
   * Claims a domain to confirm ownership of respective domain
   * 設定用戶目錄。
   * IDP配置。
* AEM 管理員:
   * 管理本地組、權限和權限。

### 3. Onboard Users and Manage Access in Admin Console:

![procesoverview3.jpg](./assets/processOverview3.jpg)

Three methods to onboard users, depending on size and preference:
* 在Admin Console中手動建立用戶
* 上載.csv檔案
* Sync users from enterprise Active
Directory

### 4.管理員配置組織和授予用戶和組對環境的訪問權限

## 幫助和資源

* [First Time Login - Cloud Service](/help/journey-onboarding/sysadmin/learning-path-aem-users.md)
* [配置對AEMas a Cloud Service的訪問](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html?lang=en#accessing)
