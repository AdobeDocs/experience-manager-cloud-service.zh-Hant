---
title: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本注意事項。'
description: ' [!DNL Adobe Experience Manager]  as a Cloud Service 的目前維護版本注意事項。'
source-git-commit: 4aa4954f214545dcd768fdf955f1fc2f776da939
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 82%

---


# 維護版本注意事項 {#maintenance-release-notes}

下節是 Experience Manager as a Cloud Service 目前維護版本的技術版本注意事項。

## 11835 版 {#release-11835}

以下摘要為2023年4月19日公開發行之維護版本11835的持續改善。 此維護版本是針對先前 11382 維護版本的更新。

此維護版本的功能啟用將為您提供完整的功能集。 如需完整詳情，請參閱[最新版本注意事項](/help/release-notes/release-notes-cloud/release-notes-current.md)。

### 已修正的問題 {#fixed-issues-11835}

- SITES-12573 - 如果有一個變數未指定，在篩選條件中使用變數的 GraphQL 查詢將會失敗。如果您搭配 AEM as a Cloud Service 使用 GraphQL，請勿更新到這個版本。
- SKYOPS-51970 - 識別出 buildImage 步驟所使用之 FACT 版本的迴歸，導致使用者對應不相符。
- GRANITE-44542 - 已針對部分客戶回報問題，這些客戶沒有為內含在套件篩選器中的資料夾指定套件 nodetype (透過提供具有 jcr:primaryType 的 .content.xml 指定)。這會讓這些資料夾被視為 nt:folder，在多種情況下會產生問題。
- SKYOPS-56928 - Apache HTTPD回歸可能造成404錯誤。 如果您遇到這些問題，基於安全原因，建議您回復至舊版，並避免在該時段期間執行任何管道。

### 嵌入式技術 {#embedded-tech-11835}

| 科技 | 版本 | 連結 |
|---|---|---|
| AEM OAK | 1.44-T20221206170501-6d59064 | [Oak API 1.44.0 API](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.44.0/index.html) |
| AEM SLING API | 2.27.0 版 | [Apache Sling API 2.27.0 API](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTL | 1.4.20-1.4.0 版本 | [HTML 範本語言規格](https://github.com/adobe/htl-spec) |
| AEM 核心元件 | 2.21.2 版 | [AEM WCM 核心元件](https://github.com/adobe/aem-core-wcm-components) |
