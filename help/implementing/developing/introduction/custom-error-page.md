---
title: 自訂錯誤頁面
description: AEM隨附標準錯誤處理常式，可自訂處理HTTP錯誤。
exl-id: b74c65d1-8ef5-4ad4-8255-8187f3b1d84c
source-git-commit: ab68c03b29f3d2179b33c61a6d853d80ccb17615
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 2%

---

# 自訂錯誤頁面 {#customizing-error-pages}

AEM隨附處理HTTP錯誤的標準錯誤處理常式；例如，透過顯示：

![標準錯誤訊息](assets/error-message-standard.png)

為了回應錯誤，AEM提供 `404.jsp` 指令碼 `/libs/sling/servlet/errorhandler`.

>[!TIP]
>
>由於AEM以Apache Sling為基礎，因此可取得詳細資訊 [在Apache錯誤處理檔案中。](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html)

>[!NOTE]
>
>在作者例項上， [CQ WCM除錯篩選器](/help/implementing/deploying/configuring-osgi.md) 預設為啟用。 這一律會導致回應代碼200。 預設錯誤處理程式通過將完整堆棧跟蹤寫入響應來響應。
>
>在發佈例項上，CQ WCM除錯篩選器為 **always** 已停用（即使已設為啟用）。

## 如何自訂由錯誤處理常式顯示的頁面 {#how-to-customize-pages-shown-by-the-error-handler}

您可以開發自己的指令碼，以在發生錯誤時自訂錯誤處理常式顯示的頁面。 要執行此操作，您將運用 [AEM標準覆蓋機制](/help/implementing/developing/introduction/overlays.md) 以便您的自訂頁面建立於 `/apps` 並覆蓋位於 `/libs`.

1. 在存放庫中，複製預設指令碼：

   * 從 `/libs/sling/servlet/errorhandler/`
   * 至 `/apps/sling/servlet/errorhandler/`

   依預設，目的地路徑不存在，因此您首次執行此作業時需要建立它。

1. 導覽至 `/apps/sling/servlet/errorhandler`。您可以在此處：

   * 編輯適當的現有指令碼以提供所需資訊。 或
   * 建立和編輯所需代碼的新指令碼。

1. 儲存變更並測試。

>[!CAUTION]
>
>此 `404.jsp` 指令碼經過專門設計，以配合AEM驗證；尤其是，允許在發生這些錯誤時進行系統登入。
>
>因此，替換此指令碼應該非常謹慎。

### 自訂對HTTP 500錯誤的回應 {#customizing-the-response-to-http-errors}

HTTP [500內部伺服器錯誤](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) 表示伺服器端錯誤，例如伺服器遇到非預期的條件，使其無法履行要求。

當請求處理導致例外狀況時，Apache Sling架構(AEM建置於上):

* 記錄例外狀況
* 並在回應內文中傳回：
   * HTTP回應代碼500
   * 異常堆棧跟蹤

依據 [自訂錯誤處理常式顯示的頁面](#how-to-customize-pages-shown-by-the-error-handler) a `500.jsp` 可建立指令碼。 不過，只有在 `HttpServletResponse.sendError(500)` 會明確執行；例如從例外捕手那裡。

否則，回應代碼會設為500，但 `500.jsp` 指令碼未執行。

要處理500錯誤，錯誤處理程式指令碼的檔案名必須與異常類（或超類）相同。 要處理所有此類例外，可以建立指令碼 `/apps/sling/servlet/errorhandler/Throwable.jsp` 或 `/apps/sling/servlet/errorhandler/Exception.jsp`.

>[!NOTE]
>
>在AEM中，當從後端收到5XX錯誤時，CDN會提供一般錯誤頁面。 若要允許後端的實際回應傳遞，您必須將下列標題新增至回應： `x-aem-error-pass: true`.
>這僅適用於來自AEM或Apache/Dispatcher層的回應。 來自中間基礎架構層的其他意外錯誤仍會顯示一般錯誤頁面。

>[!CAUTION]
>
>在作者例項上， [CQ WCM除錯篩選器](/help/implementing/deploying/configuring-osgi.md) 預設為啟用。 這一律會導致回應代碼200。 預設錯誤處理程式通過將完整堆棧跟蹤寫入響應來響應。
>
>若為自訂錯誤處理常式，則需要程式碼為500的回應，因此 [必須停用CQ WCM除錯篩選器。](/help/implementing/deploying/configuring-osgi.md) 這可確保傳回回應代碼500，進而觸發正確的Sling錯誤處理常式。
>
>在發佈例項上，CQ WCM除錯篩選器為 **always** 已停用（即使已設為啟用）。
