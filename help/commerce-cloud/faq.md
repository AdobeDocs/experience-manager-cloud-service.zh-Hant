---
title: AEM —— 使用商務整合架構進行Magento整合常見問答集
description: AEM —— 使用商務整合架構進行Magento整合常見問答集
translation-type: tm+mt
source-git-commit: cafe8825fe34f158c74b94b95b7252394de26e4d
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 0%

---


# AEM —— 使用商務整合架構進行Magento整合常見問答集


## 1. GraphQL僅用於Magento，還是可用於查詢在AEM. JCR上創作的內容？

Adobe已將Magento的GraphQL API作為其所有商務相關資料的官方商務API。 因此，AEM使用GraphQL與Magento及任何商務引擎透過I/O Runtime交換商務資料。

## 2. Adobe I/O如何發揮作用？ AEM是否直接與Magento通話？

AEM可直接連線至Magento，毋需I/O Runtime圖層。 如果需要將非Magento商務後端（協力廠商解決方案）與AEM整合，I/O Runtime平台可用來主控對應層，以將Magento GraphQL API連接至任何協力廠商解決方案API。 有關此項的詳細資訊，請參閱此參 [考實作](https://github.com/adobe/commerce-cif-graphql-integration-reference)。 對於非Magento解決方案，AEM會設定為指向I/O Runtime端點。

I/O Runtime平台也可用來擴充或自訂商務服務。 對於這種使用情形，您會呼叫I/O Runtime端點，接著該端點會代管各服務的自訂實作。 可結合整合與擴充使用案例。

## 3. 產品資產（影像）是否可透過Magento管理員從AEM儲存和參考？ 如何使用動態媒體的資產？

目前沒有AEM Assets - Magento整合。 因應措施是，您可以將產品資產（影像）儲存在AEM Assets中，但您必須在Magento中手動儲存資產URL。 Dynamic Media現在是AEM Assets的一部分，而且運作方式也相同。

## 4. 馬根托的部署位置重要嗎？ （在預備或雲端）

馬根托的部署位置並不重要。 不論部署模型為何，整合與全新AEM Venia商店前線都能運作。 不過，如果根據已核准的E2E參考架構部署E2E測試，則會針對收集到的代表企業客戶個人檔案的效能KPI執行E2E測試。 因此，這將提供您其他資訊，以做為基準。

## 5. 目錄頁面或產品頁面如何在AEM中建立？ 它們在AEM中的持續性如何？

目錄頁面和產品頁面會根據一般目錄和產品頁面範本，在AEM中動態建立和快取。 AEM不會匯入和儲存任何產品或目錄資料。

## 6. 您是否也可以通過Dispatcher快取定價和其他資料。 這是否會導致頻繁的快取失效挑戰？

Dispatcher上不會快取價格或庫存等動態資料。 動態資料會透過GraphQL API直接使用Web元件擷取用戶端。 Dispatcher上僅快取靜態資料（如產品或類別資料）。 如果產品資料變更，則需要快取失效。

## 7. AEM Dispatcher的快取失效如何與AEM-Magento搭配運作？

建議為Dispatcher上快取的頁設定基於TTL的快取失效。 如需價格或庫存等動態資訊，我們建議在用戶端轉譯日期。 如需TTL型快取失效的詳細資訊，請參閱 [AEM Dispatcher](https://helpx.adobe.com/experience-manager/kb/optimizing-the-dispatcher-cache.html)

## 8. 為什麼不使用We.Retail?

Venia主題（由Magento開發）是首先行動的，並與Magento的PWA一致。 Venia主題代表最新的CSS樣式和AEM核心元件。

## 9. 當您在Magento中更新產品資料時，是否即時推送至AEM? 還是批次處理？

與AEM Cloud Service搭配使用的CIF附加元件可讓資料從Magento流入AEM隨選。 因此，當Magento中有更新時，這不是即時推播或批次處理。

## 10. 是否建議使用「商務」跨AEM內容進行統一搜尋？

提供了產品搜索參考實現，但沒有與內容相統一的搜索。 這項功能通常是客戶專屬的，在專案特定層級上可更好解決。

## 11. 「搜尋」如何與使用CIF的AEM-Magento搭配運作？

CIF提供搜尋列和搜尋結果元件。 搜索欄元件將帶有搜索詞的GraphQL請求發送到Magento。 然後，Magento會傳回包含產品名稱、價格、SLUG等的產品清單。 然後，「搜尋結果」元件會在AEM中建立的搜尋結果頁面上，在圖庫檢視中顯示搜尋結果。 「搜尋」支援基本全文搜尋。 我們使用SLUG/url索引鍵來建立PDP的參考。

## 11. 如何在MSM或翻譯中使用產品資料？

產品資料通常已在PIM或Magento中轉譯。 AEM - Magento整合支援連線至多個Magento商店和商店檢視。 在MSM設定中，通常有一個AEM網站會連結至一個Magento商店檢視。

## 13. CIF公司如何與其他商務平台合作？

透過I/O Runtime平台與協力廠商解決方案(例如其他商務解決方案（非Magento）)整合。  我們已建立參 [考實作](https://github.com/adobe/commerce-cif-graphql-integration-reference) ，以示範如何進行。 如此可在任何協力廠商商務平台上公開 [Magento GraphQL API，以重複使用](https://github.com/adobe/commerce-cif-connector) AEM CIF Cloud Connector [和](https://github.com/adobe/aem-core-cif-components) AEM CIF Core Components。 為提供最大的彈性和可擴充性，此整合層部署在無伺服器 [Adobe I/O Runtime平台上](https://www.adobe.io/apis/experienceplatform/runtime.html)。

## 14. 有沒有辦法使用商業文字來增強產品資料？ 你從哪裡做的？ 在AEM還是在Magento?

要達到此目的，有多種方法，而且這取決於使用案例。 一種方式是使用自訂屬性。 允許AEM作者在AEM的產品編輯器中變更這些欄位，並將資料同步回PIM。 另一個選項是運用AEM Experience Fragments（會插入產品頁面）。

## 15. 當使用Adobe I/O Runtime平台時，AEM-Magento之間的整合會改變嗎？

想要擴充商務服務的客戶可使用I/O Runtime平台上裝載的相同整合和編寫動作序列，以注入商業邏輯並豐富商務服務。

## 16. 由於AEM會根據AEM中的一般範本動態建立產品和目錄頁面，如果我要開啟CRXDE Lite並檢查內容下方，我會看到什麼？ 我是否會在Magento中看到以產品為基礎的完整產品樹狀結構？ 如果沒有，作者會如何增強這些頁面？

JCR目錄或產品頁面已經不存在了。 見問題12。

## 17. SPA商店前端是否可與AEM SPA編輯器搭配運作？

AEM可用作任何商店前端的製作工具。 目前，混合演算是用於新店面。 未來，AEM將會用於與SPA和PWA一起編寫。

## 18. PIM如何在此框架中運作？

PIM資料會透過GraphQL要求公開給AEM和用戶端。 我們的建議是將PIM與商務引擎（Magento或其他引擎）整合，以便從商務引擎中檢索PIM資料。

## 19. 在整個表現層使用AEM時，我們如何確保符合PCI規範？

在AMS和Magento雲端部署中使用AEM時，必須使用抽象化的付款方法。 這可讓瀏覽器用戶端直接與付款閘道供應商通訊，讓Adobe或Magento雲端都無法儲存或傳遞持卡人資料。 此方法為技術堆棧和資料中心提供了PCI法規遵從性。 不過，還有其他事項需要考慮完全符合PCI規範，例如員工與系統和資料的交互方式。 有關Magento PCI合規性的更多資訊，請參閱https://magento.com/pci-compliance

## 20. 我要如何申請I/O Runtime試用授權？

您可以在這裡申請試用授權，以使用I/O Runtime [](https://github.com/AdobeDocs/adobeio-runtime/blob/master/overview/request_a_trial.md)。



