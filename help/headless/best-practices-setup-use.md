---
title: 設定和使用 AEM GraphQL 與內容片段的最佳做法
description: 了解有關設定和使用 AEM GraphQL 與內容片段的建議最佳做法。
exl-id: 4d6a5aaa-c8be-4858-ad07-085dc4fb77e7
feature: Headless
role: Admin, Developer
source-git-commit: 38a4bf89e099432163163e90e08aa0f47407724f
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 100%

---

# 設定和使用 AEM GraphQL 與內容片段的最佳做法{#best-practices-setup-use-aem-graphql-content-fragments}

這些指南總結了設定、設定 AEM，以及將 AEM 與 GraphQL 和內容片段搭配使用的建議最佳做法。

## 快速入門 {#getting-started}

為了幫助您快速上手：

* [什麼是 Headless？](/help/headless/what-is-headless.md)
* AEM [架構](/help/headless/deployment/architecture.md)中各種環境的概觀

## 設定 {#setup}

為了安全地設定 AEM GraphQL 以用於內容片段和您的應用程式，您需要設定各種元件。

### GraphQL 端點建立 (包括安全性) {#graphql-endpoint-creation}

端點是用於存取 AEM GraphQL 的路徑。需要建立和發佈這些端點，以便安全地存取它們。

#### 詳細資料 {#details-graphql-endpoint-creation}

[在 AEM 中管理 GraphQL 端點](/help/headless/graphql-api/graphql-endpoint.md)

#### 環境 {#environments-graphql-endpoint-creation}

端點需要設定為：

* 作者
* 預覽
* 發佈

用於：

* 開發
* 測試
* 生產

### AEM Dispatcher 快取 {#dispatcher-caching}

>[!NOTE]
>如果啟用了 Dispatcher 的快取，就不需要 [CORS 設定](#cors-setup)，因此可以忽略該部分。

根據預設，不啟用 Dispatcher 的持續性查詢快取。因為使用具有多個來源的 CORS (跨來源資源共用) 的客戶必須檢閱，且可能更新其 Dispatcher 設定，因此無法預設啟用。

#### 詳細資料 {#details-dispatcher-caching}

[GraphQL 持續性查詢 - 在 Dispatcher 中啟用快取](/help/headless/deployment/dispatcher-caching.md)

#### 環境 {#environments-dispatcher-caching}

Dispatcher 通常設定為：

* 發佈：生產

### CORS 設定 {#cors-setup}

>[!NOTE]
>如果啟用了 [AEM Dispatcher](#dispatcher-caching) 的快取，就不需要 CORS 設定，因此可以忽略該部分。

若要存取 GraphQL 端點，必須設定 CORS 原則並新增至透過 Cloud Manager 部署到 AEM 的 AEM 專案。做法是為所需端點新增適當的 OSGi CORS 設定。

#### 詳細資料 {#details-cors-setup}

[跨原始資源共用 (CORS) 設定。](/help/headless/deployment/cross-origin-resource-sharing.md)

#### 環境 {#environments-cors-setup}

CORS 通常設定為：

* 發佈：生產

### 驗證 {#authentication}

用於內容片段傳遞的 Adobe Experience Manager as a Cloud Service (AEM) GraphQL API 的主要使用案例是接受協力廠商應用程式或服務的遠端查詢。這些遠端查詢可能需要經驗證的 API 存取權，以確保 Headless 內容傳遞的安全。

#### 詳細資料 {#details-authentication}

[針對內容片段之遠端 AEM GraphQL 查詢的驗證](/help/headless/security/authentication.md)

#### 環境 {#environments-authentication}

驗證通常設定為：

* 預覽
* 發佈

用於：

* 開發
* 測試
* 生產

### 權限 {#permissions}

進行 Headless 實作時，應該處理幾個安全和權限方面的問題。權限和角色可以根據 AEM 環境：**作者**&#x200B;或&#x200B;**發佈**&#x200B;進行廣泛的考量。每個環境都包含不同的角色和不同的需求。

#### 詳細資料 {#details-permissions}

[Headless 內容的權限考量事項](/help/headless/security/permissions.md)

#### 環境 {#environments-permissions}

權限通常設定為：

* 作者
* 預覽
* 發佈

用於：

* 開發
* 測試
* 生產

### 使用內容傳遞網路 (CDN) {#cdn}

使用 CDN 時，如果作為目標 `GET` 要求，則可以快取 GraphQL 查詢及其 JSON 回應。相反地，未快取的要求可能非常昂貴 (資源) 且處理速度緩慢，並且可能對來源資源產生進一步的有害影響。

#### 詳細資料 {#details-cdn}

[AEM as a Cloud Service 中的 CDN](/help/implementing/dispatcher/cdn.md)

#### 環境 {#environments-cdn}

CDN 通常設定為：

* 發佈：生產

### 設定和建立內容片段 {#cconfigure-create-content-fragments}

AEM GraphQL 用於從您的內容片段中擷取資訊。需要先進行設定，定義結構和位置，然後才能建立內容。

#### 詳細資料 {#details-content-fragments}

* [建立設定](/help/headless/setup/create-configuration.md)
* [建立內容片段模型](/help/headless/setup/create-content-model.md)
* [建立資產資料夾](/help/headless/setup/create-assets-folder.md)
* [建立和編輯內容片段](/help/headless/setup/create-content-fragment.md)

#### 環境 {#eenvironments-content-fragments}

內容片段的定義、編輯、測試、發佈和存取：

* 作者
* 預覽
* 發佈

用於：

* 開發
* 測試
* 生產

## 使用 AEM GraphQL {#use-aem-graphql}

### 最佳化 GraphQL 查詢 {#optimize-graphql-queries}

提供這些指南是為了幫助防止 GraphQL 查詢出現效能問題。

#### 詳細資料 {#details-optimize-graphql-queries}

[最佳化 GraphQL 查詢](/help/headless/graphql-api/graphql-optimization.md)

>[!NOTE]
>
>最佳化指南涵蓋了快取設定，這部分已在[設定](#setup)中介紹。

### 從您的應用程式存取 GraphQL {#access-graphql-from-your-apps}

AEM 無頭 CMS 使開發者可以自由地使用他們已經熟悉的語言、框架和工具來建置和交付卓越的體驗。

#### 詳細資料 {#details-your-apps}

* [安裝並使用 AEM SDK 進行開發](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/aem-headless-sdk.html?lang=zh-Hant)
* [AEM Headless 開發人員資源](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hant)
* 範例包括 [React](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/react-app.html?lang=zh-Hant)、[Next.js](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/next-js.html?lang=zh-Hant)、[Node.js](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/how-to/example-apps/server-to-server-app.html?lang=zh-Hant) 等

#### 環境 {#environments-your-apps}

應用程式通常在以下環境中開發、測試和使用：

* 預覽
* 發佈

用於：

* 開發
* 測試
* 生產

### 其他資源

如需更多 AEM GraphQL 和內容片段的詳細資料，請參閱以下內容：

* [與內容片段搭配使用的 AEM GraphQL API](/help/headless/graphql-api/content-fragments.md)
* [使用 GraphiQL IDE](/help/headless/graphql-api/graphiql-ide.md)
* [AEM Headless 開發人員資源](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=zh-Hant)
