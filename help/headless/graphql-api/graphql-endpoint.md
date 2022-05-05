---
title: 管理GraphQL端點AEM
description: 瞭解如何管理Adobe Experience Manager as a Cloud Service的GraphQL終端節點，以便無頭內容交付。
feature: Content Fragments,GraphQL API
exl-id: f7164ae3-4074-4db7-8c43-a79cc2ef00b1
source-git-commit: a4f3e55bb3bc39575d43894b9fea1180eaf1a578
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 5%

---

# 管理GraphQL端點AEM {#graphql-aem-endpoint}

端點是用於訪問GraphQL的路AEM徑。 使用此路徑，您（或您的應用）可以：

* 訪問GraphQL架構，
* 發送GraphQL查詢，
* 接收響應（對GraphQL查詢）。

中有兩種端點類型AEM:

* 全域
   * 可供所有站點使用。
   * 此終結點可以使用所有站點配置(在 [配置瀏覽器](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser))。
   * 如果站點配置之間應共用任何內容片段模型，則應在全局站點配置下建立這些模型。
* 站點配置：
   * 對應於在 [配置瀏覽器](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)。
   * 特定於指定的站點/項目。
   * 特定站點配置的終結點將使用來自該特定站點配置的內容片段模型以及來自全局站點配置的內容片段模型。

>[!CAUTION]
>
>內容片段編輯器允許一個站點配置的內容片段引用另一個站點配置的內容片段（通過策略）。
>
>在這種情況下，並非所有內容都可以使用特定於站點配置的終結點進行檢索。
>
>內容作者應控制此情景；例如，考慮將共用內容片段模型置於「全局站點」配置下可能很有用。

全局終結點的GraphQL的AEM儲存庫路徑是：

`/content/cq:graphql/global/endpoint`

您的應用可以在請求URL中使用以下路徑：

`/content/_cq_graphql/global/endpoint.json`

要為GraphQL啟用終結點，AEM您需要：

* [啟用GraphQL終結點](#enabling-graphql-endpoint)
* [發佈GraphQL終結點](#publishing-graphql-endpoint)

## 啟用GraphQL終結點 {#enabling-graphql-endpoint}

要啟用GraphQL終結點，您首先需要具有適當的配置。 請參閱 [內容片段 — 配置瀏覽器](/help/assets/content-fragments/content-fragments-configuration-browser.md)。

>[!CAUTION]
>
>如果 [未啟用內容片段模型的使用](/help/assets/content-fragments/content-fragments-configuration-browser.md)，也請參見Wiki頁。 **建立** 選項。

要啟用相應端點，請執行以下操作：

1. 導航到 **工具**。 **常規**，然後選擇 **圖形QL**。
1. 選擇 **建立**。
1. 的 **建立新GraphQL終結點** 對話框。 您可以在此處指定：
   * **名稱**:端點名稱；可以輸入任何文本。
   * **使用由提供的GraphQL架構**:使用下拉清單選擇所需的站點/項目。

   >[!NOTE]
   >
   >對話框中顯示以下警告：
   >
   >* *如果未妥善管理，GraphQL 端點可能會導致資料安全性和效能問題。在建立端點後，請務必設定適當的權限。*


1. 確認 **建立**。
1. 的 **後續步驟** 對話框將提供到安全控制台的直接連結，以便您能夠確保新建立的終結點具有適當的權限。

   >[!CAUTION]
   >
   >每個人都可以訪問該終結點。 這可能會引起安全問題，因為GraphQL查詢會給伺服器帶來沈重負載。
   >
   >您可以在端點上設定與您的使用案例相適應的ACL。

## 發佈GraphQL終結點 {#publishing-graphql-endpoint}

選擇新端點並 **發佈** 使其在所有環境中都完全可用。

>[!CAUTION]
>
>每個人都可以訪問該終結點。
>
>在發佈實例時，這可能會引起安全問題，因為GraphQL查詢會給伺服器帶來沈重負載。
>
>必須設定 [適合您使用案例的ACL](/help/headless/security/permissions.md) 在端點上。
