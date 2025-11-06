---
title: 存放庫瀏覽器
seo-title: Repository Browser
description: 存放庫瀏覽器針對作者、發佈和預覽層級的所有環境，提供存放庫的唯讀檢視。
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 1%

---

# 存放庫瀏覽器 {#repository-browser}

>[!NOTE]
>
>存放庫瀏覽器適用於AEM 6582版及更新版本。

>[!INFO]
>
>您也可以觀看[此片段](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html)，快速瞭解如何使用存放庫瀏覽器偵錯AEM as a Cloud Service。

## 簡介 {#introduction}

存放庫瀏覽器是開發人員工具，可為作者、發佈和預覽層級的所有環境提供存放庫的唯讀檢視。 它設計為便於檢視內容結構，以便更輕鬆地檢視內容或為內容除錯。

可從[AEM as a Cloud Service Developer Console](/help/implementing/developing/introduction/development-guidelines.md#crxde-lite-and-developer-console)存取，它可用來瀏覽所選環境的作者或發佈執行個體的存放庫。

### 存取的先決條件 {#access-prerequisites}

要存取AEM as a Cloud Service Developer Console或存放庫瀏覽器，必須滿足以下條件

若要存取AEM as a Cloud Service Developer Console，請參閱[Developer Console存取權](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console#developer-console-access)。

若要存取存放庫瀏覽器，必須具備與AEM as a Cloud Service Developer Console （以上指定）相同的條件。 檢視特定執行處理的「儲存區域瀏覽器」內容：

* 作者執行個體：擁有&#x200B;**作者執行個體**&#x200B;的AEM使用者產品設定檔的使用者，能夠以最低的讀取存取權檢視存放庫瀏覽器；瀏覽存放庫時會考量使用者的許可權。 具有AEM管理員產品設定檔的使用者可以檢視具有完整讀取存取權的存放庫瀏覽器。

* 發佈執行個體：具有&#x200B;**發佈執行個體**&#x200B;之AEM使用者產品設定檔的使用者，能夠以最低的讀取存取權檢視存放庫瀏覽器。 若沒有該產品設定檔集，使用者將以匿名使用者身分導覽，且由於許可權有限，部分路徑將不會顯示。

如需設定使用者許可權的詳細資訊，請參閱[Cloud Manager檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/requirements/users-and-roles.html)。

### 啟動存放庫瀏覽器 {#launching-the-repository-browser}

您可以依照下列步驟啟動存放庫瀏覽器。

1. 在Cloud Manager中，按一下您所選環境旁的三個點，然後選取&#x200B;**Developer Console**

   ![repobrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. 接著，按一下&#x200B;**存放庫瀏覽器**&#x200B;標籤
1. 按一下&#x200B;**Pod**&#x200B;下拉式清單，選擇與作者、發佈或預覽相對應的任何Pod。

   ![repobrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. 按一下下面的&#x200B;**開啟存放庫瀏覽器**&#x200B;連結，啟動存放庫瀏覽器。 會啟動與所選階層之代表性執行個體(pod)對應的瀏覽器。 您無法控制所啟動之層級的特定Pod。

## 功能 {#features}

### 瀏覽階層 {#navigate-the-hierarchy}

您可以使用左側導覽窗格來導覽內容階層。 按一下每個資料夾或節點會顯示其子系。 資料夾結構會反映Sling資源樹狀結構，這是JCR節點樹狀結構的超級集。

![repobrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

或者，您也可以在&#x200B;**路徑**&#x200B;欄位中輸入路徑，直接導覽至路徑，如下所示。 此路徑也會展開其在左側內容階層檢視中的位置。

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

當您按一下左側的資料夾時，「路徑」欄位會自動填入其位置。 此功能對於複製和貼上值以供日後使用很有用。

此外，當您按一下資料夾時，URL會動態修改以包含該資料夾的路徑。 此功能允許使用可書籤的URL。

對於發佈，依預設，存放庫瀏覽器只會顯示公開內容，因此某些資料夾（如`/conf`或`/home`）不會顯示。

若要使這些位置可見，請執行下列動作。

1. 按一下您所選環境旁的三個點，然後選取&#x200B;**管理存取權**

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. 尋找您的發佈執行個體，然後按一下它

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. 為發佈管理員建立產品設定檔。 在下列範例中，它稱為&#x200B;**DEV - AEM Administrators Publish**

   ![報表瀏覽器9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. 將適當的使用者（對應於應能瀏覽具有完整存取權的發佈存放庫瀏覽器的使用者）新增至新產品設定檔

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. 請稍候幾分鐘，然後開啟&#x200B;**AEM作者**&#x200B;主控台
1. 按一下作者上的&#x200B;**工具 — 安全性 — 群組**，然後按一下&#x200B;**管理員**&#x200B;群組，將對應到新產品設定檔的群組新增為管理員群組的成員。 然後，新增群組，如下所示

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. 啟動&#x200B;**管理員**&#x200B;和新的&#x200B;**DEV - AEM管理員發佈**&#x200B;群組，讓它們在發佈時可供使用

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. 好的安全性作法是，從&#x200B;**作者**&#x200B;上的管理員群組移除新的&#x200B;**DEV - AEM Administrators Publish**&#x200B;群組，以便將該新群組隔離以進行發佈

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. 存取發佈執行個體的存放庫瀏覽器時，所有資料夾皆可見，包括`/home`和`/conf`。

### 檢視JCR屬性 {#view-jcr-properties}

按一下節點，導覽瀏覽器右側窗格中會顯示其JCR屬性。 以下是`experience-fragments`節點的範例。

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

您也可以使用存放庫瀏覽器來下載內容。 在下列範例中，您可以按下&#x200B;**下載**&#x200B;連結來下載與所選節點相關聯的`jcr:data`。 此功能適用於所有二進位屬性，方法是導覽至包含屬性定義的節點。

![repobrowser5](/help/implementing/developing/tools/assets/repobrowser52.png)
