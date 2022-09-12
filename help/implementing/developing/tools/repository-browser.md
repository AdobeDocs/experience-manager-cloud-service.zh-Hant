---
title: 存放庫瀏覽器
seo-title: Repository Browser
description: 存放庫瀏覽器針對製作、發佈和預覽層級的所有環境，提供存放庫的唯讀檢視。
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
source-git-commit: 46d8d78bd14f6e311d62266aa19825f82f82030d
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 2%

---

# 存放庫瀏覽器 {#repository-browser}

>[!NOTE]
>
>AEM 6582及更新版本提供存放庫瀏覽器。

>[!INFO]
>
>您也可以觀看 [這段](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html) 有關如何使用存放庫瀏覽器除錯AEMas a Cloud Service的快速影片簡介。

## 簡介 {#introduction}

存放庫瀏覽器是開發人員工具，可針對製作、發佈和預覽層級的所有環境，提供存放庫的唯讀檢視。 其設計旨在方便檢視內容結構，以便更容易檢視或偵錯內容。

可從開發人員控制台存取，以瀏覽作者的存放庫或發佈所選環境的例項。

### 存取必要條件 {#access-prerequisites}

若要存取「開發人員控制台」或「存放庫」瀏覽器，必須符合下列條件

若要存取開發人員控制台：

* 若為生產計畫，使用者必須具備 **Cloud Manager — 開發人員角色** 在Admin Console
* 針對沙箱方案，只要使用者具備產品設定檔，便可存取AEMas a Cloud Service。

要訪問儲存庫瀏覽器，請執行以下操作：

* 使用者必須擁有 **Cloud Manager — 開發人員** 檢視製作和發佈例項Admin Console中的角色。
* 此外，對於作者，具有AEM使用者產品設定檔的使用者只需最少的讀取存取權限，即可檢視存放庫瀏覽器；瀏覽存放庫時，會考量使用者的權限。 具有AEM管理員產品設定檔的使用者可以檢視具有完整讀取存取權的存放庫瀏覽器。

如需設定使用者權限的詳細資訊，請參閱 [Cloud Manager檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### 啟動儲存庫瀏覽器 {#launching-the-repository-browser}

依照下列步驟，即可啟動存放庫瀏覽器。

1. 在Cloud Manager中，按一下您所選取環境旁的三個點，然後選取 **開發人員控制台**

   ![repbrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. 下一步，按一下 **存放庫瀏覽器** 標籤
1. 按一下 **Pod** 下拉式清單。

   ![repbrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. 按一下 **開啟儲存庫瀏覽器** 進一步連結。 這會啟動與所選階層的代表例項(pod)對應的瀏覽器。 這會啟動與所選階層的代表例項(pod)對應的瀏覽器。 請注意，您無法控制已啟動之該層級的特定Pod。

## 功能 {#features}

### 導覽階層 {#navigate-the-hierarchy}

您可以使用左側導覽窗格來瀏覽內容階層。 按一下每個資料夾或節點將顯示其子項。 資料夾結構會反映Sling資源樹，這是JCR節點樹的超集。

![repbrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

或者，您也可以在 **路徑** 欄位，如下所示。 這也會展開其在左側內容階層檢視中的位置。

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

每當您按一下左側的資料夾，「路徑」欄位都會自動填入其位置。 這對於複製和貼上值以供稍後使用很實用。

此外，按一下資料夾時，會動態修改URL以包含該資料夾的路徑。 這可允許建立書籤URL。

若是發佈，依預設，存放庫瀏覽器只會顯示公開內容，因此某些資料夾如 `/conf` 或 `/home` 將不會顯示。

若要讓這些位置可見，您需要遵循下列程式。

1. 按一下您所選取環境旁的三個點，然後選取 **管理存取**

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. 尋找您的發佈例項，然後按一下

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. 為發佈管理員建立新的產品設定檔。 在以下範例中，稱為 **開發 — AEM管理員發佈**

   ![repbrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. 將適當的使用者（與應能以完整存取權導覽發佈存放庫瀏覽器的使用者對應）新增至新的產品設定檔

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. 等候幾分鐘，然後開啟 **AEM作者** 主控台
1. 將與新產品設定檔對應的群組新增為管理員群組的成員。 您可以按一下 **工具 — 安全性 — 作者群組**，然後按一下 **管理員** 群組。 然後，新增群組，如下所示

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. 啟動 **管理員** 和新的 **開發 — AEM管理員發佈** 群組，以便在發佈時使用

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. 作為一種良好的安全做法，請刪除新 **開發 — AEM管理員發佈** 從管理員群組(於 **作者** 因此，新群組會隔離以發佈

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. 存取發佈例項的存放庫瀏覽器時，所有資料夾都會顯示，包括 `/home` 和 `/conf`.

### 查看JCR屬性 {#view-jcr-properties}

按一下節點會在導覽瀏覽器的右側窗格中顯示其JCR屬性。 以下是 `experience-fragments` 節點。

![repbrowser4](/help/implementing/developing/tools/assets/repobrowser41.png)

### 檢視內容 {#view-content}

您可以按一下導覽窗格中的資源，使用存放庫瀏覽器來檢視內容。 這會開啟瀏覽器右側的預覽，位於以個別資源命名的標籤下。

![repbrowser6](/help/implementing/developing/tools/assets/repobrowser61.png)

下列清單中的影像類型目前可使用預覽：

* apping
* avif
* gif
* jpeg
* PNG
* svg+xml
* webp
* bmp
* x圖示
* tiff

以及下列以文字為基礎的mime類型：

* `"text/*"`
* `'application/javascript'`
* `'application/json'`
* `'application/x-sh'`

### 下載內容 {#download-content}

您也可以使用存放庫瀏覽器來下載內容。 在以下範例中，您可以按 **下載** 下載連結 `jcr:data` 與所選節點關聯。 導覽至包含屬性定義的節點，即可使用此功能供所有二進位屬性使用。

![repbrowser5](/help/implementing/developing/tools/assets/repobrowser52.png)
