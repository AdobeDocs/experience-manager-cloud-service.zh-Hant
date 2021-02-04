---
title: RemotePage元件
description: RemotePage元件是自訂的頁面元件，用於編輯AEM中的遠端React SPA。
translation-type: tm+mt
source-git-commit: 6a88b93a4005b858eec222fd7ae15df9db269d31
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 1%

---

# RemotePage元件{#remote-page-component}

在決定您要在外部SPA和AEM之間使用何種整合等級[時，您通常需要能夠在AEM中檢視和編輯SPA。 ](/help/implementing/developing/headful-headless.md)RemotePage元件是專門用於此目的的自定義頁面元件。

## 概覽 {#overview}

RemotePage元件會從應用程式產生的`asset-manifest.json`擷取所有必要資產，並使用它來呈現AEM中的SPA。

## 要求{#requirements}

* 讓CORS可進行開發
* 在頁面屬性中設定遠端URL
* 在AEM中演算SPA

## 限制 {#limitations}

* RemotePage元件的當前實施僅支援遠程React應用程式。
* 在AEM中執行遠端演算時，應用程式的根HTML檔案中定義的內部CSS以及根DOM節點上的內嵌CSS將無法使用。

## 技術詳細資訊{#technical-details}

和AEM SPA專案的其他部分一樣，RemotePage元件也是開放原始碼。 有關RemotePage元件的完整技術詳細資訊，請參見GitHub儲存庫。](https://github.com/adobe/aem-spa-project-core/tree/master/ui.apps/src/main/content/jcr_root/apps/spa-project-core/components/remotepage)[
