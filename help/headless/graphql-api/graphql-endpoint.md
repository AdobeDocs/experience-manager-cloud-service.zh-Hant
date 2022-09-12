---
title: 在AEM中管理GraphQL端點
description: 了解如何在Adobe Experience Manager as a Cloud Service中管理GraphQL端點，以提供無周邊的內容。
feature: Content Fragments,GraphQL API
exl-id: f7164ae3-4074-4db7-8c43-a79cc2ef00b1
source-git-commit: 6be7cc7678162c355c39bc3000716fdaf421884d
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 5%

---

# 在AEM中管理GraphQL端點 {#graphql-aem-endpoint}

端點是用來存取AEM適用的GraphQL的路徑。 使用此路徑，您（或您的應用程式）可以：

* 訪問GraphQL架構，
* 發送您的GraphQL查詢，
* 接收回應（對您的GraphQL查詢）。

AEM中有兩種端點類型：

* 全域
   * 可供所有網站使用。
   * 此端點可使用所有Sites設定中的所有內容片段模型(定義於 [配置瀏覽器](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser))。
   * 如果有任何內容片段模型應在Sites設定之間共用，則應在全域Sites設定下建立。
* 站點配置：
   * 與Sites設定對應，如 [配置瀏覽器](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser).
   * 特定於指定的站點/項目。
   * Sites設定的特定端點會使用該特定Sites設定的內容片段模型，以及全域Sites設定的內容片段模型。

>[!CAUTION]
>
>內容片段編輯器可允許一個網站設定的內容片段參考另一個網站設定的內容片段（透過政策）。
>
>在這種情況下，並非所有內容都可使用Sites配置特定的端點進行檢索。
>
>內容作者應控制此情境；例如，建議將共用內容片段模型置於全域網站設定下，這樣做可能會很實用。

GraphQL for AEM全域端點的存放庫路徑為：

`/content/cq:graphql/global/endpoint`

您的應用程式可在請求URL中使用下列路徑：

`/content/_cq_graphql/global/endpoint.json`

若要為AEM適用的GraphQL啟用端點，您需要：

* [啟用GraphQL端點](#enabling-graphql-endpoint)
* [發佈GraphQL端點](#publishing-graphql-endpoint)

## 啟用GraphQL端點 {#enabling-graphql-endpoint}

要啟用GraphQL端點，您首先需要有適當的配置。 請參閱 [內容片段 — 設定瀏覽器](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md).

>[!CAUTION]
>
>若 [尚未啟用內容片段模型的使用](/help/sites-cloud/administering/content-fragments/content-fragments-configuration-browser.md), **建立** 選項將無法使用。

要啟用相應的端點，請執行以下操作：

1. 導覽至 **工具**, **一般**，然後選取 **GraphQL**.
1. 選擇 **建立**。
1. 此 **建立新的GraphQL端點** 對話框將開啟。 您可以在此處指定：
   * **名稱**:端點名稱；您可以輸入任何文字。
   * **使用由提供的GraphQL架構**:使用下拉式清單來選取所需的網站/專案。

   >[!NOTE]
   >
   >對話方塊中會顯示下列警告：
   >
   >* *如果未妥善管理，GraphQL 端點可能會導致資料安全性和效能問題。在建立端點後，請務必設定適當的權限。*


1. 確認為 **建立**.
1. 此 **後續步驟** 對話框將提供指向安全控制台的直接連結，以便您能夠確保新建立的端點具有適當的權限。

   >[!CAUTION]
   >
   >端點可供所有人存取。 這可能會（尤其是在發佈執行個體上）帶來安全疑慮，因為GraphQL查詢可能會對伺服器造成沈重負載。
   >
   >您可以在端點上設定與您的使用案例相應的ACL。

## 發佈GraphQL端點 {#publishing-graphql-endpoint}

選取新端點，然後 **發佈** 讓它在所有環境中都能完全使用。

>[!CAUTION]
>
>端點可供所有人存取。
>
>在發佈執行個體上，這可能會造成安全疑慮，因為GraphQL查詢可能會對伺服器造成沈重負載。
>
>您必須設定 [適合您使用案例的ACL](/help/headless/security/permissions.md) 在端點上。
