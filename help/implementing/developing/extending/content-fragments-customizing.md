---
title: 自訂和擴充內容片段
description: 內容片段可擴充標準資產。 瞭解如何自訂。
exl-id: 58152d6e-21b6-4f45-a45c-0f46ee58825e
feature: Developing, Content Fragments
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 1%

---

# 自訂和擴充內容片段{#customizing-and-extending-content-fragments}

在Adobe Experience Manager as a Cloud Service中，內容片段會擴充標準資產；請參閱：

* [建立和管理內容片段](/help/sites-cloud/administering/content-fragments/overview.md)以及使用內容片段進行[頁面製作](/help/sites-cloud/authoring/fragments/content-fragments.md)，以取得有關內容片段的進一步資訊。

* [管理Assets](/help/assets/manage-digital-assets.md)以取得有關標準資產的進一步資訊。

## 架構 {#architecture}

內容片段的基本[組成部分](/help/sites-cloud/administering/content-fragments/overview.md#constituent-parts-of-a-content-fragment)如下：

* *內容片段*&#x200B;本身
* 它包含一或多個&#x200B;*內容元素*
* 它可以有一或多個&#x200B;*內容變數*

個別內容片段是以內容片段模式為基礎：

* 內容片段模型會在建立內容片段時定義其結構。
* 片段會參考模型；因此，模型的變更可能會影響或確實影響任何相依片段。
* 模型是由資料型別建立而成。
* 新增新變數的函式等，必須據此更新片段。

  >[!NOTE]
  >
  >若要您顯示/轉譯內容片段，您的帳戶必須擁有模型的`read`許可權。

  >[!CAUTION]
  >
  >對現有內容片段模型所做的任何變更都可能影響相依片段；這可能會導致這些片段中的孤立屬性。

### 網站與Assets的整合 {#integration-of-sites-with-assets}

內容片段管理(CFM)是Adobe Experience Manager (AEM) Assets的一部分，如下所示：

* 內容片段是資產。
* 他們使用現有的Assets功能。
* 這些控制檯已與Assets （管理主控台等）完全整合。

將內容片段視為AEM Sites功能，例如：

* 可在編寫頁面時使用。

#### 將內容片段對應至Assets {#mapping-content-fragments-to-assets}

![內容片段到資產](assets/content-fragment-to-assets.png)

根據內容片段模型的內容片段會對應至單一資產：

* 所有內容都儲存在資產的`jcr:content/data`節點下：

   * 元素資料儲存在主子節點下：
     `jcr:content/data/master`

   * 變數會儲存在具有變數名稱的子節點下：
例如，`jcr:content/data/myvariation`

   * 每個元素的資料都會儲存在個別子節點中，作為具有元素名稱的屬性：
例如，專案`text`的內容儲存為`text`上的屬性`jcr:content/data/master`

* 中繼資料和關聯內容儲存在`jcr:content/metadata`下方
除了標題和說明（不被視為傳統中繼資料，且儲存在`jcr:content`中）

#### 資產位置 {#asset-location}

與標準資產一樣，內容片段位於下：

`/content/dam`

#### 資產許可權 {#asset-permissions}

請參閱[內容片段 — 刪除考量事項](/help/sites-cloud/administering/content-fragments/delete-considerations.md)。

#### 功能整合 {#feature-integration}

若要與Assets核心整合：

* 內容片段管理(CFM)功能以Assets核心為基礎。

* CFM針對卡片/欄/清單檢視中的專案提供自己的實作；這些增效模組會插入現有的Assets內容呈現實作。

* 已擴充數個Assets元件，以符合內容片段。

### 在頁面中使用內容片段 {#using-content-fragments-in-pages}

>[!CAUTION]
>
>[內容片段元件是核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=zh-Hant)的一部分。 如需詳細資訊，請參閱[開發核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=zh-Hant)。

內容片段可以從AEM頁面引用，就像任何其他資產型別一樣。 AEM提供&#x200B;**[內容片段核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=zh-Hant)** - [元件，可讓您在頁面上包含內容片段](/help/sites-cloud/authoring/fragments/content-fragments.md#adding-a-content-fragment-to-your-page)。 您也可以擴充此&#x200B;**[內容片段](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=zh-Hant)**&#x200B;核心元件。

* 元件使用`fragmentPath`屬性來參考實際內容片段。 `fragmentPath`屬性的處理方式與其他資產型別的類似屬性相同；例如，當內容片段移至其他位置時。

* 元件可讓您選取要顯示的變數。

* 此外，也可以選取段落範圍來限制輸出；例如，這可用於多欄輸出。

* 元件允許中間內容：

   * 元件可讓您在參照片段的段落之間放置其他資產（影像等）。

   * 對於中間內容：

      * 請注意不穩定參考的可能性。 中間內容（在製作頁面時新增）與旁邊段落沒有固定的關係。 在中間內容的位置之前插入新段落（在內容片段編輯器中）可能會失去相對位置。

      * 請考慮使用其他引數（例如變數和段落篩選器）來設定要在頁面上呈現的內容。

>[!NOTE]
>
>**內容片段模型：**
>
>在頁面上使用內容片段時，會參考其所根據的內容片段模式。
>
>這表示，如果您在發佈頁面時尚未發佈模型，系統會標籤此模型，並將模型新增至要與頁面一起發佈的資源。

### 與其他架構整合 {#integration-with-other-frameworks}

內容片段可以整合至：

* **翻譯**

  內容片段已與[AEM翻譯工作流程](/help/sites-cloud/administering/translation/overview.md)完全整合。 在架構層級，這表示：

   * 內容片段的個別翻譯是單獨的片段；例如：

      * 它們位於不同的語言根下，但共用相關語言根下的相對路徑：

        `/content/dam/<path>/en/<to>/<fragment>`

        與

        `/content/dam/<path>/de/<to>/<fragment>`

   * 除了規則型路徑以外，內容片段的不同語言版本之間沒有其他連線。 雖然UI提供了在語言變體之間導覽的方法，但這些變體會作為兩個單獨的片段處理。

  >[!NOTE]
  >
  >AEM翻譯工作流程可與`/content`搭配使用：
  >
  >* 由於內容片段模型位於`/conf`，這些翻譯未包含在內。 您可以國際化UI字串。

* **中繼資料結構**

   * 內容片段會使用及重複使用可使用標準資產定義的[中繼資料結構](/help/assets/metadata-schemas.md)。

   * CFM提供專屬的結構描述：

     `/libs/dam/content/schemaeditors/forms/contentfragment`

     如有需要，可延長該期限。

   * 個別結構表單已與片段編輯器整合。

## 內容片段管理API — 伺服器端 {#the-content-fragment-management-api-server-side}

您可以使用伺服器端API來存取您的內容片段；請參閱：

[com.adobe.cq.dam.cfm](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/package-summary.html#package.description)

>[!CAUTION]
>
>Adobe建議使用伺服器端API，而非直接存取內容結構。

### 重要介面 {#key-interfaces}

下列三個介面可作為進入點：

* **內容片段** ([ContentFragment](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html))

  此介面可讓您以抽象方式處理內容片段。

  介面提供您執行下列作業的方法：

   * 管理基本資料（例如，取得名稱、取得/設定標題/說明）
   * 存取中繼資料
   * 存取元素：

      * 清單元素
      * 依名稱取得元素
      * 建立元素（請參閱[警告](#caveats)）

      * 存取元素資料（請參閱`ContentElement`）

   * 為片段定義的清單變數
   * 全域建立變數
   * 管理關聯內容：

      * 清單集合
      * 新增集合
      * 移除集合

   * 存取片段的模型

  代表片段主要元素的介面包括：

   * **Content元素** ([ContentElement](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentElement.html))

      * 取得基本資料（名稱、標題、說明）
      * 取得/設定內容
      * 存取元素的變數：

         * 清單變數
         * 依名稱取得變數
         * 建立變數（請參閱[警告](#caveats)）
         * 移除變數（請參閱[警告](#caveats)）
         * 存取變化資料（請參閱`ContentVariation`）

      * 解決變數的捷徑（如果指定的變數不適用於元素，則套用一些額外的實作專用遞補邏輯）

   * **內容變數** ([ContentVariation](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ContentVariation.html))

      * 取得基本資料（名稱、標題、說明）
      * 取得/設定內容
      * 根據上次修改資訊的簡單同步處理

  所有三個介面( `ContentFragment`、`ContentElement`、`ContentVariation`)都會延伸`Versionable`介面，新增內容片段所需的版本設定功能：

   * 建立元素的版本
   * 列出元素的版本
   * 取得已建立版本之元素的特定版本內容

### 調整 — 使用adaptTo() {#adapting-using-adaptto}

可調整以下內容：

* `ContentFragment`可以調整為：

   * `Resource` — 基礎Sling資源；直接更新基礎`Resource`需要重建`ContentFragment`物件。

   * `Asset` — 代表內容片段的DAM `Asset`抽象化；直接更新`Asset`需要重建`ContentFragment`物件。

* `ContentElement`可以調整為：

   * [`ElementTemplate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/ElementTemplate.html) — 用於存取專案的結構資訊。

* [`FragmentTemplate`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/cq/dam/cfm/FragmentTemplate.html)

* `Resource`可以調整為：

   * `ContentFragment`

### 警告 {#caveats}

請注意：

* 整個API的設計目的是&#x200B;**不**&#x200B;自動保留變更（除非在API JavaDoc中另有註明）。 因此，請一律認可個別請求的資源解析器（或您實際使用的解析器）。

* 可能需要額外努力的任務：

   * Adobe建議您從`ContentFragment`建立變數。 這可確保所有元素都共用此變數，並視需要更新適當的全域資料結構，以反映內容結構中的新變數。

   * 使用`ContentElement.removeVariation()`透過元素移除現有的變數並不會更新指派給變數的全域資料結構。 若要確保這些資料結構保持同步，請改用`ContentFragment.removeVariation()`，這會移除全域變數。

## 內容片段管理API — 使用者端 {#the-content-fragment-management-api-client-side}

>[!CAUTION]
>
>使用者端API為內部API。

### 其他資訊 {#additional-information}

請參閱下列內容：

* `filter.xml`

  用於內容片段管理的`filter.xml`已設定為不與Assets核心內容套件重疊。

## 編輯工作階段 {#edit-sessions}

>[!CAUTION]
>
>請考量此背景資訊。 您不應該在此變更任何專案（因為儲存庫中已標示為&#x200B;*私人區域*），但有時這可能有助於瞭解事情的幕後運作方式。

編輯內容片段(可跨越多個檢視(= HTML頁面))屬於原子性質。 因此，原子式多檢視編輯功能不是典型的AEM概念，內容片段會使用所謂的&#x200B;*編輯工作階段*。

當使用者在編輯器中開啟內容片段時，會啟動編輯工作階段。 當使用者透過選取&#x200B;**儲存**&#x200B;或&#x200B;**取消**&#x200B;而離開編輯器時，編輯工作階段即已完成。

技術上，所有編輯都是在&#x200B;*即時*&#x200B;內容上完成的，就像所有其他AEM編輯一樣。 開始編輯工作階段時，會建立目前未編輯狀態的版本。 如果使用者取消編輯，則會還原該版本。 如果使用者按一下&#x200B;**儲存**，則不會執行任何特定動作，因為編輯是在&#x200B;*即時*&#x200B;內容上執行，因此所有變更都會持續存在。 此外，按一下「**儲存**」會觸發一些背景處理，例如建立全文檢索搜尋資訊或處理混合媒體資產，或同時觸發兩者。

對於邊緣案例有一些安全措施；例如，如果使用者嘗試離開編輯器而未儲存或取消編輯工作階段。 此外，定期自動儲存也可防止資料遺失。
兩個使用者可以同時編輯相同的內容片段，因此會覆寫彼此的變更。 若要防止此情況，內容片段必須透過在片段上套用DAM管理的*簽出*&#x200B;動作來鎖定。

## 範例 {#examples}

### 範例：存取現有的內容片段 {#example-accessing-an-existing-content-fragment}

若要實現此目標，您可以將代表API的資源調整為：

`com.adobe.cq.dam.cfm.ContentFragment`

例如：

```java
// first, get the resource
Resource fragmentResource = resourceResolver.getResource("/content/dam/fragments/my-fragment");
// then adapt it
if (fragmentResource != null) {
    ContentFragment fragment = fragmentResource.adaptTo(ContentFragment.class);
    // the resource is now accessible through the API
}
```

### 範例：建立內容片段 {#example-creating-a-new-content-fragment}

若要以程式設計方式建立內容片段，請使用從模型資源改寫的`FragmentTemplate`。

例如：

```java
Resource modelRsc = resourceResolver.getResource("...");
FragmentTemplate tpl = modelRsc.adaptTo(FragmentTemplate.class);
ContentFragment newFragment = tpl.createFragment(parentRsc, "A fragment name", "A fragment description.");
```

### 範例：指定自動儲存間隔 {#example-specifying-the-auto-save-interval}

[自動儲存間隔](/help/sites-cloud/administering/content-fragments/managing.md#save-close-and-versions) （以秒為測量單位）可使用組態管理員(ConfMgr)定義：

* 節點： `<conf-root>/settings/dam/cfm/jcr:content`
* 屬性名稱： `autoSaveInterval`
* 類型：`Long`

* 預設： `600` （10分鐘）；這在`/libs/settings/dam/cfm/jcr:content`上定義

如果您想要設定5分鐘的自動儲存間隔，請在節點上定義屬性。

例如：

* 節點： `/conf/global/settings/dam/cfm/jcr:content`
* 屬性名稱： `autoSaveInterval`

* 類型：`Long`

* 值： `300` （5分鐘等於300秒）

## 用於頁面編寫的元件 {#components-for-page-authoring}

如需詳細資訊，請參閱

* [核心元件 — 內容片段元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=zh-Hant) （建議）
