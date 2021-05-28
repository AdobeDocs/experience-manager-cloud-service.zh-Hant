---
title: 商務整合架構(CIF)附加元件的重大變更
description: 與舊版CIF相比，Commerce Integration Framework(CIF)有顯著變更。
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32,c136763f-56aa-450e-8796-bc84bf6c205d
source-git-commit: ac64ca485391d843c0ebefcf86e80b4015b72b2f
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 1%

---

# 商務整合架構(CIF)附加元件的重大變更{#notable-changes}

Adobe Experience Manager as aCloud Service提供許多新功能，並帶來許多管理AEM專案的可能性。 若要進一步了解這些功能，請依照[變更連結，將Experience Manager作為Cloud Service](/help/release-notes/aem-cloud-changes.md)。

本檔案著重說明Commerce Integration Framework(CIF)附加元件與舊版CIF之間的重要差異，主要稱為CIF Classic(Quickstart)和CIF開放原始碼。

## 安裝和更新

AEM CIF附加元件會透過Cloud Manager安裝。 安裝需要CIF卡，但可安裝CIF卡而無卡的沙箱除外。 憑借AEM合約中的CIF附加元件，自動收到積分。

該附加元件會隨著一般AEM的更新而自動更新，作為Cloud Service更新的一部分。

**舊版CIF**

* CIF Classic:無需安裝，CIF是快速入門的一部分。 CIF更新是一般AEM或Service Pack更新的一部分
* AEM內部部署的CIF開放原始碼：透過GitHub進行安裝。 更新是手動更新/維護工作的一部分。
* AEM Adobe Managed Services的CIF開放原始碼：透過Customer Success Manager進行安裝。 更新是手動更新/維護工作的一部分。

## 端點配置

端點會透過Cloud Manager UI或其CLI進行設定和更新。

**舊版CIF**

* CIF Classic:在AEM中透過OSGi設定
* CIF開放原始碼：透過CIF組態瀏覽器

## CIF Venia項目部署

在[Cloud Manager Git存放庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html)中可用的專案，並透過[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html)完成部署

**舊版CIF**

* CIF Classic:透過AEM套件安裝
* CIF開放原始碼：透過[Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=zh-Hant)

## 產品目錄資料

透過對支援所需GraphQL API的外部端點的即時呼叫，隨選要求產品目錄資料。 這些API支援在任何指定日期存取即時或暫存資料。 無需複製。

**舊版CIF**

* CIF Classic:即時和分段產品資料會透過完整或增量產品匯入，匯入並保存在AEM Author的JCR中。 即時產品資料會複製至AEM Publish。

## 透過AEM轉譯提供產品目錄體驗

AEM會使用指派給產品和類別的AEM目錄範本，即時轉譯產品目錄體驗。 無需複製。

**舊版CIF**

* CIF Classic:AEM作者會使用目錄Blueprint工具，為每個類別/產品建立AEM頁面。 這些頁面會復寫至AEM Publish。

>[!NOTE]
>
>如需如何將CIF與AEM Managed Service或AEM內部部署搭配使用的其他檔案，請參閱[商務整合架構](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
