---
title: 商業整合框架(CIF)附加項的顯著變化
description: 與舊的CIF版本相比，商業整合框架(CIF)發生了顯著變化。
exl-id: 5a526960-96a1-421e-9fb0-0825e7df8f32
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---

# 對商業整合框架(CIF)附加項的顯著更改{#notable-changes}

Adobe Experience Manager as a Cloud Service為管理您的項目帶來了許多新的功能和AEM可能性。 要瞭解有關這些功能的更多資訊，請點擊連結 [對Experience Manageras a Cloud Service的更改](/help/release-notes/aem-cloud-changes.md)。

本文檔重點介紹了Commerce Integration Framework(CIF)附加版和舊CIF版之間的重要區別，這些版本主要稱為CIF Classic(Quickstart)和CIF Open-source。

## 安裝和更新

CIF附AEM加程式通過雲管理器安裝。 安裝需要CIF信用，但沙箱除外，CIF可以安裝，而無信用。 通過您合同中的CIF附加項的預配自動收AEM到信用。

該載入項將作為常規as a Cloud Service更新的一部分自動AEM更新。

**以前的CIF版本**

* CIF經典：無需安裝， CIF是Quickstart的一部分。 CIF更新是常規或Service Pack更AEM新的一部分
* CIF本地開AEM源：通過GitHub進行安裝。 更新是手動更新/維護工作的一部分。
* 用於Adobe Managed Services的CIFAEM開源：通過Customer Success Manager進行安裝。 更新是手動更新/維護工作的一部分。

## 終結點配置

通過Cloud Manager UI或其CLI配置和更新終結點。

**以前的CIF版本**

* CIF經典：通過OSGi配AEM置
* CIF開源：通過CIF配置瀏覽器

## 部署CIF Venia項目

項目可用於 [Cloud Manager Git儲存庫](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) 部署通過 [雲管理器](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html)

**以前的CIF版本**

* CIF經典：通過包AEM安裝
* CIF開源：通過 [雲管理器](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html?lang=zh-Hant)

## 產品目錄資料

通過即時調用支援所需GraphQL API的外部終結點，產品目錄資料可按需獲得請求。 這些API支援在任何給定日期訪問即時或暫存資料。 不需要複製。

**以前的CIF版本**

* CIF經典：通過完整或增量產品導入，即時和分段產品資料將導入並保留在AEM Author上的JCR中。 將即時產品資料複製到AEM發佈。

## 產品目錄體驗與呈AEM現

使AEM用已分配給產品和類別的AEM目錄模板即時呈現產品目錄體驗。 不需要複製。

**以前的CIF版本**

* CIF經典：AEM作者使用目AEM錄藍圖工具為每個類別/產品建立一個頁面。 這些頁面被複製到AEM發佈。

>[!NOTE]
>
>有關如何將CIF與托管服務或本地AEM服務一起使用AEM的其他文檔，請參閱 [商務整合框架](https://www.adobe.io/apis/experiencecloud/commerce-integration-framework/getting-started.html)
