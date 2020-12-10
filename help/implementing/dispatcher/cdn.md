---
title: AEM as a Cloud Service 中的 CDN
description: AEM as a Cloud Service 中的 CDN
translation-type: tm+mt
source-git-commit: 40119f7b3bdf36af668b79afbcb2802a0b2a6033
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 7%

---


# AEM as a Cloud Service 中的 CDN {#cdn}

AEM as Cloud Service隨附內建CDN。 其主要目的是透過從邊緣的CDN節點（在瀏覽器附近）傳送可快取的內容，來減少延遲。 它已完全受管理，並且已設定為提供最佳的 AEM 應用程式效能。

AEM管理的CDN將可滿足大部分客戶的效能與安全性需求。 對於發佈層，客戶可選擇從自己的CDN指向它，而他們需要管理CDN。 這將根據符合特定先決條件（包括但不限於與其CDN廠商舊有整合且難以放棄的客戶）而逐個允許。

## AEM Managed CDN {#aem-managed-cdn}

請依照下列章節，使用Cloud Manager自助服務UI，使用Adobe的現成可用CDN來準備內容傳送：

1. [管理SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md)
1. [管理自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/introduction.md)

**限制流量**

依預設，對於Adobe Managed CDN設定，所有公開流量都可以進入發佈服務，適用於生產與非生產（開發與階段）環境。 如果您希望限制特定環境的發佈服務流量（例如，限制IP位址範圍的轉移），您可以透過Cloud Manager UI以自助方式進行。

請參閱[管理IP允許清單](/help/implementing/cloud-manager/ip-allow-lists/introduction.md)以瞭解更多資訊。

## 客戶CDN指向AEM Managed CDN {#point-to-point-CDN}

如果客戶必須使用其現有的CDN，則可以管理它並將其指向Adobe的受管理CDN，但必須符合下列條件：

* 客戶必須有現有的CDN，而且要取代的工作量很大。
* 客戶必須加以管理。
* 客戶必須能夠設定CDN以搭配AEM做為雲端服務使用——請參閱下方的設定指示。
* 客戶必須有工程CDN專家隨時待命，以備相關問題出現時使用。
* 客戶必須先執行並成功通過負載測試，才能開始生產。

配置說明：

1. 使用域名設定`X-Forwarded-Host`標頭。
1. 使用原始網域（即Adobe的CDN入口）設定主機標題。 價值應來自Adobe。
1. 將SNI報頭髮送到源。 與主機標頭一樣， sni標頭必須是源域。
1. 設定`X-Edge-Key`，以正確將流量路由至AEM伺服器。 價值應來自Adobe。

在接受即時流量之前，您應向Adobe客戶支援驗證端對端流量路由是否正常運作。

雖然從客戶CDN到Adobe受管CDN的躍點可能會很有效率，但由於額外的躍點，可能會造成小的效能點擊。

請注意，此客戶CDN設定支援發佈層，但不支援在作者層之前。
