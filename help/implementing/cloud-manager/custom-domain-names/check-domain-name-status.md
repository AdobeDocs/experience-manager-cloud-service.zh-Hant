---
title: 檢查域名狀態
description: 檢查域名狀態
translation-type: tm+mt
source-git-commit: 5cd22d8af20bb947e4cdab448cf8f20c6596bb2e
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 0%

---


# 檢查域名狀態 {#check-status}

您可以通過從「域設定」(Domain Settings)頁面的「環境」(Environments)表中按一下域名的「狀態」(Status)表徵圖來確定是否已成功驗證域名。

>[!NOTE]
>當您在「新增自訂網域」精靈的驗證步驟中選取「儲存」時，Cloud Manager會自動觸發TXT驗證。 對於後續的驗證，您必須主動選取狀態旁的「再次驗證」圖示。 插入影像

Cloud Manager將通過TXT值驗證域所有權，並顯示以下狀態消息之一：

* **域驗證失敗** TXT值缺失或檢測到錯誤。 請依照指示重試。 準備就緒後，您必須選取狀態旁的「再次驗證」圖示。

* **正在進行域驗證**&#x200B;正在進行中。 此狀態通常會在您選取狀態旁的「再次驗證」圖示後顯示。

* **已驗證，部署失敗** TXT驗證成功。 但是，CDN部署失敗。 Adobe代表會自動收到通知。

* **域驗證和部署**&#x200B;此狀態表示您的自定義域名已準備好使用。 注意：此時，您的自訂網域名稱已可供測試，並可指向Cloud Manager網域名稱。 請前往「設定DNS設定INSERT LINK」，瞭解如何執行此動作。

* **刪除**&#x200B;自訂網域名稱正在進行中。

* **刪除失敗**&#x200B;刪除自定義域名失敗。 您必須重試。 請至「刪除自訂網域名稱」以進一步瞭解主題。


## 配置DNS設定 {#configure-dns}

在您的自訂網域名稱經過成功驗證和部署後，您就可以使用DNS提供者更新自訂網域名稱的DNS記錄。 如此，您的網站便可為訪客提供服務。 因此，此活動通常在上線前完成。

>[!NOTE]
>您或貴組織中適當的個人必須能夠登入或聯絡您的DNS提供者（您向其購買網域的公司），並在您的DNS設定中進行更新。

為此，您必須確定您必須將DNS設定設為將自訂網域名稱指向 `CNAME` Cloud Manager網域名稱的Apex記錄。 一 `CNAME` 旦布建了A或A記錄，就會將網域的所有網際網路流量路由至網域所指的位置。 如果未布建該位置來提供流量，則會發生中斷。 如果尚未測試，內容中可能會有錯誤。 這就是為什麼測試完成後，客戶就可立即上線，而且始終要執行此步驟。

### CNAME記錄 {#cname-record}

以下幾節將幫助您確定哪種記錄適合您的DNS配置。

標準名稱或記 `CNAME` 錄是一種DNS記錄，可將別名映射為真或標準域名。 CNAME記錄通常用於將子網域（例如）映射 `www.example.com` 至代管該子網域內容的網域。

登入您的網域註冊機構並建立CNAME記錄，將您的自訂網域名稱指向目標，如下所示：

| CNAME | 自訂網域名稱指向目標 |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |

### APEX記錄 {#apex-record}

頂點網域是不包含子網域（例如example.com）的自訂網域。 頂端網域會透過您的DNS `A` 提供者 `ALIAS` ，以 `ANAME` 及記錄進行設定。 Apex網域必須指向特定的IP位址。

透過網域提供者，將下列所有A記錄新增至網域的DNS設定：

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`

## 檢查DNS記錄狀態 {#check-status-dns-record}

您可以從「網域設定」頁面的「環境」表格中，按一下DNS記錄的「狀態」圖示，判斷您的網域名稱是否正確解析為AEM雲端服務網站。 Cloud Manager會針對您的網域名稱執行DNS查閱，並顯示下列其中一條狀態訊息：

>[!NOTE]
>當您的自訂網域名稱首次成功驗證並部署時，Cloud Manager會自動觸發DNS查閱。 對於後續嘗試，必須主動選擇狀 **態旁邊的** 「重新解析」表徵圖。 插入影像

* **在您的自訂網域名**&#x200B;稱經過成功驗證和部署之後，將無法偵測到未偵測到DNS狀態。 當您的自訂網域名稱正在刪除時，也會觀察到此狀態。

* **DNS解析錯誤**&#x200B;這表示DNS記錄配置尚未解析／指向，或是錯誤。 Adobe代表會自動收到通知。

   >[!NOTE]
   >您必須按照相應 `CNAME` 的指 `A-record` 示配置或。 請至「設定DNS設定INSERT LINK」以進一步瞭解主題。 準備就緒後，您必須選取狀態旁的「重新解析」圖示。

* **正在進行DNS解**&#x200B;析。 此狀態通常會在您選取狀態旁的「再次解析」圖示後顯示。

* **DNS解析正確** DNS設定已正確設定。 您的網站為訪客提供服務。
