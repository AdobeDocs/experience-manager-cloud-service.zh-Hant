---
title: AEM - 使用 Commerce Integration Framework 進行商務整合常見問題集
description: AEM - 使用 Commerce Integration Framework 進行商務整合常見問題集
exl-id: 0a946d98-22c7-445d-984a-9e09c306ce45
feature: Commerce Integration Framework
role: Admin, Architect, User
source-git-commit: fecbebde808c545a84889da5610a79c088f2f459
workflow-type: ht
source-wordcount: '960'
ht-degree: 100%

---

# AEM - 使用 Commerce Integration Framework 進行商務整合常見問題集

## &#x200B;1. CIF GraphQL 僅可用於商業，還是可用於查詢在 AEM JCR 上創作的內容？

Adobe 已採用 Adobe Commerce 的 GraphQL API 作為其所有商務相關資料的官方商務 API。因此，AEM 會使用 GraphQL 與 Adobe Commerce 以及透過 I/O 執行階段的任何商務引擎交換商務資料。此 GraphQL API 獨立於 AEM 的 GraphQL API 來存取內容片段。

## &#x200B;2. 產品資產 (影像) 是否可以透過 Adobe Commerce 管理員從 AEM 儲存和參考？如何使用 Dynamic Media 中的資產？

沒有可用的官方 AEM Assets - Adobe Commerce 整合。[Marketplace](https://marketplace.magento.com) 上提供了合作夥伴連接器<!-- THIS IS THE OLD URL THAT WAS USED. IT WAS 404 (https://marketplace.magento.com/bounteous-dam.html) -->

或者您可以使用因應措施，將產品資產 (影像) 儲存在 AEM Assets 中，但必須手動將資產 URL 儲存在 Adobe Commerce 中。Dynamic Media 現在屬於 AEM Assets 的一部分，其運作方式也一樣。

## &#x200B;3. 商務解決方案部署的位置重要嗎？(內部部署或在雲端中)

不重要，商務解決方案部署在哪裡都可以。無論部署模型如何，CIF 和 AEM 店面都可以正常運作。但是，如果使用建議的 E2E 參考架構部署解決方案，則可以針對代表典型企業客戶概況的效能 KPI 執行 E2E 測試。此方法提供了可當作基準的附加資訊。

## &#x200B;4. 如何在 AEM 中建立目錄頁面或產品頁面？它們如何留存在 AEM 中？

目錄頁面和產品頁面是根據一般目錄和產品頁面範本，在 AEM 中動態建立和快取的。產品或目錄資料不會匯入和儲存在 AEM 中。

## &#x200B;5. 當您在商務解決方案中更新產品資料時，會即時推送到 AEM 嗎？或者是採用批次處理？

與 AEM Cloud Service 結合使用的 CIF 附加元件可讓資料按照需求從商務解決方案流向 AEM。因此，當您的商務解決方案更新了內容時，不會即時推送或批次處理。

## &#x200B;6. 具有 CIF 的 AEM 支援多大的目錄大小？

這還需要將其他方面納入考慮。您的目錄資料和頁面的快取比率是多少？您預計高峰時段有多少並行要求？您商務解決方案 API 的可擴充性如何？

## &#x200B;7. PIM 如何在該框架中發揮作用？

PIM 資料透過 GraphQL 要求公開給 AEM 和用戶端。建議將 PIM 與商務引擎 (Adobe Commerce 或其他) 整合，以便從商務引擎擷取 PIM 資料。

## &#x200B;8. 您是否也透過 Dispatcher 快取定價和其他資料？這是否會引發頻繁的快取失效挑戰？

價格或庫存等動態資料不會在 Dispatcher 上快取。動態資料是透過 GraphQL API 在用戶端直接使用 Web 元件擷取的。僅靜態資料 (例如產品或類別資料) 可在 Dispatcher 上快取。如果產品資料發生變化，就需要快取失效。

## &#x200B;9. AEM Dispatcher 的快取失效如何與 AEM 和 Commerce 搭配使用？

Adobe 建議為 Dispatcher 上快取的頁面設定 TTL 型快取失效。對於價格或庫存等動態訊息，Adobe 建議在用戶端呈現資料。有關 TTL 型快取失效的詳細資訊，請參閱[最佳化 Dispatcher 快取](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17458.html?lang=zh-Hant)。

## &#x200B;10. 對於使用 Commerce 跨 AEM 內容進行整合搜尋有什麼建議嗎？

提供了產品搜尋參考實施，但沒有與內容進行整合搜尋。此功能是特定於客戶的，且最好在特定專案層級上解決。

## 11.「搜尋」在 AEM 和使用 CIF 的商務上的運作方式為何？

CIF 可提供搜尋列和搜尋結果元件。搜尋列元件會將包含搜尋字詞的 GraphQL 要求傳送至商務解決方案，然後商務解決方案會傳回包含產品名稱、價格、SLUG 等的產品清單。然後，搜尋結果元件會將搜尋結果顯示在於 AEM 中所建立搜尋結果頁面的程式庫檢視中。搜尋支援基本的全文搜尋。我們可使用 SLUG/url 鍵來建置對 PDP 的參考。

## &#x200B;12. 如何將產品資料用於 MSM 或翻譯？

產品資料已在 PIM 或 Adobe Commerce 中進行翻譯。AEM - Adobe Commerce 整合支援連接到多個 Adobe Commerce 商店和商店檢視。在 MSM 設定中，通常會將一個 AEM 網站連結到一個 Adobe Commerce 商店檢視。

## &#x200B;13. 是否能夠使用商務文字來增強產品資料？要在哪裡進行？在 AEM 還是在商務解決方案中？

Adobe 建議在 AEM 中管理行銷相關資料和內容。使用內容片段透過附加屬性修飾商務解決方案中的產品資料，或為非結構化內容建立體驗片段，並將其連結到您的產品。

## &#x200B;14. 在整個表示層使用 AEM 時，如何確保 PCI 合規性？

Adobe 建議使用抽象的付款方式。這可讓瀏覽器用戶端與支付閘道提供者直接通訊，如此 Adobe 或商務解決方案都不會儲存或傳遞持卡人資料。此方法僅需要 3 級 PCI 合規性。然而，要完全符合 PCI 標準還需要考慮其他事項，例如員工如何與系統和資料互動。有關 Adobe Commerce PCI 合規性的詳細資訊，請參閱「[PCI 合規性要求](https://business.adobe.com/products/magento/pci-compliance.html)」。

## &#x200B;15. 如果我使用 AEM 和 Adobe Commerce 雲端版本，此聯合解決方案是否符合 PCI 要求？

是的，可根據要求提供自我評估問卷 D 和合規性證明。

## &#x200B;16. 如何申請 I/O 執行階段試用版授權？

如需申請使用 I/O 執行階段的試用版授權的詳細資訊，請參閱[取得存取權](https://developer.adobe.com/runtime/docs/guides/overview/getting_access/)。