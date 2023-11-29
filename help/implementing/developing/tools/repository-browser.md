---
title: 存放庫瀏覽器
seo-title: Repository Browser
description: 存放庫瀏覽器針對作者、發佈和預覽層級的所有環境，提供存放庫的唯讀檢視。
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
source-git-commit: a7fa9ecc54bdee394852d765011df2ddd0a4950c
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 2%

---

# 存放庫瀏覽器 {#repository-browser}

>[!NOTE]
>
>存放庫瀏覽器適用於AEM 6582版及更新版本。

>[!INFO]
>
>您也可以觀看 [此剪輯](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html) ，快速瞭解如何使用存放庫瀏覽器針對AEMas a Cloud Service進行偵錯。

## 簡介 {#introduction}

存放庫瀏覽器是開發人員工具，可為作者、發佈和預覽層級的所有環境提供存放庫的唯讀檢視。 它設計為便於檢視內容結構，以便更輕鬆地檢視內容或為內容除錯。

可從存取 [AEMas a Cloud Service開發人員主控台](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)，它可用來瀏覽選定環境的作者或發佈執行個體的存放庫。

### 存取必要條件 {#access-prerequisites}

若要存取AEMas a Cloud Service開發人員控制檯或存放庫瀏覽器，下列條件必須滿足

若要存取AEMas a Cloud Service開發人員主控台：

* 對於生產計畫，使用者必須具有 **Cloud Manager — 開發人員角色** 在Adobe Admin Console中
* 對於沙箱計畫，它可供任何具有產品設定檔的使用者使用，以讓他們存取AEMas a Cloud Service。

若要存取存放庫瀏覽器：

* 使用者必須擁有 **Cloud Manager — 開發人員** 在AEMas a Cloud Service開發人員控制檯中擔任檢視作者和發佈執行個體的角色。
* 此外，對於作者，具有AEM使用者產品設定檔的使用者可以以最低的讀取存取權檢視存放庫瀏覽器；瀏覽存放庫時會考量使用者的許可權。 具有AEM管理員產品設定檔的使用者可以檢視具有完整讀取存取權的存放庫瀏覽器。

如需關於設定使用者許可權的詳細資訊，請參閱 [Cloud Manager檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/requirements/users-and-roles.html).

### 啟動存放庫瀏覽器 {#launching-the-repository-browser}

您可以依照下列步驟啟動存放庫瀏覽器。

1. 在Cloud Manager中，按一下您所選環境旁的三個點，然後選取 **開發人員主控台**

   ![repobrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. 接下來，按一下 **存放庫瀏覽器** 標籤
1. 按一下「 」，選擇與作者、發佈或預覽相對應的任何Pod **Pod** 下拉式清單。

   ![repobrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. 按一下「 」以啟動存放庫瀏覽器 **開啟存放庫瀏覽器** 連結更靠下方。 會啟動與所選階層之代表性執行個體(pod)對應的瀏覽器。 您無法控制所啟動之層級的特定Pod。

## 功能 {#features}

### 瀏覽階層 {#navigate-the-hierarchy}

您可以使用左側導覽窗格來導覽內容階層。 按一下每個資料夾或節點會顯示其子系。 資料夾結構會反映Sling資源樹狀結構，這是JCR節點樹狀結構的超級集。

![repobrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

或者，您可以直接導覽至路徑，方法是在以下位置輸入該路徑： **路徑** 欄位，如下所示。 此路徑也會展開其在左側內容階層檢視中的位置。

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

當您按一下左側的資料夾時，「路徑」欄位會自動填入其位置。 此功能對於複製和貼上值以供日後使用很有用。

此外，當您按一下資料夾時，URL會動態修改以包含該資料夾的路徑。 此功能允許使用可書籤的URL。

對於發佈，依預設，存放庫瀏覽器僅顯示公開內容，因此某些資料夾如下 `/conf` 或 `/home` 不可見。

若要使這些位置可見，請執行下列動作。

1. 按一下您所選環境旁的三個點，然後選取 **管理存取權**

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. 尋找您的發佈執行個體，然後按一下它

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. 為發佈管理員建立產品設定檔。 在以下範例中，它稱為 **DEV - AEM管理員發佈**

   ![repobrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. 將適當的使用者（對應於應能瀏覽具有完整存取權的發佈存放庫瀏覽器的使用者）新增至新產品設定檔

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. 等候幾分鐘，然後開啟 **AEM作者** 主控台
1. 按一下「 」，將與新產品設定檔相對應的群組新增為管理員群組的成員 **工具 — 安全性 — 作者上的群組**，然後按一下 **管理員** 群組。 然後，新增群組，如下所示

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. 啟動 **管理員** 和新的 **DEV - AEM管理員發佈** 群組，讓這些區段可在發佈時使用

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. 根據良好的安全性實務，請移除新的 **DEV - AEM管理員發佈** 群組（位於管理員群組） **作者** 因此新群組會被隔離以發佈

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. 存取發佈執行個體的存放庫瀏覽器時，所有資料夾皆可見，包括 `/home` 和 `/conf`.

### 檢視JCR屬性 {#view-jcr-properties}

按一下節點，導覽瀏覽器右側窗格中會顯示其JCR屬性。 以下是的範例 `experience-fragments` 節點。

![repobrowser4](/help/implementing/developing/tools/assets/repobrowser41.png)

### 檢視內容 {#view-content}

您可以使用存放庫瀏覽器來檢視內容。 按一下導覽窗格中的資源，即可在瀏覽器右側，在名稱為各資源名稱的標籤下開啟預覽。

![repobrowser6](/help/implementing/developing/tools/assets/repobrowser61.png)

預覽適用於下列影像型別：

* apng
* avif
* gif
* jpeg
* PNG
* svg+xml
* webp
* bmp
* x圖示
* tiff

對於下列文字型MIME型別，和：

* `"text/*"`
* `'application/javascript'`
* `'application/json'`
* `'application/x-sh'`

### 下載內容 {#download-content}

您也可以使用存放庫瀏覽器來下載內容。 在以下範例中，您可以按下 **下載** 下載連結 `jcr:data` 與所選節點相關聯。 此功能適用於所有二進位屬性，方法是導覽至包含屬性定義的節點。

![repobrowser5](/help/implementing/developing/tools/assets/repobrowser52.png)
