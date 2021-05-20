---
title: 自訂錯誤頁面
description: AEM隨附標準錯誤處理常式，可自訂處理HTTP錯誤。
exl-id: b74c65d1-8ef5-4ad4-8255-8187f3b1d84c
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---

# 自定義錯誤頁{#customizing-error-pages}

AEM隨附處理HTTP錯誤的標準錯誤處理常式；例如，透過顯示：

![標準錯誤訊息](assets/error-message-standard.png)

為了回應錯誤，AEM在`/libs/sling/servlet/errorhandler`下提供`404.jsp`指令碼。

>[!TIP]
>
>由於AEM以Apache Sling為基礎，因此Apache錯誤處理檔案中[會提供詳細資訊。](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html)

>[!NOTE]
>
>在製作例項上，預設會啟用[CQ WCM除錯篩選器](/help/implementing/deploying/configuring-osgi.md)。 這一律會導致回應代碼200。 預設錯誤處理程式通過將完整堆棧跟蹤寫入響應來響應。
>
>在發佈執行個體上，CQ WCM除錯篩選器會一律停用&#x200B;****（即使已設為啟用）。

## 如何自訂錯誤處理常式{#how-to-customize-pages-shown-by-the-error-handler}顯示的頁面

您可以開發自己的指令碼，以在發生錯誤時自訂錯誤處理常式顯示的頁面。 若要這麼做，您將運用[AEM標準覆蓋機制](/help/implementing/developing/introduction/overlays.md)，讓您的自訂頁面在`/apps`下建立，並覆蓋`/libs`下的預設頁面。

1. 在存放庫中，複製預設指令碼：

   * 從 `/libs/sling/servlet/errorhandler/`
   * 至 `/apps/sling/servlet/errorhandler/`

   依預設，目的地路徑不存在，因此您首次執行此作業時需要建立它。

1. 導航到 `/apps/sling/servlet/errorhandler`. 您可以在此處：

   * 編輯適當的現有指令碼以提供所需資訊。 或
   * 建立和編輯所需代碼的新指令碼。

1. 儲存變更並測試。

>[!CAUTION]
>
>`404.jsp`指令碼經過專門設計，以應對AEM驗證；尤其是，允許在發生這些錯誤時進行系統登入。
>
>因此，替換此指令碼應該非常謹慎。

### 自訂HTTP 500錯誤的回應{#customizing-the-response-to-http-errors}

HTTP [500內部伺服器錯誤](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)表示伺服器端錯誤，例如伺服器遇到非預期的條件，使其無法履行請求。

當請求處理導致例外時，Apache Sling架構(內建AEM):

* 記錄例外狀況
* 並在回應內文中傳回：
   * HTTP回應代碼500
   * 異常堆棧跟蹤

通過[自定義由錯誤處理程式](#how-to-customize-pages-shown-by-the-error-handler)顯示的頁面，可以建立`500.jsp`指令碼。 但只有在明確執行`HttpServletResponse.sendError(500)`時，才會使用；例如從例外捕手那裡。

否則，回應代碼會設為500，但不會執行`500.jsp`指令碼。

要處理500錯誤，錯誤處理程式指令碼的檔案名必須與異常類（或超類）相同。 要處理所有此類異常，可以建立指令碼`/apps/sling/servlet/errorhandler/Throwable.jsp`或`/apps/sling/servlet/errorhandler/Exception.jsp`。

>[!CAUTION]
>
>在製作例項上，預設會啟用[CQ WCM除錯篩選器](/help/implementing/deploying/configuring-osgi.md)。 這一律會導致回應代碼200。 預設錯誤處理程式通過將完整堆棧跟蹤寫入響應來響應。
>
>若為自訂錯誤處理常式，則需要程式碼為500的回應，因此需要停用[CQ WCM除錯篩選器。](/help/implementing/deploying/configuring-osgi.md) 這可確保傳回回應代碼500，進而觸發正確的Sling錯誤處理常式。
>
>在發佈執行個體上，CQ WCM除錯篩選器會一律停用&#x200B;****（即使已設為啟用）。
