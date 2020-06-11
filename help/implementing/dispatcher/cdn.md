---
title: AEM中的CDN（雲端服務）
description: AEM中的CDN（雲端服務）
translation-type: tm+mt
source-git-commit: a9bf697f65febcd9ba99539d8baa46f7a8d165e3
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 1%

---


# AEM中的CDN（雲端服務） {#cdn}

AEM as Cloud Service隨附內建CDN。 其主要目的是透過從邊緣的CDN節點（在瀏覽器附近）傳送可快取的內容，來減少延遲。 它已完全受管理，並且已設定為提供最佳的 AEM 應用程式效能。

AEM管理的CDN將可滿足大部分客戶的效能與安全性需求。 客戶可選擇從自己需要管理的CDN指向它。 這將根據符合特定先決條件（包括但不限於與其CDN廠商舊有整合且難以放棄的客戶）而逐個允許。

## AEM Managed CDN  {#aem-managed-cdn}

請依照下列步驟，使用Adobe的現成可用CDN來準備內容傳送：

1. 透過共用包含此資訊之安全表單的連結，將已簽署的SSL憑證和機密金鑰提供給Adobe。 請與客戶支援協調此項工作。
   **注意：** Aem作為雲端服務不支援「已驗證網域(DV)」憑證。
1. 通知客戶支援：
   * 哪個自定義域應與給定環境關聯，如程式ID和環境ID所定義。 請注意，作者端不支援自訂網域。
   * 如果需要任何IP白名單來限制特定環境的流量。
1. 與客戶支援協調，瞭解DNS記錄必要變更的時間安排。 根據是否需要頂點記錄，這些說明不同：
   * 如果不需要頂端記錄，客戶應將CNAME DNS記錄設定為將其FQDN指向 `cdn.adobeaemcloud.com`。
   * 如果需要尖峰記錄，請建立指向下列IP的A記錄： 151.101.3.10、151.101.67.10、151.101.131.10、151.101.195.10。 如果所需的FQDN與DNS區域匹配，客戶需要一個頂點記錄。 可使用Unix dig命令測試此命令，以查看輸出的SOA值是否與域匹配。 例如，該命 `dig anything.dev.adobeaemcloud.com` 令返回SOA(Start of Authority，即 `dev.adobeaemcloud.com` zone)，因此它不是APEX記錄，而 `dig dev.adobeaemcloud.com` 返回SOA, `dev.adobeaemcloud.com` 因此它是頂點記錄。
1. 當SSL憑證即將到期時，您會收到通知，因此您可以重新提交新的SSL憑證。

**限制流量**

依預設，對於Adobe Managed CDN設定，所有公開流量都可以進入發佈服務，適用於生產與非生產（開發與階段）環境。 如果您希望限制特定環境的發佈服務流量（例如，限制IP位址範圍的轉移），您應與客戶支援合作設定這些限制。

## 客戶CDN指向AEM Managed CDN {#point-to-point-CDN}

如果客戶必須使用其現有的CDN，則可以管理它並將其指向Adobe的受管理CDN，但必須符合下列條件：

* 客戶必須有現有的CDN，而且要取代的工作量很大。
* 客戶必須加以管理。
* 客戶必須能夠設定CDN以搭配AEM做為雲端服務使用——請參閱下方的設定指示。
* 客戶必須有工程CDN專家隨時待命，以備相關問題出現時使用。
* 客戶必須先執行並成功通過負載測試，才能開始生產。

配置說明：

1. 使用網 `X-Forwarded-Host` 域名稱設定標題。
1. 使用原始網域（即Adobe的CDN入口）設定主機標題。 價值應來自Adobe。
1. 將SNI報頭髮送到源。 與主機標頭一樣， sni標頭必須是源域。
1. 設定 `X-Edge-Key`要將流量正確路由至AEM伺服器所需的。 價值應來自Adobe。

在接受即時流量之前，您應向Adobe客戶支援驗證端對端流量路由是否正常運作。

請注意，由於額外的跳數，可能會造成小幅效能點擊，不過從客戶CDN到Adobe受管CDN的跳數可能會很有效。
