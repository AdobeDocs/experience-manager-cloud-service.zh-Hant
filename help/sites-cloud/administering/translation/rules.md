---
title: 識別要翻譯的內容
description: 了解翻譯規則如何識別需要翻譯的內容。
feature: Language Copy
role: Admin
exl-id: 24cc6aa6-5b3c-462b-a10a-8b25277229dc
source-git-commit: 6be7cc7678162c355c39bc3000716fdaf421884d
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 0%

---

# 識別要翻譯的內容 {#identifying-content-to-translate}

翻譯規則可識別要翻譯的頁面、元件和資產，這些內容包含在翻譯專案中，或排除在翻譯專案之外。 翻譯頁面或資產時，AEM會擷取此內容，以便傳送至翻譯服務。

>[!TIP]
>
>如果您是初次翻譯內容，請參閱 [網站翻譯歷程，](/help/journey-sites/translation/overview.md) 這是使用AEM功能強大的翻譯工具來轉譯您的AEM Sites內容的引導式路徑，最適合沒有AEM或翻譯體驗的人。

## 內容片段和翻譯規則 {#content-fragments}

只有在 **啟用翻譯的內容模型欄位** 選項未在 [翻譯整合框架配置級別。](integration-framework.md#assets-configuration-properties)

若 **啟用翻譯的內容模型欄位** 選項處於作用中狀態，AEM將使用 **可翻譯** 欄位 [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragments-models.md#properties) 確定欄位是否要翻譯，並自動建立相應的翻譯規則。 此選項取代您可能建立的任何翻譯規則，不需要干預或執行其他步驟。

如果您想使用翻譯規則來轉譯內容片段，請 **啟用翻譯的內容模型欄位** 轉換整合架構設定的選項必須停用，您必須依照下列步驟建立規則。

## 總覽 {#overview}

頁面和資產在JCR存放庫中會以節點呈現。 提取的內容是節點的一個或多個屬性值。 翻譯規則可識別包含要擷取內容的屬性。

翻譯規則以XML格式表示，並儲存在以下可能的位置：

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

該檔案適用於所有翻譯項目。

規則包含下列資訊：

* 規則應用到的節點路徑
   * 此規則也適用於節點的子系。
* 包含要翻譯內容的節點屬性的名稱
   * 該屬性可以特定於特定資源類型或所有資源類型。

例如，您可以建立規則，將作者新增的內容轉譯至您頁面上的所有文字元件。 規則可識別 `/content` 節點和 `text` 屬性 `core/wcm/components/text/v2/text` 元件。

有 [主控台](#translation-rules-ui) 已新增用於設定翻譯規則。 UI中的定義會填入您的檔案。

如需AEM中內容翻譯功能的概觀，請參閱 [轉譯多語言網站的內容](overview.md).

>[!NOTE]
>
>AEM支援資源類型和參考屬性之間的一對一對應，以轉譯頁面上的參考內容。

## 頁面、元件和資產的規則語法 {#rule-syntax-for-pages-components-and-assets}

規則是 `node` 具有一個或多個子項的元素 `property` 元素和零個或多個子項 `node` 元素：

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

每個 `node` 元素具有以下特性：

* 此 `path` 屬性包含規則所應用分支的根節點的路徑。
* 子項 `property` 元素標識要為所有資源類型轉換的節點屬性：
   * 此 `name` 屬性包含屬性名稱。
   * 選填 `translate` 屬性等於 `false` 如果屬性未翻譯。 預設情況下，值為 `true`. 此屬性在覆寫先前的規則時很實用。
* 子項 `node` 元素標識要針對特定資源類型轉換的節點屬性：
   * 此 `resourceType` 屬性包含解析到實現資源類型的元件的路徑。
   * 子項 `property` 元素標識要轉換的節點屬性。 使用此節點的方式與子節點相同 `property` 節點規則的元素。

下列範例規則會造成 `text` 要翻譯的屬性 `/content` 節點。 此規則對於任何將內容儲存於 `text` 屬性，例如文字元件。

```xml
<node path="/content">
          <property name="text"/>
</node>
```

下列範例會轉譯所有內容 `text` 屬性，也轉換影像元件的其他屬性。 如果其他元件具有相同名稱的屬性，則不會套用規則。

```xml
<node path="/content">
      <property name="text"/>
      <node resourceType="core/wcm/components/image/v2/image">
         <property name="image/alt"/>
         <property name="image/jcr:description"/>
         <property name="image/jcr:title"/>
      </node>
</node>
```

## 從頁面擷取資產的規則語法  {#rule-syntax-for-extracting-assets-from-pages}

使用下列規則語法來包含內嵌在元件中或從元件參照的資產：

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

每個 `assetNode` 元素具有以下特性：

* 一 `resourceType` 屬性等於解析到元件的路徑
* 一 `assetReferenceAttribute` 屬性等於儲存資產二進位檔（針對內嵌資產）或參考資產路徑之屬性的名稱

下列範例會從影像元件中擷取影像：

```xml
<assetNode resourceType="core/wcm/components/image/v2/image" assetReferenceAttribute="fileReference"/>
```

## 覆寫規則 {#overriding-rules}

此 `translation_rules.xml` 檔案包含 `nodelist` 具有多個子項的元素 `node` 元素。 AEM會從上到下讀取節點清單。 當多個規則以相同節點為目標時，會使用檔案中較低的規則。 例如，下列規則會造成 `text` 要翻譯的屬性，但 `/content/mysite/en` 頁面分支：

```xml
<nodelist>
     <node path="/content”>
           <property name="text" />
     </node>
     <node path=“/content/mysite/en”>
          <property name=“text” translate=“false" />
     </node>
<nodelist>
```

## 篩選屬性 {#filtering-properties}

您可以使用 `filter` 元素。

例如，下列規則會造成 `text` 要轉換的屬性，但具有屬性的節點除外 `draft` 設為 `true`.

```xml
<nodelist>
    <node path="/content”>
     <filter>
   <node containsProperty="draft" propertyValue="true" />
     </filter>
        <property name="text" />
    </node>
<nodelist>
```

## 翻譯規則UI {#translation-rules-ui}

控制台也可用於配置翻譯規則。

若要存取：

1. 導覽至 **工具** 然後 **一般**.

1. 選擇 **翻譯設定**.

在翻譯規則UI中，您可以：

1. **新增內容**，可讓您新增路徑。

   ![添加翻譯上下文](../assets/add-translation-context.png)

1. 使用路徑瀏覽器來選取所需的內容，然後點選或按一下 **確認** 按鈕進行保存。

   ![選擇上下文](../assets/select-context.png)

1. 然後，您需要選取內容，然後按一下 **編輯**. 這會開啟翻譯規則編輯器。

   ![翻譯規則編輯器](../assets/translation-rules-editor.png)

您可以透過UI變更四個屬性：

* `isDeep`
* `inherit`
* `translate`
* `updateDestinationLanguage`

### isDeep {#isdeep}

**`isDeep`**  適用於節點篩選器，且預設為true。 它會檢查節點（或其祖先）是否包含篩選器中具有指定屬性值的屬性。 若為false，則只會檢查目前節點。

例如，即使父節點具有屬性，子節點也會添加到翻譯作業中 `draftOnly` 設為true，以標幟草稿內容。 此處 `isDeep` 會開始運作並檢查父節點是否具有屬性 `draftOnly` 為true，並排除這些子節點。

在編輯器中，您可以核取/取消核取 **深** 在 **篩選器** 標籤。

![篩選規則](../assets/translation-rules-editor-filters.png)

以下是產生的XML的範例，當 **深** 在UI中未勾選：

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

### 繼承 {#inherit}

**`inherit`** 適用於屬性。 依預設，會繼承每個屬性，但如果您不希望子項繼承某些屬性，則可將此屬性標籤為false，以便僅將其套用至該特定節點。

在UI中，您可以勾選/取消勾選 **繼承** 在 **屬性** 標籤。

### 翻譯 {#translate}

**`translate`** 僅用於指定是否轉換屬性。

在UI中，您可以勾選/取消勾選 **翻譯** 在 **屬性** 標籤。

### updateDestinationLanguage {#updatedestinationlanguage}

**`updateDestinationLanguage`** 用於沒有文字但語言代碼的屬性，例如 `jcr:language`. 用戶未翻譯文本，而是語言區域設定從源到目標。 這些屬性不會傳送以供翻譯。

在UI中，您可以勾選/取消勾選 **翻譯** 在 **屬性** 頁簽來修改此值，但對於具有語言代碼作為值的特定屬性。

協助釐清 `updateDestinationLanguage` 和 `translate`，以下是只有兩個規則的上下文的簡單範例：

![updateDestinationLanguage示例](../assets/translation-rules-updatedestinationlanguage.png)

xml中的結果如下所示：

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## 手動編輯規則檔案 {#editing-the-rules-file-manually}

此 `translation_rules.xml` 隨AEM安裝的檔案包含一組預設的翻譯規則。 您可以編輯檔案以支援翻譯專案的需求。 例如，您可以新增規則，以便翻譯自訂元件的內容。

如果您編輯 `translation_rules.xml` 檔案中，將備份副本保留在內容包中。 重新安裝某些AEM軟體包可以替換當前 `translation_rules.xml` 檔案。 若要在此情況下還原規則，您可以安裝包含備份副本的套件。

>[!NOTE]
>
>建立內容套件後，請在每次編輯檔案時重建套件。

## 翻譯規則檔案範例 {#example-translation-rules-file}

```xml
<?xml version="1.0" encoding="UTF-8"?><nodelist>
  <node path="/content">
    <property name="addLabel"/>
    <property name="allowedResponses"/>
    <property name="alt"/>
    <property name="attachFileLabel"/>
    <property name="benefits"/>
    <property name="buttonLabel"/>
    <property name="chartAlt"/>
    <property name="confirmationMessageToggle"/>
    <property name="confirmationMessageUntoggle"/>
    <property name="constraintMessage"/>
    <property name="contentLabel"/>
    <property name="denyText"/>
    <property name="detailDescription"/>
    <property name="emptyText"/>
    <property name="helpMessage"/>
    <property name="image/alt"/>
    <property name="image/jcr:description"/>
    <property name="image/jcr:title"/>
    <property name="jcr:description"/>
    <property name="jcr:title"/>
    <property name="heading"/>
    <property name="label"/>
    <property name="main"/>
    <property name="listLabel"/>
    <property name="moreText"/>
    <property name="pageTitle"/>
    <property name="placeholder"/>
    <property name="requiredMessage"/>
    <property name="resetTitle"/>
    <property name="subjectLabel"/>
    <property name="subtitle"/>
    <property name="tableData"/>
    <property name="text"/>
    <property name="title"/>
    <property name="navTitle"/>
    <property name="titleDivContent"/>
    <property name="toggleLabel"/>
    <property name="transitionLabel"/>
    <property name="untoggleLabel"/>
    <property name="name"/>
    <property name="occupations"/>
    <property name="greetingLabel"/>
    <property name="signInLabel"/>
    <property name="signOutLabel"/>
    <property name="pretitle"/>
    <property name="cq:panelTitle"/>
    <property name="actionText"/>
    <property name="cq:language" updateDestinationLanguage="true"/>
    <node pathContains="/cq:annotations">
      <property name="text" translate="false"/>
    </node>
    <node path="/content/wknd"/>
  </node>
  <node path="/content/forms">
    <property name="text" translate="false"/>
  </node>
  <node path="/content/dam">
    <property name="dc:description"/>
    <property name="dc:rights"/>
    <property name="dc:subject"/>
    <property name="dc:title"/>
    <property name="defaultContent"/>
    <property name="jcr:description"/>
    <property name="jcr:title"/>
    <property name="pdf:Title"/>
    <property name="xmpRights:UsageTerms"/>
    <property name="main"/>
    <property name="adventureActivity"/>
    <property name="adventureDescription"/>
    <property name="adventureDifficulty"/>
    <property name="adventureGearList"/>
    <property name="adventureGroupSize"/>
    <property name="adventureItinerary"/>
    <property name="adventurePrice"/>
    <property name="adventureTitle"/>
    <property name="adventureTripLength"/>
    <property name="adventureType"/>
    <node pathContains="/jcr:content/metadata/predictedTags">
      <property name="name"/>
    </node>
  </node>
  <assetNode assetReferenceAttribute="fragmentPath" resourceType="cq/experience-fragments/editor/components/experiencefragment"/>
  <assetNode assetReferenceAttribute="fragmentVariationPath" resourceType="core/wcm/components/experiencefragment/v1/experiencefragment"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="dam/cfm/components/contentfragment"/>
  <assetNode resourceType="docs/components/download"/>
  <assetNode resourceType="docs/components/image"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="foundation/components/image"/>
  <assetNode assetReferenceAttribute="asset" resourceType="foundation/components/video"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="foundation/components/download"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="core/wcm/components/download/v1/download"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="wcm/foundation/components/image"/>
  <assetNode assetReferenceAttribute="fragmentPath" resourceType="core/wcm/components/contentfragment/v1/contentfragment"/>
  <assetNode assetReferenceAttribute="fileReference" resourceType="core/wcm/components/image/v2/image"/>
</nodelist>
```
