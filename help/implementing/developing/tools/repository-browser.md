---
title: 儲存庫瀏覽器
seo-title: Repository Browser
description: 儲存庫瀏覽器為作者、發佈和預覽層上的所有環境提供了儲存庫的只讀視圖。
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
source-git-commit: db70857458722f870dad37ac2bee6a19ef54171e
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 2%

---

# 儲存庫瀏覽器 {#repository-browser}

>[!NOTE]
>
>6582及更高版本上AEM提供了儲存庫瀏覽器。

>[!INFO]
>
>您還可以 [這個剪輯](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html) 有關如何使用儲存庫瀏覽器調試as a Cloud Service的快速視頻介AEM紹。

## 簡介 {#introduction}

儲存庫瀏覽器是一種開發工具，它為作者、發佈和預覽層上的所有環境提供了儲存庫的只讀視圖。 它設計為便於查看內容結構，以便更容易查看或調試內容。

可從開發人員控制台訪問，它可用於瀏覽作者的儲存庫或發佈所選環境的實例。

### 訪問先決條件 {#access-prerequisites}

必須滿足以下條件才能訪問開發人員控制台或儲存庫瀏覽器

要訪問Developer Console:

* 對於生產程式，用戶必須 **雲管理器 — 開發人員角色** Admin Console
* 對於沙盒程式，任何用戶都可以使用產品配置檔案，讓他們可以訪問AEMas a Cloud Service。

要訪問儲存庫瀏覽器：

* 用戶必須 **雲管理器 — 開發人員** 在Admin Console中查看「作者」和「發佈」實例的角色。
* 此外，對於作者而言，具有「用戶產品配置AEM檔案」的用戶可以以最少的讀取權限查看儲存庫瀏覽器；瀏覽儲存庫時尊重用戶的權限。 具有「管理員AEM產品配置檔案」的用戶可以使用完全讀取權限查看儲存庫瀏覽器。

有關設定用戶權限的詳細資訊，請參閱 [Cloud Manager文檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html)。

### 啟動儲存庫瀏覽器 {#launching-the-repository-browser}

可以按照以下步驟啟動儲存庫瀏覽器。

1. 在雲管理器中，按一下所選環境旁邊的三點，然後選擇 **開發人員控制台**

   ![repbrowser 1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. 接下來，按一下 **儲存庫瀏覽器** 頁籤
1. 通過按一下 **莢** 下拉清單。

   ![repbrowser 2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. 按一下 **開啟儲存庫瀏覽器** 連結進一步向下。 這將啟動與所選層的代表實例(pod)對應的瀏覽器。 這將啟動與所選層的代表實例(pod)對應的瀏覽器。 請注意，您無法控制已啟動的層的特定pod。

## 功能 {#features}

### 導航層次結構 {#navigate-the-hierarchy}

可以使用左側導航窗格來對內容層次結構進行修改。 按一下每個資料夾或節點將顯示其子項。 資料夾結構反映Sling資源樹，它是JCR節點樹的超集。

![repbrowser 3](/help/implementing/developing/tools/assets/repobrowser3.png)

對於發佈，預設情況下儲存庫瀏覽器只顯示公共內容，因此某些資料夾如 `/conf` 或 `/home` 不可見。

要使這些位置可見，您需要遵循以下步驟。

1. 按一下所選環境旁邊的三點，然後選擇 **管理訪問**

   ![repbrowser 7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. 查找發佈實例，然後按一下

   ![repbrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. 為發佈管理員建立新的產品配置檔案。 在下面的示例中，它稱為 **DEV — 管AEM理員發佈**

   ![repbrowser 9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. 向新產品配置檔案中添加相應用戶，這些用戶與應該能夠以完全訪問權限導航發佈儲存庫瀏覽器的用戶相對應

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. 等待幾分鐘，然後開啟 **AEM作者** 控制台
1. 將與新產品配置檔案對應的組添加為管理員組的成員。 您可以通過按一下 **工具 — 安全性 — 作者組**，然後按一下 **管理員** 組。 然後，按如下所示添加組

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. 激活 **管理員** 和新 **DEV — 管AEM理員發佈** 組，以便它們在發佈時可用

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. 作為一種良好的安全做法，請刪除 **DEV — 管AEM理員發佈** 組，從管理員組 **作者** 所以新組別被隔離出來發佈

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. 訪問發佈實例的儲存庫瀏覽器時，所有資料夾都可見，包括 `/home` 和 `/conf`。

### 查看JCR屬性 {#view-jcr-properties}

按一下某個節點將在導航瀏覽器的右窗格中顯示其JCR屬性。 下面是 `experience-fragments` 的下界。

![repbrowser 4](/help/implementing/developing/tools/assets/repobrowser41.png)

### 檢視內容 {#view-content}

您可以使用儲存庫瀏覽器通過按一下導航窗格中的資源來查看內容。 這將開啟瀏覽器右側以相應資源命名的頁籤下的預覽。

![repbrowser 6](/help/implementing/developing/tools/assets/repobrowser61.png)

預覽當前可用於以下清單中的影像類型：

* 拍
* 飛行
* gif
* jpeg
* PNG
* svg+xml
* 網頁
* 骨
* x表徵圖
* 原告

對於以下基於文本的mime類型：

* `"text/*"`
* `'application/javascript'`
* `'application/json'`
* `'application/x-sh'`

### 下載內容 {#download-content}

您還可以使用儲存庫瀏覽器下載內容。 在下面的示例中，您可以按 **下載** 連結以下載 `jcr:data` 與所選節點關聯。 通過導航到包含屬性定義的節點，此功能可用於所有二進位屬性。

![rep瀏覽器5](/help/implementing/developing/tools/assets/repobrowser52.png)
