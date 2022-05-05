---
title: 預配過程 — 概述
description: 預配過程 — 概述
source-git-commit: ffeda76f9c661117ddba50588ebea01d151ee8c3
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 7%

---


# AEMas a Cloud Service:登機和訪問

此頁列出有關Experience Manageras a Cloud Service的預配過程的自助資源。

## AEMas a Cloud Service設定過程概述

本節提供下列主題的重要文章：

* 訪問AEMas a Cloud Service
* Adobe Experience Manager as a Cloud Service登機和配置過程
* 幫助和資源


### 訪問AEMas a Cloud Service

自動資源調配完成後：

* 授予的訪問權 — Adobe將在AdobeIdentity Management系統(IMS)內建立一個組織
* 預設情況下，指定管理員將擁有管理員權限
* 管理員可以通過Admin Console為其他團隊成員添加用戶和角色
* 查看用戶基於角色的權限，以確定雲管理器中的權限分配

![procesoverview.jpg](assets/processOverview.jpg)


有關詳細資訊，請訪問 [Experience Manageras a Cloud ServiceExperience League](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/home.html?lang=en)

### 資源和連結

* [AEM as a Cloud Service 的 IMS 支援](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en)
* [雲管理器中基於角色的權限](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/role-based-permissions.html?lang=en#what-is-required)
* [存取 Experience Manager as a Cloud Service ](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html?lang=en#getting-access)


## Adobe Experience Manager as a Cloud Service登陸進程

### 1。採購訂單觸發器自動預配。

### 2.板載組織到Adobe Admin Console:

![procesoverview2.jpg](assets/processOverview2.jpg)

* 系統管理員：
   * 設定AEM計畫和環境。
   * 導航至管理任務的Admin Console。
   * 聲明域以確認各域的所有權
   * 設定用戶目錄。
   * IDP配置。
* AEM 管理員:
   * 管理本地組、權限和權限。

### 3.板載用戶和管理訪問Admin Console:

![procesoverview3.jpg](assets/processOverview3.jpg)

板載用戶的三種方法（取決於大小和首選項）:
* 在Admin Console中手動建立用戶
* 上載.csv檔案
* 從企業Active Directory同步用戶

### 4.管理員配置組織和授予用戶和組對環境的訪問權限

## 幫助和資源

* [首次登錄 — Cloud Service](/help/journey-onboarding/sysadmin/learning-path-aem-users.md)
* [配置對AEMas a Cloud Service的訪問](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/accessing/overview.html?lang=en#accessing)
