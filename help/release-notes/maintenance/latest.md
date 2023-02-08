---
title: 的最新維護髮行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
description: 的最新維護髮行說明 [!DNL Adobe Experience Manager] as a Cloud Service。
source-git-commit: 76da86d31e2780c2d22419cb8a338cf37963fad8
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 5%

---


# 維護髮行說明 {#maintenance-release-notes}

以下章節概述Experience Manageras a Cloud Service最新維護版本的技術發行說明。

## 版本10912 {#release-10912}

以下摘要為2023年2月3日公開發行的維護版本10912的持續改善。 此維護版本是先前維護版本9850的更新。

本維護版本的啟用功能將提供完整的功能集。 請參閱 [最新發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md) 以取得完整詳細資訊。

### 已知問題 {#known-issues}

如果您使用CORS，請勿升級。 我們在此版本中發現影響GraphQL內容傳送部分的問題。 變更GraphQL持續查詢快取方式的預設AEM Dispatcher設定，可能會使用CORS設定中斷客戶持續查詢的GraphQL內容傳送。

### 內嵌技術 {#embedded-tech}

| 科技 | 版本 | 連結 |
|---|---|---|
| AEM WCM核心元件 | 2.21.2版 | [GitHub](https://github.com/adobe/aem-core-wcm-components) |
