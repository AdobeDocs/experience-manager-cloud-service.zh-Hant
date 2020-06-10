---
title: AEM中的CDN（雲端服務）
description: AEM中的CDN（雲端服務）
translation-type: tm+mt
source-git-commit: 9d99a7513a3a912b37ceff327e58a962cc17c627
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 2%

---


# AEM中的CDN（雲端服務） {#cdn}

AEM as Cloud Service隨附內建CDN。 其主要目的是透過從邊緣的CDN節點（在瀏覽器附近）傳送可快取的內容，來減少延遲。 它已完全受管理，並且已設定為提供最佳的 AEM 應用程式效能。

AEM總共提供兩個選項：

1. AEM Managed CDN - AEM的現成可用CDN。 它是緊密整合的選項，不需要大量客戶投資來支援與AEM的CDN整合。
1. 客戶管理的CDN指向AEM Managed CDN —— 客戶將自己的CDN指向AEM的現成可用的CDN。 客戶仍需要管理其自己的CDN，但是與AEM整合的投資並不大。

第一個選項應滿足大多數客戶效能和安全性要求。 此外，它需要客戶的最小努力。

第二個選項將逐個允許。 此決定是基於符合某些先決條件，包括但不限於與其CDN廠商舊有整合且難以放棄的客戶。

以下是比較兩個選項的決策矩陣。 詳細資訊請參閱下列章節。

| 詳細資料 | AEM Managed CDN | 客戶管理的CDN指向AEM CDN |
|---|---|---|
| **客戶工作** | 沒有，它完全整合。 只需將CNAME指向AEM Managed CDN。 | 適度的客戶投資。 客戶必須管理自己的CDN。 |
| **先決條件** | 無 | 需要替換的現有CDN十分繁雜。 上線前必須先示範成功的負載測試。 |
| **CDN專業知識** | 無 | 需要至少一次兼職的工程資源及能夠設定客戶CDN的詳細CDN知識。 |
| **安全性** | 由 Adobe 管理. | 由Adobe管理（也可由客戶在自己的CDN管理）。 |
| **效能** | 由Adobe最佳化。 | 將受益於某些AEM CDN功能，但由於額外的跳數，可能會造成小幅效能點擊。 **注意**: 從客戶CDN跳至Adobe立即可用的CDN可能會很有效率)。 |
| **快取** | 支援在調度器上應用的快取標頭。 | 支援在調度器上應用的快取標頭。 |
| **影像和視訊壓縮功能** | 可與Adobe Dynamic Media搭配使用。 | 可搭配Adobe Dynamic Media或客戶管理的CDN影像／視訊解決方案使用。 |

## AEM Managed CDN  {#aem-managed-cdn}

請依照下列步驟，使用Adobe的現成可用CDN來準備內容傳送：

1. 您將透過共用包含此資訊之安全表單的連結，將已簽署的SSL憑證和機密金鑰提供給Adobe。 請與客戶支援協調此項工作。
   **注意：** Aem作為雲端服務不支援「已驗證網域(DV)」憑證。
1. 您應通知客戶支援：
   * 哪個自定義域應與給定環境關聯，如程式ID和環境ID所定義。 請注意，作者端不支援自訂網域。
   * 如果需要任何IP白名單來限制特定環境的流量。
1. 您應與客戶支援協調DNS記錄必要變更的時間安排。 根據是否需要頂點記錄，這些說明不同：
   * 如果不需要頂端記錄，客戶應將CNAME DNS記錄設定為將其FQDN指向 `cdn.adobeaemcloud.com`。
   * 如果需要尖峰記錄，請建立指向下列IP的A記錄： 151.101.3.10、151.101.67.10、151.101.131.10、151.101.195.10。 如果所需的FQDN與DNS區域匹配，客戶需要一個頂點記錄。 可使用Unix dig命令測試此命令，以查看輸出的SOA值是否與域匹配。 例如，該命 `dig anything.dev.adobeaemcloud.com` 令返回SOA(Start of Authority，即 `dev.adobeaemcloud.com` zone)，因此它不是APEX記錄，而 `dig dev.adobeaemcloud.com` 返回SOA, `dev.adobeaemcloud.com` 因此它是頂點記錄。
1. 當SSL憑證即將到期時，您會收到通知，因此您可以重新提交新的SSL憑證。

**限制流量**

依預設，對於Adobe Managed CDN設定，所有公開流量都可以進入發佈服務，適用於生產與非生產（開發與階段）環境。 如果您希望限制特定環境的發佈服務流量（例如，限制IP位址範圍的轉移），您應與客戶支援合作設定這些限制。

## 客戶CDN指向AEM Managed CDN {#point-to-point-CDN}

如果您想要使用現有的CDN，但無法滿足客戶管理的CDN的需求，則支援此功能。 在這種情況下，您可以管理自己的CDN，但指向Adobe的受管CDN。

請注意：

1. 您必須有現有的CDN。
1. 你必須管好它。
1. 您必須能夠設定CDN以搭配Aem做為雲端服務使用——請參閱下方的設定指示。
1. 您必須有工程CDN專家隨時待命，以防相關問題出現。
1. 您必須先執行並成功通過負載測試，才能開始生產。

配置說明：

1. 使用網 `X-Forwarded-Host` 域名稱設定標題。
1. 使用原始網域（即Adobe的CDN入口）設定主機標題。 價值應來自Adobe。
1. 將SNI報頭髮送到源。 與主機標頭一樣， sni標頭必須是源域。
1. 設定 `X-Edge-Key`要將流量正確路由至AEM伺服器所需的。 價值應來自Adobe。

在接受即時流量之前，您應向Adobe客戶支援驗證端對端流量路由是否正常運作。
