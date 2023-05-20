---
title: 自訂錯誤頁面
description: 帶AEM有標準錯誤處理程式，用於處理HTTP錯誤，可以自定義。
exl-id: b74c65d1-8ef5-4ad4-8255-8187f3b1d84c
source-git-commit: b20d40a9f5f4bda51c67cda1164d0c4d74943aa1
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 2%

---

# 自定義錯誤頁 {#customizing-error-pages}

帶AEM有處理HTTP錯誤的標準錯誤處理程式；例如，通過顯示：

![標準錯誤消息](assets/error-message-standard.png)

要響應錯誤，AEM請提供 `404.jsp` 指令碼 `/libs/sling/servlet/errorhandler`。

>[!TIP]
>
>因AEM為基於Apache Sling，有更多資訊 [中。](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html)

>[!NOTE]
>
>在作者案中， [CQ WCM調試篩選器](/help/implementing/deploying/configuring-osgi.md) 預設情況下啟用。 這始終導致響應代碼200。 預設錯誤處理程式通過將完整堆棧跟蹤寫入響應來響應。
>
>在發佈實例上，CQ WCM調試篩選器為 **總是** 已禁用（即使配置為已啟用）。

## 如何自定義錯誤處理程式顯示的頁 {#how-to-customize-pages-shown-by-the-error-handler}

您可以開發自己的指令碼，以便在遇到錯誤時自定義錯誤處理程式顯示的頁。 為此，您將利用 [AEM標準覆蓋機構](/help/implementing/developing/introduction/overlays.md) 以便在 `/apps` 並覆蓋下面的預設頁面 `/libs`。

1. 在儲存庫中，複製預設指令碼：

   * 從 `/libs/sling/servlet/errorhandler/`
   * 至 `/apps/sling/servlet/errorhandler/`

   預設情況下，目標路徑不存在，因此您需要在首次執行此操作時建立它。

1. 導覽至 `/apps/sling/servlet/errorhandler`。在此，您可以：

   * 編輯相應的現有指令碼以提供所需的資訊。 或
   * 建立和編輯所需代碼的新指令碼。

1. 保存更改和test。

>[!CAUTION]
>
>的 `404.jsp` 指令碼是專門設計來滿足驗證AEM的；特別是，在出現這些錯誤時允許系統登錄。
>
>因此，更換這個劇本應該非常小心。

### 自定義對HTTP 500錯誤的響應 {#customizing-the-response-to-http-errors}

HTTP [500內部伺服器錯誤](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) 指示伺服器端錯誤，如伺服器遇到意外情況，導致無法完成請求。

當請求處理導致異常時，Apache Sling框架(基於AEM此框架構建):

* 記錄異常
* 並返回回答正文：
   * HTTP響應代碼500
   * 異常堆棧跟蹤

按 [自定義錯誤處理程式顯示的頁](#how-to-customize-pages-shown-by-the-error-handler) a `500.jsp` 可以建立指令碼。 但是，僅當 `HttpServletResponse.sendError(500)` 明確執行；也就是從例外捕手那裡。

否則，響應代碼設定為500，但 `500.jsp` 指令碼未執行。

要處理500個錯誤，錯誤處理程式指令碼的檔案名必須與異常類（或超類）相同。 要處理所有此類異常，可以建立指令碼 `/apps/sling/servlet/errorhandler/Throwable.jsp` 或 `/apps/sling/servlet/errorhandler/Exception.jsp`。

>[!NOTE]
>
>在作AEM為Cloud Service，當從後端接收到5XX錯誤時，CDN將提供一般錯誤頁。 為了允許後端的實際響應通過，您需要向響應添加以下標頭： `x-aem-error-pass: true`。
>這僅適用於來自Apache/AEMDispatcher層的響應。 來自中間基礎結構層的其他意外錯誤仍將顯示一般錯誤頁。

>[!CAUTION]
>
>在作者案中， [CQ WCM調試篩選器](/help/implementing/deploying/configuring-osgi.md) 預設情況下啟用。 這始終導致響應代碼200。 預設錯誤處理程式通過將完整堆棧跟蹤寫入響應來響應。
>
>對於自定義錯誤處理程式，需要代碼為500的響應 — 因此 [需要禁用CQ WCM調試篩選器。](/help/implementing/deploying/configuring-osgi.md) 這確保返迴響應代碼500，這反過來觸發正確的Sling錯誤處理程式。
>
>在發佈實例上，CQ WCM調試篩選器為 **總是** 已禁用（即使配置為已啟用）。
