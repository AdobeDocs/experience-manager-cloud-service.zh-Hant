---
title: 商務整合框架(CIF)附加元件的顯著變更
description: 與舊版CIF相比，商務整合架構(CIF)有顯著的改變。
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32,c136763f-56aa-450e-8796-bc84bf6c205d
translation-type: tm+mt
source-git-commit: 7a52e4b62f5a18f9c68e5afb0d464bd11be732d2
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 5%

---

# 商務整合框架(CIF)附加元件的顯著變更{#notable-changes}

Adobe Experience Manager是Cloud Service，為您的專案提供許多新功能與可AEM能。 若要進一步瞭解這些功能，請遵循[Experience Manager變更為Cloud Service](/help/release-notes/aem-cloud-changes.md)的連結。

本檔案著重說明商務整合框架(CIF)附加元件與舊版CIF之間的重要差異，主要稱為CIF Classic(Quickstart)和CIF開放原始碼。

## 安裝與更新

CIF附AEM加元件會透過Cloud Manager安裝。 安裝需要CIF信用額，但沙盒除外，CIF可以安裝，不需信用額。 信用額會透過合約中的CIF附加元件自動收到AEM。

附加元件會隨著定期更新而自動更AEM新，做為Cloud Service更新。

**舊版CIF**

* CIF Classic:無需安裝， CIF是快速入門計畫的一部分。 CIF更新是定期或Service Pack更AEM新的一部分
* CIF內部開AEM放源：透過GitHub進行安裝。 更新是手動更新／維護工作的一部分。
* CIF Open-source for AEM Adobe Managed Services:透過Customer Success Manager進行安裝。 更新是手動更新／維護工作的一部分。

## 端點配置

端點會透過Cloud Manager UI或其CLI進行設定和更新。

**舊版CIF**

* CIF Classic:透過OSGi組態，於AEM
* CIF開放原始碼：透過CIF組態瀏覽器

## CIF Venia項目的部署

[Cloud Manager Git儲存庫中提供的項目，並通過[Cloud Manager](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/deploying/overview.html)完成部署](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html)

**舊版CIF**

* CIF Classic:透過套件AEM安裝
* CIF開放原始碼：透過[Cloud Manager](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)

## 產品目錄資料

透過即時呼叫支援所需GraphQL API的外部端點，隨選取得產品目錄資料。 這些API支援在任何指定日期存取即時或分段資料。 無需複製。

**舊版CIF**

* CIF Classic:即時和分段產品資料會透過完整或增量產品匯入，匯入並持續存留在AEM Author的JCR中。 即時產品資料會複製至AEM Publish。

## 產品型錄體驗與轉AEM譯

使AEM用已指派給產品和類別的AEM目錄範本即時轉換產品目錄體驗。 無需複製。

**舊版CIF**

* CIF Classic:AEM Author使用目AEM錄藍圖工具為每個類別／產品建立頁面。 這些頁面會複製至AEM Publish。

>[!NOTE]
>
>有關如何搭配受管服務或內部部署使AEM用CIF的其AEM他文檔，請參閱[商務整合架構](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
