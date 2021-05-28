---
title: 規劃階段
description: 規劃階段
exl-id: 987cb929-7871-4fec-8ef5-4d2f5f2f2186
source-git-commit: 856266faf4cb99056b1763383d611e9b2c3c13ea
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 88%

---

# 規劃 {#planning-phase}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_planning"
>title="規劃您的轉變"
>abstract="在展開轉換至 Cloud Service 的過程前，您應該先熟悉 AEM as a Cloud Service、檢視針對其採取的重大變更，並檢視已遭取代或淘汰的功能。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/overview-best-practices-analyzer.html" text="Best Practices Analyzer"

在展開轉換至 Cloud Service 的過程前，您應該先熟悉 AEM as a Cloud Service、檢視針對其採取的重大變更，並檢視已遭取代或淘汰的功能。

## 重大變更 {#notable-changes}

AEM as a Cloud Service 提供許多管理 AEM 專案的新功能，並帶來許多可能性。

但 AEM as a Cloud Service 與 AEM On-premise 或 Adobe Managed Services 之間仍有許多差異。

請參考 [AEM 雲端服務的重大變更](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/aem-cloud-changes.html)以了解重要差異。

## 過時的功能 {#deprecated-features}

Adobe 持續評估產品功能，以更新或替代的方式來改善或取代舊功能，以提升客戶享有的整體價值，且隨時謹慎考慮是否回溯相容。

請參考[過時的功能](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/release-notes/deprecated-removed-features.html#deprecated-features)，深入了解已在 Experience Manager as a Cloud Service 中標示為過時的功能。

## 了解規劃階段 {#introduction}

下圖將展示「規劃」階段中的關鍵步驟：

![影像](/help/move-to-cloud-service/assets/planning-phaseimg1.png)

### 評定雲端服務整備 {#access-cloud-readiness}

「規劃」階段中的第一個步驟，便是評定您是否已整備完畢，可從現有的 AEM 版本移轉至 Cloud Service；接著，也要判斷必須重構以便與 AEM as a Cloud Service 相容的區域。

您必須對照重大變更和過時的功能，對目前的 AEM 原始碼進行綜合評估，以便判斷轉換過程中預期的投入程度。

您可以在目前的AEM版本上執行Best Practices Analyzer，以加速評估步驟。 有關更多詳細資訊，請參閱[Best Practices Analyzer](/help/move-to-cloud-service/best-practices-analyzer/overview-best-practices-analyzer.md)。

>[!NOTE]
>如果您已經能存取 Cloud Manager 和雲端服務環境，建議您在 Cloud Manager 品質管線中執行目前的程式碼，評估需針對原始碼採取哪些變更，以便與雲端服務相容。

### 檢視資源規劃 {#review-resource-planning}

一旦評估好移轉至雲端服務所需的投入程度，您便應該確定資源、建立團隊，並安排轉換程序中的角色和責任。

### 建立 KPI {#establish-kpis}

如果您先前尚未建立關鍵績效指標 (KPI)，我們建議您為 Adobe Experience Manager (AEM) 實作建立 KPI，協助您的團隊專注於最重要的事項。

請參考[開發 KPI](https://guided.adobe.com/welcome/aem/part6.html)，了解如何為您的企業目標選擇正確的 KPI。
