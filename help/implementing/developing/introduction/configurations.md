---
title: 設定和設定瀏覽器
description: 瞭解Adobe Experience Manager (AEM)設定，以及這些設定如何在AEM中管理工作區設定。
exl-id: 0ade04df-03a9-4976-a4b7-c01b4748474d
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 4%

---

# 設定和設定瀏覽器 {#configuration-browser}

Adobe Experience Manager (AEM)設定可管理AEM中的設定，並作為工作區。

## 什麼是設定？ {#what-is-a-configuration}

可以從兩個不同的觀點來考慮設定。

* [管理員](#configurations-administrator)使用設定作為AEM內的工作區，以定義和管理設定群組。
* [開發人員](#configurations-developer)使用實作設定的基礎設定機制，以便在AEM中儲存和查詢設定。

簡而言之：從管理員的觀點來看，組態是您建立工作區以管理AEM中設定的方式，而開發人員應瞭解AEM如何使用及管理存放庫中的這些組態。

無論您如何認為，設定在AEM中有兩個主要用途：

* 設定可為特定使用者群組啟用某些功能。
* 設定會定義這些功能的存取權。

## 管理員設定 {#configurations-administrator}

AEM管理員和作者可以將設定視為工作區。 藉由實作這些功能的存取許可權，這些工作區可用於收集設定群組及其相關內容，以進行組織作業。

可針對AEM中的許多不同功能建立設定。

* [上下文中心區段](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)
* [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
* [可編輯的範本](/help/sites-cloud/authoring/sites-console/templates.md)
* 各種雲端設定

### 範例 {#administrator-example}

例如，管理員可以為可編輯的範本建立兩個組態。

* WKND — 一般
* WKND-Magazine

然後，管理員可以使用WKND-General設定建立一般頁面範本，然後使用WKND-Magazine下的雜誌專用範本。

然後，管理員可以將WKND-General與WKND網站的所有內容相關聯。 不過，WKND-Magazine設定只會與magazine網站相關聯。

藉由執行此動作：

* 內容作者為雜誌建立頁面時，作者可以選擇一般範本(WKND-General)或雜誌範本(WKND-Magazine)。
* 當內容作者為網站中其他非雜誌部分建立頁面時，作者只能從一般範本(WKND-General)中選擇。

類似設定不僅適用於可編輯範本，也適用於雲端設定、ContextHub區段和內容片段模型。

### 使用設定瀏覽器 {#using-configuration-browser}

組態瀏覽器可讓管理員輕鬆建立、管理及設定AEM中組態的存取權。

>[!NOTE]
>
>如果您的使用者具有`admin`許可權，則只能使用設定瀏覽器建立設定。 若要指派存取許可權給組態或修改組態，也需要有此類`admin`許可權。

#### 建立設定 {#creating-a-configuration}

使用設定瀏覽器，即可在AEM中輕鬆建立設定。

1. 登入AEM as a Cloud Service，從主功能表選取&#x200B;**工具** > **一般** > **設定瀏覽器**。
1. 選取「**建立**」。
1. 提供設定的&#x200B;**標題**&#x200B;和&#x200B;**名稱**。

   ![建立設定](assets/configuration-create.png)

   * **標題** 應該是描述性的。
   * **名稱**&#x200B;會成為存放庫中的節點名稱。
      * 它會根據標題自動產生，並根據[AEM命名慣例進行調整。](naming-conventions.md)
      * 如有需要，可加以調整。
1. 檢查您要允許的設定型別。
   * [上下文中心區段](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)
   * [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
   * [可編輯的範本](/help/sites-cloud/authoring/sites-console/templates.md)
   * 各種雲端設定
1. 選取「**建立**」。

>[!TIP]
>
>設定可以巢狀化。

#### 編輯設定及其存取許可權 {#access-rights}

如果您將設定視為工作區，則可以在這些設定上設定存取權，以強制實行誰可以存取這些工作區，誰不可以存取。

1. 登入AEM as a Cloud Service，從主功能表選取&#x200B;**工具** > **一般** > **設定瀏覽器**。
1. 選取您要編輯的組態，然後在工具列中選取&#x200B;**屬性**。
1. 選取您要新增至設定的任何其他功能。

   >[!NOTE]
   >
   >建立設定後，就無法取消選取功能。

1. 使用&#x200B;**有效許可權**按鈕來檢視角色矩陣，以及這些角色目前授與組態哪些許可權。
   ![有效許可權視窗](assets/configuration-effective-permissions.png)
1. 若要指派新許可權，請在&#x200B;**新增許可權**&#x200B;區段的&#x200B;**選取使用者或群組**&#x200B;欄位中輸入使用者或群組名稱。
   * **選取使用者或群組**&#x200B;欄位會根據現有的使用者和角色提供自動完成功能。
1. 從自動完成結果中選取適當的使用者或角色。
   * 您可以選取多個使用者或角色。
1. 檢查一或多個選取的使用者或角色應該擁有的存取選項，然後按一下[新增]。****
   ![新增存取許可權至設定](assets/configuration-edit.png)
1. 重複這些步驟，您就可以選取使用者或角色，並視需要指派其他存取許可權。
1. 完成時選取&#x200B;**儲存並關閉**。

## 開發人員設定 {#configurations-developer}

作為開發人員，請務必瞭解AEM as a Cloud Service如何處理設定，以及如何處理設定解析。

### 設定與內容分離 {#separation-of-config-and-content}

雖然[管理員和使用者可能會將設定視為工作區](#configurations-administrator)，以管理不同的設定和內容，但請務必瞭解設定和內容是由AEM在存放庫中分別儲存和管理。

* `/content`是所有內容的首頁。
* `/conf`是所有設定的主目錄。

內容透過`cq:conf`屬性參考其關聯組態。 AEM會根據內容及其內容`cq:conf`屬性執行查詢，以尋找適當的組態。

### 範例 {#developer-example}

在此範例中，假設您有一些對DAM設定感興趣的應用程式程式碼。

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

所有組態查詢的起點是位於`/content`下的內容資源。 這可能是頁面、頁面內的元件、資產或DAM資料夾。 這是您要尋找適用於此內容的正確設定的實際內容。

現在擁有`Conf`物件，您可以擷取您感興趣的特定設定專案。 在此案例中，它是`dam/imageserver`，這是與`imageserver`相關的設定集合。 `getItem`呼叫傳回`ValueMap`。 接著您會讀取`bgkcolor`字串屬性，並提供「FFFFFF」的預設值，以防屬性（或整個設定專案）不存在。

現在來看看對應的JCR內容：

```text
/content/dam/wknd
    + jcr:content
      - cq:conf = "/conf/wknd"
    + image.png [dam:Asset]

/conf/wknd
    + settings
      + dam
        + imageserver [cq:Page]
          + jcr:content
            - bgkcolor = "FF0000"
```

在此範例中，您可以在此處假設WKND特定的DAM資料夾以及對應的設定。 從該資料夾`/content/dam/wknd`開始，您可以看到名稱為`cq:conf`的字串屬性參考了套用至子樹狀結構的組態。 屬性設定在資產資料夾或頁面的`jcr:content`上。 這`conf`個連結是明確的，因此只要檢視CRXDE中的內容，就能輕鬆追蹤連結。

在`/conf`內跳轉，追蹤參考，然後檢視是否有`/conf/wknd`節點。 此為設定。 其查詢對應用程式程式碼而言是透明的。 範常式式碼從未有專屬參考，而是隱藏在`Conf`物件之後。 要套用哪個設定，需透過JCR內容控制。

您會看到組態包含固定名稱的`settings`節點，其中包含實際專案，包括您在此情況下所需的`dam/imageserver`。 此類專案可視為「設定檔案」，並由包含實際內容的`jcr:content`的`cq:Page`表示。

最後，您會看到此範常式式碼需要的屬性`bgkcolor`。 您從`getItem`回訪的`ValueMap`是以頁面的`jcr:content`節點為基礎。

### 設定解析度 {#configuration-resolution}

上述基本範例顯示單一組態。 但在許多情況下，您會想要有不同的設定，例如預設全域設定、每個品牌的不同設定，以及子專案的特定設定。

為了支援此組態查詢，AEM具有繼承和遞補機制，其偏好設定順序如下：

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * 從`/content`中某處`cq:conf`參考的特定設定
   * 階層是任意的，而且可以像您的網站結構一樣設計，知道這一點並非應用程式程式碼的業務
   * 可由具有設定許可權的使用者在執行階段變更
1. `/conf/<siteconfig>/<parentconfig>`
   * 周遊父級以取得遞補設定
   * 可由具有設定許可權的使用者在執行階段變更
1. `/conf/<siteconfig>`
   * 周遊父級以取得遞補設定
   * 可由具有設定許可權的使用者在執行階段變更
1. `/conf/global`
   * 系統全域設定
   * 您安裝的全域預設值
   * 由`admin`角色設定
   * 可由具有設定許可權的使用者在執行階段變更
1. `/apps`
   * 應用程式預設值
   * 已修正應用程式部署
   * 在執行階段為唯讀
1. `/libs`
   * AEM產品預設值
   * 僅可依Adobe變更，不允許專案存取
   * 已修正應用程式部署
   * 在執行階段為唯讀

### 使用設定 {#using-configurations}

AEM中的設定是根據Sling內容感知設定。 Sling套件組合提供的服務API可用於取得內容感知設定。 內容感知組態是與內容資源或資源樹狀結構相關的組態，如上一個範例](#developer-example)所述[。

如需內容感知設定、範例及使用方式的詳細資訊，請參閱[Sling檔案。](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)。

### ConfMgr Web主控台 {#confmgr-web-console}

為了偵錯和測試目的，`https://<host>:<port>/system/console/conf`有一個&#x200B;**ConfMgr**&#x200B;網頁主控台，可顯示指定路徑/專案的設定。

![ConfMgr](assets/configuration-confmgr.png)

只需提供：

* **內容路徑**
* **專案**
* **使用者**

按一下[解決] ****，您就可以檢視已解決的組態，並取得有助於解決這些組態的程式碼範例。

### 內容感知設定Web主控台 {#context-aware-web-console}

為了偵錯和測試目的，`https://<host>:<port>/system/console/slingcaconfig`有一個&#x200B;**內容感知設定**&#x200B;網頁主控台，可讓您查詢存放庫中的內容感知設定並檢視其屬性。

![內容感知設定Web主控台](assets/configuration-context-aware-console.png)

只需提供：

* **內容路徑**
* **設定名稱**

按一下「解決&#x200B;****」，以擷取所選組態的相關內容路徑和屬性。
