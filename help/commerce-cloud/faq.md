---
title: AEM — 使用Commerce Integration Framework進行Commerce整合常見問題集
description: AEM — 使用Commerce Integration Framework進行Commerce整合常見問題集
exl-id: 0a946d98-22c7-445d-984a-9e09c306ce45
source-git-commit: 5ad33f0173afd68d8868b088ff5e20fc9f58ad5a
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 0%

---

# AEM — 使用Commerce Integration Framework進行Commerce整合常見問題集

## 1. CIF GraphQL是否僅用於商務，或是否可用於查詢在AEM JCR上編寫的內容？

Adobe已採用Adobe Commerce的GraphQL API作為適用於所有商務相關資料的官方Commerce API。 因此，AEM會使用GraphQL透過I/O Runtime與Adobe Commerce及任何商務引擎交換商務資料。 此GraphQL API獨立於AEM GraphQL API，可存取內容片段。

## 2.能否透過Adobe Commerce管理員從AEM儲存及參考產品資產（影像）？ 如何使用Dynamic Media中的資產？

沒有官方的AEM Assets — 提供Adobe Commerce整合。 上有可用的合作夥伴聯結器 [marketplace](https://marketplace.magento.com) <!-- THIS IS THE OLD URL THAT WAS USED. IT WAS 404 (https://marketplace.magento.com/bounteous-dam.html) -->

或者，作為因應措施，您可以在AEM Assets中儲存產品資產（影像），但您必須在Adobe Commerce中手動儲存資產URL。 Dynamic Media現在是AEM Assets的一部分，且運作方式相同。

## 3.商業解決方案的部署位置重要嗎？ （內部部署或雲端）

不，您的商務解決方案部署在哪裡並不重要。 不論部署模式為何，CIF和AEM儲存庫都能運作。 不過，如果解決方案是使用建議的E2E參考架構進行部署，則E2E測試可以根據代表典型企業客戶設定檔的效能KPI執行。 此方法提供可當作基準的其他資訊。

## 4.如何在AEM中建立目錄頁面或產品頁面？ 它們如何在AEM中持續存在？

目錄頁面和產品頁面是根據通用目錄和產品頁面範本，在AEM中動態建立及快取。 AEM中不會匯入及儲存任何產品或目錄資料。

## 5.當您更新商務解決方案中的產品資料時，這是否為對AEM的即時推送？ 還是批次流程？

搭配AEM Cloud Service使用的CIF附加元件可讓資料從商務解決方案依需求傳輸至AEM。 因此，當您的商務解決方案中有更新時，這不是即時推送或批次流程。

## 6. AEM支援CIF的目錄大小多大？

這取決於您必須考慮的其他幾個方面。 您的目錄資料和頁面的快取比率是多少？ 您預期在高峰時段會有多少同時請求？ 您的商務解決方案API的擴充性如何？

## 7. PIM如何在這個架構中運作？

PIM資料會透過GraphQL要求向AEM和使用者端公開。 我們的建議是將PIM與商務引擎(Adobe Commerce或其他)整合，以便之後可以從商務引擎擷取PIM資料。

## 8.您也透過Dispatcher快取定價和其他資料嗎？ 這是否會造成頻繁的快取失效挑戰？

Dispatcher上不會快取價格或詳細目錄等動態資料。 直接透過GraphQL API，使用網頁元件在使用者端擷取動態資料。 Dispatcher上只會快取靜態資料（例如產品或類別資料）。 如果產品資料變更，則需要讓快取失效。

## 9. AEM Dispatcher的快取失效如何與AEM和商務搭配運作？

Adobe建議針對Dispatcher上快取的頁面設定TTL型快取失效。 若是價格或庫存等動態資訊，Adobe建議在使用者端轉譯資料。 如需有關TTL型快取失效的詳細資訊，請參閱 [最佳化Dispatcher快取](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html) 和 [AEM效能最佳化](https://experienceleague.adobe.com/docs/commerce-operations/deliver-commerce-at-scale/performance.html).

## 10.對於使用Commerce跨AEM內容進行整合式搜尋是否有任何建議？

已提供產品搜尋參考實作，但未提供具有內容的整合式搜尋。 此功能因客戶而異，專案專屬層級也能提供更好的解決方案。

## 11. Search如何使用CIF搭配AEM和商務使用？

CIF提供搜尋列和搜尋結果元件。 搜尋列元件會將具有搜尋字詞的GraphQL要求傳送至商業解決方案，然後傳回包含產品名稱、價格、SLUG等的產品清單。 「搜尋結果」元件接著會在以AEM建立的搜尋結果頁面上的相簿檢視中顯示搜尋結果。 「搜尋」支援基本的全文檢索搜尋。 我們使用SLUG/url鍵來建置PDP的參考。

## 12.如何在MSM或翻譯中使用產品資料？

產品資料已在PIM或Adobe Commerce中轉譯。 AEM - Adobe Commerce整合支援連線至多個Adobe Commerce商店和商店檢視。 在MSM設定中，通常一個AEM網站會連結至一個Adobe Commerce商店檢視。

## 13.是否有辦法以商業文字來增強產品資料？ 您會在哪裡執行此動作？ 在AEM中還是在商業解決方案中？

Adobe建議管理AEM中的行銷相關資料和內容。 使用內容片段的其他屬性裝飾您的商業解決方案的產品資料，或建立非結構化內容的體驗片段並將其與您的產品連結。

## 14.在整個簡報層使用AEM時，我們如何確保PCI相容性？

Adobe建議使用抽象的付款方法。 這樣一來，瀏覽器使用者端就會與支付閘道提供者直接通訊，因此Adobe或商業解決方案都不會保留或傳遞持卡人資料。 此方法只需要第3級PCI相容性。 不過，還有其他完全符合PCI規範的事項需要考慮，例如員工如何與系統和資料互動。 如需Adobe Commerce PCI法規遵循的詳細資訊，請參閱 [PCI法規遵循需求](https://business.adobe.com/products/magento/pci-compliance.html).

## 15.如果我使用AEM和Adobe Commerce雲端版本，此聯合解決方案是否符合PCI規範？

可以，您可以依要求取得自我評估問卷D和合規證明。

## 16.如何要求I/O Runtime試用版授權？

您可以要求試用授權以使用I/O Runtime [此處](https://developer.adobe.com/app-builder/trial/).
