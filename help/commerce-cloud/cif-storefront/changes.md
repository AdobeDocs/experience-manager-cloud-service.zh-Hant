---
title: Commerce integration framework (CIF)附加元件重大變更
description: 與舊版Commerce integration framework (CIF)相比，CIF有重大變更。
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
feature: Commerce Integration Framework
role: Admin
source-git-commit: 856442039fcd25ec675a6258d182f7a35f590c3c
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---


# Commerce integration framework (CIF)附加元件的重大變更 {#notable-changes}

Adobe Experience Manager as a Cloud Service提供許多管理AEM專案的新功能，並帶來許多可能性。 若要進一步瞭解這些功能，請依照連結操作[Experience Manager as a Cloud Service的變更。](/help/release-notes/aem-cloud-changes.md)

本檔案著重說明Commerce integration framework (CIF)附加元件與舊版CIF (稱為CIF Classic (Quickstart)和CIF開放原始碼)之間的重要差異。

## 安裝與更新

AEM CIF附加元件是透過Cloud Manager安裝。 安裝需要CIF點數，但沙箱除外，因為沙箱中可安裝CIF而不需要點數。 系統會透過在您的AEM合約中布建CIF附加元件來自動接收學分。

此附加元件會隨著定期的AEM as a Cloud Service更新而自動更新。

### 舊版CIF {#previous-versions-installation}

* CIF Classic：不需要安裝，CIF是快速入門的一部分。 CIF更新是定期AEM或Service Pack更新的一部分
* 適用於AEM內部部署的CIF開放原始碼：透過GitHub安裝。 更新是手動更新/維護工作的一部分。
* 適用於CIF的AEM開放原始碼Adobe Managed Services：透過Adobe客戶團隊安裝。 更新是手動更新/維護工作的一部分。

## 端點設定 {#endpoint-configuration}

端點會透過Cloud Manager UI或其CLI進行設定和更新。

### 舊版CIF {#previous-versions-endpoint}

* CIF Classic：透過AEM中的OSGi設定
* CIF開放原始碼：透過CIF設定瀏覽器

## 部署CIF Venia專案 {#venia-project}

[Cloud Manager Git存放庫](/help/implementing/cloud-manager/managing-code/integrating-with-git.md)中可用的專案，以及透過[Cloud Manager完成的部署。](/help/implementing/deploying/overview.md)

### 舊版CIF {#previous-versions-venia}

* CIF Classic：透過AEM套件安裝
* CIF開放原始碼：透過[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/introduction.html)

## 產品目錄資料 {#product-catalog-data}

透過對支援必要GraphQL API的外部端點的即時呼叫，可隨選要求產品目錄資料。 這些API支援在任何指定日期存取即時或分階段資料。 不需要復寫。

### 舊版CIF {#previous-versions-catalog}

* CIF Classic：透過完整或差異產品匯入，即時和階段產品資料會匯入並儲存在AEM Author上的JCR中。 即時產品資料會復寫到AEM Publish。

## AEM轉譯的產品目錄體驗 {#catalog-experiences}

AEM會使用已指派給產品和類別的AEM目錄範本，即時呈現產品目錄體驗。 不需要復寫。

### 舊版CIF {#previous-cif-versions}

* CIF Classic： AEM Author會使用目錄Blueprint工具，為每個類別/產品建立AEM頁面。 這些頁面會復寫到AEM Publish。

>[!NOTE]
>
>如需如何將CIF與AEM Managed Service或AEM內部部署搭配使用的其他檔案，請參閱[Commerce integration framework。](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
