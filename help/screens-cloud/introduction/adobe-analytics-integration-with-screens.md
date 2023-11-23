---
title: Adobe Analytics與AEM Screens整合
seo-title: Adobe Analytics Integration with AEM Screens
description: 請詳閱本頁，瞭解開箱即用的AEM Screens與Adobe Analytics整合，並為您提供播放證明。
seo-description: Follow this page to learn about out of the box integration of AEM Screens with Adobe Analytics and provides you with a proof of play.
uuid: 80d61af7-bf4d-46ca-a026-99a666c2e1a0
contentOwner: trushton
content-type: reference
products: SG_EXPERIENCEMANAGER/Cloud/SCREENS
topic-tags: administering
discoiquuid: b1a0e00e-0368-42c9-8bcd-5f00b4d0990c
docset: aem65
role: Admin, Developer
level: Intermediate
source-git-commit: bf0a841a5cd5eb278fd3d59484c84d1cee172b4e
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# Adobe Analytics與AEM Screens整合 {#adobe-analytics-integration-with-aem-screens}

本節涵蓋下列主題：

* **概觀**
* **架構詳細資料**

## 概觀 {#overview}

***AEM Screens*** 運用Adobe Analytics，您可以透過跨管道分析（可協助將位置中顯示的內容與其他資料來源建立關聯）這項市場獨特功能。

AEM Screens提供與Adobe Analytics的現成整合，並為您提供播放證明。

本節說明以下與Adobe Analytics連線AEM Screens專案相關的功能：

* 允許依裝置提供播放報表的證明
* 允許依資產播放報告的證明
* 確保擷取所有播放器事件並加上時間戳記
* 如果播放未連線至網路，請確定所有播放器事件都儲存在本機
* 允許建立回饋迴路，以追蹤一段時間內的播放事件
* 允許系統根據內容作者定義的成功標準修改內容和版面

因此，Adobe Analytics與AEM Screens的整合會強制進行下列作業 *目標*：

* 實現數位招牌實作的投資報酬率
* 整合Analytics，作為日後啟用收集和分析使用資訊的基礎

## 架構詳細資料 {#architectural-details}

AEM Screens客戶想要瞭解內容在何時顯示，以及顯示時間（彙總）。 這是招牌解決方案的常見功能。 AEM Screens不會建置我們自己的分析，而是會利用Adobe Analytics，透過它，我們可以在市場上實現一些獨一無二的東西 — 跨管道分析，有助於將位置中顯示的內容與其他資料來源建立關聯。

下列架構圖表說明Adobe Analytics與AEM Screens的整合：

![與Adobe Analytics整合](/help/screens-cloud/assets/analytics-architecture.png)

## 在AEM Screens雲端中啟用Adobe Analytics {#enabling-adobe-analytics-in-aem-screens-cloud}

請聯絡您的Adobe關係管理員，以在Screens Cloud中啟用Adobe分析。

## Screens Analytics：啟用流程 {#screens-analytics-enablement-flow}

>[!CAUTION]
>
>在您設定屬性之前，請聯絡您的Adobe關係管理員以建立票證以取得 **Analytics API金鑰** 和 **分析專案** 與AEM Screens搭配使用。

## 在AEM Screens中使用Adobe Analytics服務 {#using-adobe-analytics-service-in-aem-screens}

此情境會透過韌體和Instrument Screens核心元件中分析服務的REST呼叫叫用Analytics API，以明確建立和傳送特定使用案例的特定事件，同時允許擴充功能，讓任何自訂訊息可從自訂開發頻道傳送到Analytics。

Analytics事件會離線儲存在indexedDB中，並在稍後加入區塊並傳送至雲端。
