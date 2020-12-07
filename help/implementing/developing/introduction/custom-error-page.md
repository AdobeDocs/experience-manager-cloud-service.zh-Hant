---
title: 自訂錯誤頁面
description: AEM隨附標準錯誤處理常式，可自訂HTTP錯誤。
translation-type: tm+mt
source-git-commit: d7e9bdee83f1b85436185ca57420ee178268cb33
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---


# 自定義錯誤頁{#customizing-error-pages}

AEM隨附標準錯誤處理常式，可處理HTTP錯誤；例如，顯示：

![標準錯誤訊息](assets/error-message-standard.png)

為回應錯誤，AEM在`/libs/sling/servlet/errorhandler`下方提供`404.jsp`指令碼。

>[!TIP]
>
>由於AEM是以Apache Sling為基礎，因此Apache錯誤處理檔案中有[的詳細資訊。](https://sling.apache.org/documentation/the-sling-engine/errorhandling.html)

>[!NOTE]
>
>在作者實例上，預設會啟用[CQ WCM除錯篩選器](/help/implementing/deploying/configuring-osgi.md)。 這一律會產生回應代碼200。 預設錯誤處理程式通過將完整堆棧跟蹤寫入響應來響應。
>
>在發佈例項上，CQ WCM除錯篩選器會一律停用&#x200B;****（即使設定為已啟用）。

## 如何自訂錯誤處理常式{#how-to-customize-pages-shown-by-the-error-handler}所顯示的頁面

您可以開發自己的指令碼，以自訂在遇到錯誤時由錯誤處理常式顯示的頁面。 若要這麼做，您將運用[AEM的標準覆蓋機制](/help/implementing/developing/introduction/overlays.md)，讓您的自訂頁面在`/apps`下建立，並覆蓋`/libs`下的預設頁面。

1. 在儲存庫中，複製預設指令碼：

   * 從 `/libs/sling/servlet/errorhandler/`
   * 至 `/apps/sling/servlet/errorhandler/`

   目標路徑預設不存在，因此您首次執行此動作時需要建立它。

1. 導航到 `/apps/sling/servlet/errorhandler`. 您可以在這裡：

   * 編輯適當的現有指令碼，以提供所需的資訊。 或
   * 建立和編輯所需程式碼的新指令碼。

1. 儲存變更並進行測試。

>[!CAUTION]
>
>`404.jsp`指令碼是專門設計來配合AEM驗證；尤其是允許在發生這些錯誤時進行系統登錄。
>
>因此，更換此指令碼時應格外小心。

### 自定義對HTTP 500錯誤的響應{#customizing-the-response-to-http-errors}

HTTP [500內部伺服器錯誤](https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html)表示伺服器端錯誤，例如伺服器遇到意外狀況，使其無法完成請求。

當請求處理導致例外時，Apache Sling架構（AEM是建立在此架構上）:

* 記錄異常
* 並返回回應正文：
   * HTTP回應碼500
   * 異常堆棧跟蹤

通過[自定義錯誤處理程式](#how-to-customize-pages-shown-by-the-error-handler)顯示的頁，可以建立`500.jsp`指令碼。 但是，只有在明確執行`HttpServletResponse.sendError(500)`時才使用；例如從例外捕手那裡。

否則，響應代碼設定為500，但不執行`500.jsp`指令碼。

要處理500個錯誤，錯誤處理程式指令碼的檔案名必須與異常類（或超類）相同。 要處理所有此類例外，可以建立指令碼`/apps/sling/servlet/errorhandler/Throwable.jsp`或`/apps/sling/servlet/errorhandler/Exception.jsp`。

>[!CAUTION]
>
>在作者實例上，預設會啟用[CQ WCM除錯篩選器](/help/implementing/deploying/configuring-osgi.md)。 這一律會產生回應代碼200。 預設錯誤處理程式通過將完整堆棧跟蹤寫入響應來響應。
>
>對於自訂錯誤處理常式，需要代碼為500的回應——因此必須停用[CQ WCM除錯篩選。](/help/implementing/deploying/configuring-osgi.md) 這可確保傳回回回應程式碼500，這會反過來觸發正確的Sling錯誤處理常式。
>
>在發佈例項上，CQ WCM除錯篩選器會一律停用&#x200B;****（即使設定為已啟用）。
