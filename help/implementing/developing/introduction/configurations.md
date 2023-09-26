---
title: 設定和設定瀏覽器
description: 瞭解Adobe Experience Manager (AEM)設定，以及這些設定如何在AEM中管理工作區設定。
exl-id: 0ade04df-03a9-4976-a4b7-c01b4748474d
source-git-commit: 78ead5f15c2613d9c3bed3025b43423a66805c59
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 4%

---

# 設定和設定瀏覽器 {#configuration-browser}

Adobe Experience Manager (AEM)設定可管理AEM中的設定，並作為工作區。

## 什麼是設定？ {#what-is-a-configuration}

可以從兩個不同的觀點來考慮設定。

* [管理員](#configurations-administrator) 使用設定作為AEM內的工作區來定義和管理設定群組。
* [開發人員](#configurations-developer) 使用實作設定的基礎設定機制，以在AEM中儲存和查詢設定。

簡而言之：從管理員的觀點來看，組態是您建立工作區以管理AEM中設定的方式，而開發人員應瞭解AEM如何使用及管理存放庫中的這些組態。

無論您如何認為，設定在AEM中有兩個主要用途：

* 設定可為特定使用者群組啟用某些功能。
* 設定會定義這些功能的存取權。

## 管理員設定 {#configurations-administrator}

AEM管理員和作者可以將設定視為工作區。 藉由實作這些功能的存取許可權，這些工作區可用於收集設定群組及其相關內容，以進行組織作業。

可針對AEM中的許多不同功能建立設定。

* [上下文中心區段](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)
* [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
* [可編輯的範本](/help/sites-cloud/authoring/features/templates.md)
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
>您只能使用設定瀏覽器建立設定，前提是您的使用者已 `admin` 權利。 此類 `admin` 指派存取許可權給設定或修改設定時，也需要許可權。

#### 建立設定 {#creating-a-configuration}

使用設定瀏覽器，即可在AEM中輕鬆建立設定。

1. 登入AEMas a Cloud Service，並從主功能表選取 **工具** -> **一般** -> **設定瀏覽器**.
1. 點選或按一下&#x200B;**建立**。
1. 提供設定的&#x200B;**標題**&#x200B;和&#x200B;**名稱**。

   ![建立設定](assets/configuration-create.png)

   * **標題** 應該是描述性的。
   * **名稱**&#x200B;會成為存放庫中的節點名稱。
      * 系統會根據標題自動產生，並依據下列專案進行調整 [AEM命名慣例。](naming-conventions.md)
      * 如有需要，可加以調整。
1. 檢查您要允許的設定型別。
   * [上下文中心區段](/help/sites-cloud/authoring/personalization/contexthub-segmentation.md)
   * [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)
   * [可編輯的範本](/help/sites-cloud/authoring/features/templates.md)
   * 各種雲端設定
1. 點選或按一下&#x200B;**建立**。

>[!TIP]
>
>設定可以巢狀化。

#### 編輯設定及其存取許可權 {#access-rights}

如果您將設定視為工作區，則可以在這些設定上設定存取權，以強制實行誰可以存取這些工作區，誰不可以存取。

1. 登入AEMas a Cloud Service，並從主功能表選取 **工具** -> **一般** -> **設定瀏覽器**.
1. 選取要編輯的組態，然後選取 **屬性** 工具列中的。
1. 選取您要新增至設定的任何其他功能。

   >[!NOTE]
   >
   >建立設定後，就無法取消選取功能。

1. 使用 **有效許可權** 按鈕以檢視角色及其目前授予設定的許可權矩陣。
   ![有效許可權視窗](assets/configuration-effective-permissions.png)
1. 若要指派新許可權，請在 **選取使用者或群組** 中的欄位 **新增許可權** 區段。
   * 此  **選取使用者或群組** 欄位會根據現有使用者和角色提供自動完成功能。
1. 從自動完成結果中選取適當的使用者或角色。
   * 您可以選取多個使用者或角色。
1. 勾選一或多個選取的使用者或角色應該擁有的存取選項，然後按一下 **新增**.
   ![將存取權新增至設定](assets/configuration-edit.png)
1. 重複這些步驟，您就可以選取使用者或角色，並視需要指派其他存取許可權。
1. 點選或按一下 **儲存並關閉** 完成後。

## 開發人員設定 {#configurations-developer}

作為開發人員，請務必瞭解AEMas a Cloud Service如何處理設定，以及如何處理設定解析。

### 設定與內容分離 {#separation-of-config-and-content}

雖然 [管理員和使用者可能會將設定視為工作區](#configurations-administrator) 若要管理不同的設定和內容，請務必瞭解設定和內容會由AEM在存放庫中個別儲存和管理。

* `/content` 是所有內容的首頁。
* `/conf` 是所有設定的首頁。

內容透過 `cq:conf` 屬性。 AEM會根據內容及其內容相關資訊來執行查詢 `cq:conf` 屬性以尋找適當的設定。

### 範例 {#developer-example}

在此範例中，假設您有一些對DAM設定感興趣的應用程式程式碼。

```java
Conf conf = resource.adaptTo(Conf.class);
ValueMap imageServerSettings = conf.getItem("dam/imageserver");
String bgkcolor = imageServerSettings.get("bgkcolor", "FFFFFF");
```

所有設定查詢的起點是下的內容資源 `/content`. 這可能是頁面、頁面內的元件、資產或DAM資料夾。 這是您要尋找適用於此內容的正確設定的實際內容。

現在使用 `Conf` 您可以擷取您感興趣的特定組態專案。 在此案例中，它是 `dam/imageserver`，此為與相關的設定集合。 `imageserver`. 此 `getItem` 呼叫傳回 `ValueMap`. 接著閱讀 `bgkcolor` 字串屬性，並提供「FFFFFF」預設值，以防屬性（或整個設定專案）不存在。

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

在此範例中，您可以在此處假設WKND特定的DAM資料夾以及對應的設定。 從該資料夾開始 `/content/dam/wknd`，您會看到有一個字串屬性命名為 `cq:conf` 會參照套用至子樹狀結構的組態。 屬性設定在 `jcr:content` 資產資料夾或頁面的。 這些 `conf` 連結是明確的，因此只要檢視CRXDE中的內容即可輕鬆追蹤。

跳入 `/conf`，請依照參考資料操作，並檢視 `/conf/wknd` 節點。 此為設定。 其查詢對應用程式程式碼而言是透明的。 範常式式碼從未有專屬的參考，而是隱藏在 `Conf` 物件。 要套用哪個設定，需透過JCR內容控制。

您會看到設定包含固定名稱 `settings` 包含實際專案的節點，包括 `dam/imageserver` 在此情況下，您需要。 此類專案可視為「設定檔案」，並以 `cq:Page` 包含 `jcr:content` 儲存實際內容。

最後，您會看到屬性 `bgkcolor` 此範常式式碼需要的。 此 `ValueMap` 您從回來 `getItem` 根據頁面的 `jcr:content` 節點。

### 設定解析度 {#configuration-resolution}

上述基本範例顯示單一組態。 但在許多情況下，您會想要有不同的設定，例如預設全域設定、每個品牌的不同設定，以及子專案的特定設定。

為了支援此組態查詢，AEM具有繼承和遞補機制，其偏好設定順序如下：

1. `/conf/<siteconfig>/<parentconfig>/<myconfig>`
   * 參考自的特定設定 `cq:conf` 中的某處 `/content`
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
   * 由設定 `admin` 角色
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

AEM中的設定是根據Sling內容感知設定。 Sling套件組合提供的服務API可用於取得內容感知設定。 內容感知組態是與內容資源或資源樹狀結構相關的組態 [如上一個範例所述。](#developer-example)

如需內容感知設定、範例及使用方式的詳細資訊， [請參閱Sling檔案。](https://sling.apache.org/documentation/bundles/context-aware-configuration/context-aware-configuration.html)

### ConfMgr Web主控台 {#confmgr-web-console}

為了進行偵錯和測試，我們提供 **ConfMgr** Web主控台： `https://<host>:<port>/system/console/conf`，可顯示指定路徑/專案的設定。

![ConfMgr](assets/configuration-confmgr.png)

只需提供：

* **內容路徑**
* **項目**
* **使用者**

按一下 **解析** 因此，您可以檢視已解析哪些組態，並取得有助於解析這些組態的程式碼範例。

### 內容感知設定Web主控台 {#context-aware-web-console}

為了進行偵錯和測試，我們提供 **內容感知設定** Web主控台： `https://<host>:<port>/system/console/slingcaconfig`，可查詢存放庫中的內容感知設定並檢視其屬性。

![內容感知設定Web控制檯](assets/configuration-context-aware-console.png)

只需提供：

* **內容路徑**
* **設定名稱**

按一下 **解析** 因此您可以擷取所選組態的關聯內容路徑和屬性。
