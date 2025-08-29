---
title: 在Cloud Manager中將Edge Delivery Services與Adobe管理的CDN整合
description: null
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
hide: true
hidefromtoc: true
source-git-commit: 71ea3b810d4145d5581c29e26db9bc157c425a15
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---


# 在Cloud Manager中將Edge Delivery Services與Adobe管理的CDN整合 {#integrate-adbe-cdn-with-edservices-in-cm}

Adobe Managed CDN (AMC-D)與Edge Delivery Services原生整合，為您提供Adobe Experience Manager (AEM) Sites高效且分散於全球的體驗。

這些功能可共同為您提供下列優點：

* 由Adobe管理的一整套企業級CDN。
* 現代化的邊緣傳送層，可加速要求、最佳化快取，並保護使用者不受常見攻擊。
* 適用於網域管理、SSL憑證和管道導向部署的統一Cloud Manager工作流程。

<!--
Adobe's Edge Delivery Services (EDS) can take advantage of an Adobe managed CDN. EDS is a framework that optimizes website delivery for speed, simplicity, and scalability by pushing content closer to the user through edge nodes. It is not a replacement for a CDN, but rather a way to enhance content delivery, especially when you use the Adobe managed CDN. It offers you the following benefits:

* Adobe-Managed CDN: EDS can use an Adobe-managed CDN, offering features like self-service CDN management and automatic certificate renewal. 
* EDS and AEM: EDS is a feature of AEM as a Cloud Service and works alongside the AEM authoring environment. 
* Performance enhancement: EDS, in conjunction with an Adobe Managed CDN, improves website performance by caching content at edge locations closer to users, reducing latency. 
* Flexibility: EDS provides flexibility in content delivery, allowing your organization to choose between the Adobe-managed CDN or their own CDN setup, based on their needs and existing infrastructure. 
Self-Service CDN Management:
Adobe-managed CDN within EDS enables self-service configuration and management tasks like SSL certificate setup. 
 
Use Cases:
EDS with CDN integration is beneficial for various scenarios, including e-commerce storefronts and websites requiring high performance and scalability. -->

## Cloud Manager中Adobe Managed CDN的Edge Delivery Services部署選項 {#deployment-options}

本主題說明在Cloud Manager中以Adobe Managed CDN部署Edge Delivery Services的兩種方式，同樣重要的是，可協助您決定最適合使用案例的選項。

Edge Delivery Services可使用下列兩個選項之一進行設定。 各有不同功能。

|  | 部署選項 | 重要檔案 | 功能 | 最適合 |
| --- | --- | --- | --- | --- |
| 選項1 | *具有*&#x200B;現有的AEM as a Cloud Service (AEMaaCS)環境 | [從現有環境設定Proxy](https://www.aem.live/docs/byo-cdn-adobe-managed#option-1-setup-a-proxy-from-an-existing-environment) | 設定管道通常適用於AEMaaCS環境 | 已在Cloud Manager中執行Sites且想要快速且低風險的效能提升的團隊。 |
| 選項2 | *沒有*&#x200B;現有的AEMaaCS環境；稱為獨立的「Edge環境」。 | [在沒有現有環境的情況下設定Edge Delivery網站](https://www.aem.live/docs/byo-cdn-adobe-managed#option-2-setup-an-edge-delivery-site-without-an-existing-environment) | 設定管道目前只能透過有限的Beta計畫用於Edge環境。<br>請參閱[新增Edge Delivery設定管道](help/implementing/cloud-manager/release-notes/current.md##add-eds-pipeline)。 | 想要採用完整Edge Delivery架構和精細路由的新組建或移轉。 |

<!-- Ultimately this URL above will need to be updated on GA -->

| 選項 | 摘要 | 最適合 | 重要檔案 |
| --- | --- | --- | --- |
| Adobe Managed CDN Proxy | Adobe Managed CDN面對現有的AEM Sites環境。 您目前的Sites管道仍為「原點」，而AMC-D處理邊緣快取和TLS終止。 | 已在Cloud Manager中執行Sites且想要快速且低風險的效能提升的團隊。 | 設定AMC-D代理 |
| 使用originSelectors設定管線 | 專用的Edge Delivery設定管道會直接將靜態和動態內容發佈到邊緣。 `originSelectors`在AMC-D和您的AEM作者/發佈層級之間路由流量。 | 想要採用完整Edge Delivery架構和精細路由的新組建或移轉。 | 設定Edge Delivery管道 |

>[!TIP]
>
>不確定要選擇哪個路徑？ 請參閱下列[選擇部署模式](#choose-deployment-model)以取得決策准則。

## 選擇部署模型 {#choose-deployment-model}

這兩種模式可以在同一個Cloud Manager程式中並存，允許分階段移轉。

| 如果您…… | 然後使用…… |
| :--- | :--- |
| 需要快速且只需很少變更的推出，且已在Cloud Manager中代管網站 | AMC-D Proxy |
| 計畫重新建構Edge Delivery的內容，或想要在多個來源之間取得更細微的路由 | 設定Edge傳遞管道+ `originSelectors` |

## 先決條件 {#prerequisites}

1. 在Cloud Manager中布建您的網站 — 兩種部署模式都需要。 關注登入AEM網站。

2. 自備Git (BYOG) （選用） — 如果您將網站程式碼儲存在Adobe Git之外，請完成BYOG上線。

3. Edge Delivery授權 — 確保您的程式已獲得Edge Delivery Services的授權。


