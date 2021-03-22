---
title: AEM-使用商務整合架構的商務整合常見問答集
description: AEM-使用商務整合架構的商務整合常見問答集
translation-type: tm+mt
source-git-commit: 903a78d98082b937128073d5edce23dc70b01a1d
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 0%

---


# AEM-使用商務整合架構的商務整合常見問答集


## 1.CIF GraphQL僅用於商務，還是可用於查詢在。 JCR上創作的AEM內容？

Adobe已採用Magento的GraphQL API，做為所有商務相關資料的官方商務API。 因此，AEM使用GraphQL與Magento及任何商務引擎透過I/O Runtime交換商務資料。 此GraphQL API與GraphQL API無關AEM，可存取內容片段。

## 2.Adobe I/O是如何發揮作用的？ 是否AEM直接與Magento交談？

可以AEM直接連接到Magento，而不使用I/O Runtime層。 如果需要將非Magento商務後端（協力廠商解決方案）整合在一起AEM,I/O Runtime平台可用來主控對應層，將MagentoGraphQL API連接至任何協力廠商解決方案API。 有關此項的詳細資訊，請參閱此[參考實作](https://github.com/adobe/commerce-cif-graphql-integration-reference)。 對於非Magento解決方AEM案，將配置為指向I/O Runtime端點。

I/O Runtime平台也可用來擴充或自訂商務服務。 對於這種使用情形，您會呼叫I/O Runtime端點，接著該端點會代管各服務的自訂實作。 可結合整合與擴充使用案例。

## 3.產品資產（影像）是否可透過Magento管理員AEM儲存和參考？ 如何消費來自Dynamic Media的資產？

目前沒有AEM Assets——Magento一體化。 因應措施是，您可以將產品資產（影像）儲存在AEM Assets，但您必須手動將資產URL儲存在Magento中。 Dynamic Media現在是AEM Assets的一部分，將採取同樣的方式。

## 4.在何處部署商務解決方案是否重要？ （在預備或雲端）

您的商務解決方案部署在何處並不重要。 無論部署模式為何，AEM整合與全新Venia商店前線都能運作。 不過，如果根據已核准的E2E參考架構部署E2E測試，則會針對收集到的代表企業客戶個人檔案的效能KPI執行E2E測試。 因此，這將提供您其他資訊，以做為基準。

## 5.目錄頁面或產品頁面在中的建立方式AEM? 他們如何堅持AEM?

目錄頁面和產品頁面是根據一般目錄和產品頁面范AEM本動態建立和快取的。 不會將產品或目錄資料匯入並儲存在AEM中。

## 6.當您在商務解決方案中更新產品資料時，是否即時推送至AEM? 還是批次處理？

CIF附加元件與Cloud Service搭配使AEM用，讓資料從商務解決方案流AEM向隨選。 因此，當您的商務解決方案中有更新時，這不是即時推播或批次處理。

## 7.CIF支援的型AEM錄大小為何？

當產品資料和目錄頁面動態建立和快取時，沒有修正大小限制。 但是，目錄大小只有一個方面需要考慮。 快取率、並行資料要求和頁面建立都可能會影響擴充性和效能。

## 8.PIM如何在此框架中運作？

PIM資料通過GraphQL請AEM求公開給客戶端。 我們的建議是將PIM與商務引擎(Magento等)相整合，以便從商務引擎中檢索PIM資料。

## 9.您是否也可以通過Dispatcher快取定價和其他資料。 這是否會導致頻繁的快取失效挑戰？

Dispatcher上不會快取價格或庫存等動態資料。 動態資料會透過GraphQL API直接使用Web元件擷取用戶端。 Dispatcher上僅快取靜態資料（如產品或類別資料）。 如果產品資料變更，則需要快取失效。

## 10.Dispatcher的快取失效如AEM何與商AEM務搭配運作？

建議為Dispatcher上快取的頁設定基於TTL的快取失效。 如需價格或庫存等動態資訊，我們建議在用戶端轉譯日期。 有關基於TTL的快取失效的詳細資訊，請參AEM閱[ Dispatcher](https://helpx.adobe.com/experience-manager/kb/optimizing-the-dispatcher-cache.html)

## 11.是否建議使用「商務」對內容進行AEM統一搜尋？

提供了產品搜索參考實現，但沒有與內容相統一的搜索。 這項功能通常是客戶專屬的，在專案特定層級上可更好解決。

## 12.使用CIF搜尋與商AEM務如何運作？

CIF提供搜尋列和搜尋結果元件。 搜尋列元件會傳送含搜尋詞的GraphQL要求給商務解決方案，然後傳回包含產品名稱、價格、SLUG等的產品清單。 然後，「搜尋結果」元件會在所建立之搜尋結果頁面的圖庫檢視中顯示搜尋結果AEM。 「搜尋」支援基本全文搜尋。 我們使用SLUG/url索引鍵來建立PDP的參考。

## 13.如何在MSM或翻譯中使用產品資料？

產品資料通常已在PIM或Magento中轉譯。 -AEMMagento整合支援與多個Magento商店和商店視圖的連接。 在MSM設定中，通常有一AEM個網站會連結至一個Magento商店檢視。

## 14.CIF如何與非Magento商務平台搭配運作？

透過I/O Runtime平台與協力廠商解決方案(例如其他商務解決方案(非Magento)整合。  我們已建立[參考實作](https://github.com/adobe/commerce-cif-graphql-integration-reference)，以示範如何進行。 這樣，在任何第三方商務平台上公開MagentoGraphQL API，即可重複使用[AEM CIF雲連接器](https://github.com/adobe/commerce-cif-connector)和[AEM CIF核心元件](https://github.com/adobe/aem-core-cif-components)。 為提供最大的靈活性和可擴充性，此整合層部署在無伺服器[Adobe I/O Runtime平台](https://www.adobe.io/apis/experienceplatform/runtime.html)上。

## 15.有沒有辦法使用商業文字來增強產品資料？ 你從哪裡做的？ 在商AEM務解決方案中？

我們建議在中管理行銷相關資料和內AEM容。 使用內容片段的其他屬性來裝飾商務解決方案中的產品資料，或建立並連結體驗片段，以便將未結構化的內容與您的產品搭配使用。

## 16.當使用Adobe I/O Runtime平AEM台時，Magento之間的整合會改變嗎？

想要擴充商務服務的客戶可使用I/O Runtime平台上裝載的相同整合和編寫動作序列，以注入商業邏輯並豐富商務服務。

## 17.店SPA面會與編輯搭SPA配使用嗎？

可AEM當做任何商店前端的製作工具。 目前，店面會使用伺服器端和用戶端轉換(混合AEM)。 我們將於2021年稍後發佈PWA對無頭和無頭內容製作的支援。


## 18.在整個表現層使用時，我們如AEM何確保PCI合規性？

我們建議使用抽象化的付款方式。 這樣，瀏覽器用戶端就能與支付閘道提供者直接通訊，讓Adobe或商務解決方案都無法保存或傳遞持卡人資料。 此方法只需要3級PCI合規性。 不過，還有其他事項需要考慮完全符合PCI規範，例如員工與系統和資料的交互方式。 有關MagentoPCI合規性的更多資訊，請參閱https://magento.com/pci-compliance

## 19.如果我使用和AEMMagento雲端版本，此聯合解決方案是否符合PCI標準？

是的，自我評估調查表D和法規遵從性證明可應要求提供。


## 20.我要如何申請I/O Runtime試用授權？

您可以要求試用授權，以便使用I/O Runtime [，此處](https://adobeio.typeform.com/to/obqgRm)。
