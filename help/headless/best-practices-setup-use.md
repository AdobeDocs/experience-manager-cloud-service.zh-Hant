---
title: 搭配內容片段設定及使用AEM GraphQL的最佳做法
description: 瞭解設定及搭配內容片段使用AEM GraphQL的建議最佳實務。
exl-id: 4d6a5aaa-c8be-4858-ad07-085dc4fb77e7
feature: Headless
role: Admin, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 29%

---

# 搭配內容片段設定及使用AEM GraphQL的最佳做法{#best-practices-setup-use-aem-graphql-content-fragments}

這些指引總結了搭配GraphQL和內容片段設定、設定和使用AEM的建議最佳作法。

## 快速入門 {#getting-started}

協助您快速上手：

* [什麼是Headless？](/help/headless/what-is-headless.md)
* AEM [架構](/help/headless/deployment/architecture.md)中各種環境的概觀

## 設定 {#setup}

若要安全地設定AEM GraphQL以搭配內容片段和應用程式使用，您需要設定各種元件。

### GraphQL端點建立（包括安全性） {#graphql-endpoint-creation}

端點是用於存取 AEM GraphQL 的路徑。需要建立和發佈這些端點，才能安全地存取它們。

#### 詳細資料 {#details-graphql-endpoint-creation}

[在 AEM 中管理 GraphQL 端點](/help/headless/graphql-api/graphql-endpoint.md)

#### 環境 {#environments-graphql-endpoint-creation}

需要在以下位置設定端點：

* 作者
* 預覽
* 發佈

針對：

* 開發
* 測試
* 生產

### AEM Dispatcher快取 {#dispatcher-caching}

>[!NOTE]
>如果已啟用Dispatcher中的快取，則不需要[CORS設定](#cors-setup)，因此可以忽略。

根據預設，不啟用 Dispatcher 的持續性查詢快取。因為使用具有多個來源的 CORS (跨來源資源共用) 的客戶必須檢閱，且可能更新其 Dispatcher 設定，因此無法預設啟用。

#### 詳細資料 {#details-dispatcher-caching}

[GraphQL 持續性查詢 - 在 Dispatcher 中啟用快取](/help/headless/deployment/dispatcher-caching.md)

#### 環境 {#environments-dispatcher-caching}

Dispatcher通常設定用於：

* Publish：生產

### CORS設定 {#cors-setup}

>[!NOTE]
>如果[AEM Dispatcher](#dispatcher-caching)中的快取已啟用，則不需要CORS設定，因此可忽略此區段。

若要存取GraphQL端點，必須設定CORS原則，並新增至透過Cloud Manager部署至AEM的AEM專案。 這可透過為所需端點新增適當的OSGi CORS設定檔案來完成。

#### 詳細資料 {#details-cors-setup}

[跨原始資源共用 (CORS) 設定。](/help/headless/deployment/cross-origin-resource-sharing.md)

#### 環境 {#environments-cors-setup}

CORS通常設定為：

* Publish：生產

### 驗證 {#authentication}

用於內容片段傳送的Adobe Experience Manager as a Cloud Service (AEM) GraphQL API的主要使用案例是接受來自協力廠商應用程式或服務的遠端查詢。 這些遠端查詢可能需要經驗證的 API 存取權，以確保 Headless 內容傳遞的安全。

#### 詳細資料 {#details-authentication}

[針對內容片段之遠端 AEM GraphQL 查詢的驗證](/help/headless/security/authentication.md)

#### 環境 {#environments-authentication}

驗證通常設定為：

* 預覽
* 發佈

針對：

* 開發
* 測試
* 生產

### 權限 {#permissions}

進行 Headless 實作時，應該處理幾個安全和權限方面的問題。權限和角色可以根據 AEM 環境：**作者**&#x200B;或&#x200B;**發佈**&#x200B;進行廣泛的考量。每個環境都包含不同的角色和不同的需求。

#### 詳細資料 {#details-permissions}

[Headless 內容的權限考量事項](/help/headless/security/permissions.md)

#### 環境 {#environments-permissions}

許可權通常設定為：

* 作者
* 預覽
* 發佈

針對：

* 開發
* 測試
* 生產

### 使用內容傳遞網路(CDN) {#cdn}

使用CDN時，如果目標為`GET`請求，則可快取GraphQL查詢及其JSON回應。 相反地，未快取的請求可能非常（資源）昂貴且處理緩慢，可能對來源的資源造成進一步的負面影響。

#### 詳細資料 {#details-cdn}

[AEM as a Cloud Service 中的 CDN](/help/implementing/dispatcher/cdn.md)

#### 環境 {#environments-cdn}

CDN通常設定為：

* Publish：生產

### 設定和建立內容片段 {#cconfigure-create-content-fragments}

AEM GraphQL是用來從您的內容片段中擷取資訊。 必須先設定這些專案，然後定義結構和位置，您才能建立內容。

#### 詳細資料 {#details-content-fragments}

* [建立設定](/help/headless/setup/create-configuration.md)
* [建立內容片段模型](/help/headless/setup/create-content-model.md)
* [建立Assets資料夾](/help/headless/setup/create-assets-folder.md)
* [建立和編輯您的內容片段](/help/headless/setup/create-content-fragment.md)

#### 環境 {#eenvironments-content-fragments}

在以下位置定義、編寫、測試、發佈和存取內容片段：

* 作者
* 預覽
* 發佈

針對：

* 開發
* 測試
* 生產

## 使用AEM GraphQL {#use-aem-graphql}

### 最佳化GraphQL查詢 {#optimize-graphql-queries}

提供這些准則是為了協助防止您的GraphQL查詢出現效能問題。

#### 詳細資料 {#details-optimize-graphql-queries}

[最佳化 GraphQL 查詢](/help/headless/graphql-api/graphql-optimization.md)

>[!NOTE]
>
>最佳化准則涵蓋快取組態，已包含在[設定](#setup)中。

### 從您的應用程式存取GraphQL {#access-graphql-from-your-apps}

AEM Headless CMS讓開發人員可以自由使用他們熟悉的語言、架構和工具，建置並提供卓越的體驗。

#### 詳細資料 {#details-your-apps}

* [安裝及使用用於開發的AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/aem-headless-sdk.html)
* [AEM Headless開發人員資源](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hant)
* 範例，包括[React](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/react-app.html)、[Next.js](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/next-js.html)、[Node.js](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/server-to-server-app.html)等

#### 環境 {#environments-your-apps}

應用程式通常會開發、測試及用於：

* 預覽
* 發佈

針對：

* 開發
* 測試
* 生產

### 其他資源

如需AEM GraphQL和內容片段的詳細資訊，請參閱下列內容：

* [與內容片段搭配使用的 AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
* [使用 GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md)
* [AEM Headless開發人員資源](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hant)
