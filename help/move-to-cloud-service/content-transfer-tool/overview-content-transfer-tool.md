---
title: 內容傳輸工具概觀
description: 內容傳輸工具概觀
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---


# 概覽 {#overview-content-transfer-tool}

「內容傳輸工具」是由Adobe開發的工具，可用來將現有內容從來源AEM例項（內部部署或AMS）移至目標AEM Cloud服務例項。

此工具還自動傳輸承擔者（用戶或組）。

內容傳輸有兩個相關階段：

1. **提取**:  擷取是指從來源AEM例項擷取內容至稱為移轉集的臨 *時區域*。 移 *轉集* 是Adobe提供的雲端儲存區，可暫時儲存來源AEM執行個體與Cloud Service AEM執行個體之間傳輸的內容。

   如需詳細 [資訊，請參閱內容傳輸中的擷取](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#extraction-process) 程式。

2. **擷取**: 擷取是指從移轉集將內 *容擷取* ，到目標Cloud Service例項。

   如需詳細 [資訊，請參閱內容傳輸中的擷取程式](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#ingestion-process) 。

移 *轉集* ，具有下列屬性：

* 在內容傳輸活動期間，最多可以一次建立和維護四個遷移集。
* 每個移轉集都應有唯一的名稱。
* 如果移轉集已停用超過30天，則會自動刪除它。
* 無論何時建立遷移集，它都與特定環境相關聯。 您只能將內容內嵌至相同環境的作者或發佈例項。

「內容傳輸工具」的功能可支援差異內容的向上調整，只能傳輸自先前的內容傳輸活動以來所做的變更。

>[!NOTE]
> 在初次傳輸內容後，建議您先執行頻繁的差異化內容頂層，以縮短最終差異化內容傳輸的內容凍結期，然後再在雲端服務上線。

在提取階段，要補 ***充現有遷移集*** ，必須禁 *用覆蓋選項* 。 如需詳細 [資訊，請參閱](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-extraction-process) 「向上擷取」。

在接收階段，要在當前內容之上應用Delta內容，必 *須禁用* 「擦除」選項。 如需詳細 [資訊，請參閱](/help/move-to-cloud-service/content-transfer-tool/using-content-transfer-tool.md#top-up-ingestion-process) 「向上擷取」。


## 准則與最佳實務 {#best-practices}

請依照以下章節瞭解使用內容傳輸工具的准則和最佳實務：

* 建議先對儲存庫執行壓縮、資料儲存一致性檢查，以發現潛在問題並減少儲存庫中存在的垃圾。

* 如果AEM Cloud作者內容傳送網路(CDN)設定已設定為擁有IP的白名單，則應確保來源環境IP也新增至白名單，如此來源環境與AEM Cloud環境就可以彼此通訊。

* 在擷取階段，建議使用啟用的擦除模式來執行擷取，當目標AEM Cloud Service環境中的現有儲存庫（作者或發佈）將完全刪除，然後使用移轉集資料進行更新時。 ** 此模式比非擦除模式快得多，在非擦除模式中，遷移集將應用於當前內容。

* 內容傳輸活動完成後，雲端服務環境中需要正確的專案結構，以確保內容在雲端服務環境中成功呈現。