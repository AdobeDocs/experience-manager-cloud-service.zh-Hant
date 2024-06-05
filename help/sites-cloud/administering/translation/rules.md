---
title: 識別要翻譯的內容
description: 瞭解翻譯規則如何識別需要翻譯的內容。
feature: Language Copy
role: Admin
exl-id: 24cc6aa6-5b3c-462b-a10a-8b25277229dc
solution: Experience Manager Sites
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1288'
ht-degree: 1%

---

# 識別要翻譯的內容 {#identifying-content-to-translate}

翻譯規則會針對翻譯專案中包含或排除的頁面、元件和資產，識別要翻譯的內容。 在翻譯頁面或資產時，AEM會擷取此內容，以便將其傳送至翻譯服務。

>[!TIP]
>
>如果您不熟悉翻譯內容，請參閱 [網站翻譯歷程，](/help/journey-sites/translation/overview.md) 將引導您使用AEM強大的翻譯工具來翻譯AEM Sites內容，非常適合沒有AEM或翻譯經驗的人士。

## 內容片段和翻譯規則 {#content-fragments}

本檔案所述翻譯規則僅適用於 **啟用內容模型欄位以進行翻譯** 選項尚未在啟用 [翻譯整合框架設定層級。](integration-framework.md#assets-configuration-properties)

如果 **啟用內容模型欄位以進行翻譯** 選項作用中，AEM將使用 **可翻譯** 欄位於 [內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#properties) 以判斷欄位是否要翻譯，並據此自動建立翻譯規則。 此選項會取代您可能已建立的任何翻譯規則，而且不需要介入或額外的步驟。

如果要使用翻譯規則來翻譯您的內容片段，請 **啟用內容模型欄位以進行翻譯** 必須停用「翻譯整合架構」設定上的選項，而且您必須依照下列步驟建立規則。

## 概觀 {#overview}

頁面和資產在JCR存放庫中會顯示為節點。 擷取的內容是節點的一或多個屬性值。 翻譯規則會識別包含要擷取之內容的屬性。

翻譯規則會以XML格式表示，並儲存在下列可能位置：

* `/libs/settings/translation/rules/translation_rules.xml`
* `/apps/settings/translation/rules/translation_rules.xml`
* `/conf/global/settings/translation/rules/translation_rules.xml`

檔案適用於所有翻譯專案。

規則包含下列資訊：

* 規則套用的節點路徑
   * 此規則也會套用至節點的子代。
* 包含要翻譯之內容的節點屬性名稱
   * 屬性可特定於特定資源型別或所有資源型別。

例如，您可以建立規則來轉譯作者新增至您頁面上所有文字元件的內容。 此規則可識別 `/content` 節點和 `text` 的屬性 `core/wcm/components/text/v2/text` 元件。

有一個 [主控台](#translation-rules-ui) 已新增用於設定翻譯規則。 UI中的定義將為您填入檔案。

如需AEM內容翻譯功能的總覽，請參閱 [翻譯多語言網站的內容](overview.md).

>[!NOTE]
>
>AEM支援資源型別和參考屬性之間的一對一對應，以便翻譯頁面上的參考內容。

## 頁面、元件和資產的規則語法 {#rule-syntax-for-pages-components-and-assets}

規則是 `node` 具有一或多個子項的元素 `property` 元素和零個或多個子項 `node` 元素：

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

每一個 `node` 元素具有下列特性：

* 此 `path` attribute包含套用規則之分支的根節點的路徑。
* 子項 `property` 元素會為所有資源型別識別要翻譯的節點屬性：
   * 此 `name` 屬性包含屬性名稱。
   * 選填 `translate` 屬性等於 `false` 如果屬性未翻譯。 預設值為 `true`. 覆寫先前的規則時，此屬性相當實用。
* 子項 `node` 元素會針對特定資源型別識別要翻譯的節點屬性：
   * 此 `resourceType` attribute包含解析為實作資源型別的元件的路徑。
   * 子項 `property` 元素會識別要翻譯的節點屬性。 以與子節點相同的方式使用此節點 `property` 節點規則的元素。

以下範例規則會導致 `text` 要為以下的所有頁面翻譯的屬性 `/content` 節點。 此規則適用於任何將內容儲存在 `text` 屬性，例如文字元件。

```xml
<node path="/content">
          <property name="text"/>
</node>
```

以下範例轉譯所有 `text` 屬性，也會轉譯影像元件的其他屬性。 如果其他元件具有同名屬性，則規則不適用於它們。

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

每個 `assetNode` 元素具有下列特性：

* 一 `resourceType` 代表解析為元件的路徑的屬性
* 一 `assetReferenceAttribute` 屬性，代表儲存資產二進位檔（用於內嵌資產）之屬性的名稱或參考資產的路徑

下列範例會從影像元件中擷取影像：

```xml
<assetNode resourceType="core/wcm/components/image/v2/image" assetReferenceAttribute="fileReference"/>
```

## 覆寫規則 {#overriding-rules}

此 `translation_rules.xml` 檔案包含 `nodelist` 具有多個子項的元素 `node` 元素。 AEM會從上到下讀取節點清單。 如果有多個規則鎖定同一個節點，系統會使用檔案中較低位置的規則。 例如，下列規則會導致所有內容在 `text` 要翻譯的屬性，但 `/content/mysite/en` 頁面分支：

```xml
<nodelist>
     <node path="/content">
           <property name="text" />
     </node>
     <node path="/content/mysite/en">
          <property name="text" translate="false" />
     </node>
<nodelist>
```

## 篩選屬性 {#filtering-properties}

您可以使用來篩選具有特定屬性的節點 `filter` 元素。

例如，下列規則會導致所有內容在 `text` 要翻譯的屬性，但具有屬性的節點除外 `draft` 設為 `true`.

```xml
<nodelist>
    <node path="/content">
     <filter>
   <node containsProperty="draft" propertyValue="true" />
     </filter>
        <property name="text" />
    </node>
<nodelist>
```

## 翻譯規則UI {#translation-rules-ui}

控制檯也可用於設定翻譯規則。

若要存取它：

1. 瀏覽至 **工具** 然後 **一般**.

1. 選取「**翻譯設定**」。

在翻譯規則UI中，您可以：

1. **新增內容**，可讓您新增路徑。

   ![新增翻譯內容](../assets/add-translation-context.png)

1. 使用路徑瀏覽器來選取所需的前後關聯，然後選取 **確認** 按鈕以儲存。

   ![選取內容](../assets/select-context.png)

1. 之後，您需要選取內容，然後按一下 **編輯**. 如此將可開啟翻譯規則編輯器。

   ![翻譯規則編輯器](../assets/translation-rules-editor.png)

您可以透過UI變更四個屬性：

* `isDeep`
* `inherit`
* `translate`
* `updateDestinationLanguage`

### isDeep {#isdeep}

**`isDeep`**  適用於節點篩選器，預設為true。 它會檢查節點（或其上階）是否在篩選器中包含具有指定屬性值的屬性。 若為false，則僅檢查目前節點。

例如，即使父節點具有屬性，子節點也會新增到翻譯作業中 `draftOnly` 設為true可標幟草稿內容。 此處 `isDeep` 就會開始使用，並檢查父節點是否具備屬性 `draftOnly` 為true並排除這些子節點。

在編輯器中，您可以核取/取消核取 **深入** 在 **篩選器** 標籤。

![篩選規則](../assets/translation-rules-editor-filters.png)

以下是產生的XML範例，當 **深入** 未在UI中勾選：

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

### 繼承 {#inherit}

**`inherit`** 適用於屬性。 依預設，每個屬性都會被繼承，但如果您希望某個屬性不被子項繼承，則可以將此屬性標示為false，使其僅套用至該特定節點。

在UI中，您可以勾選/取消勾選 **繼承** 在 **屬性** 標籤。

### translate {#translate}

**`translate`** 僅用於指定是否翻譯屬性。

在UI中，您可以勾選/取消勾選 **Translate** 在 **屬性** 標籤。

### updatedestinationlanguage {#updatedestinationlanguage}

**`updateDestinationLanguage`** 用於沒有文字但有語言代碼的屬性，例如 `jcr:language`. 使用者不會翻譯文字，而是從來源到目的地的語言地區設定。 不會傳送此類屬性以供翻譯。

在UI中，您可以勾選/取消勾選 **Translate** 在 **屬性** 標籤修改此值，但針對語言程式碼為值的特定屬性。

協助釐清兩者之間的差異 `updateDestinationLanguage` 和 `translate`，以下是僅有兩個規則之內容的簡單範例：

![updateDestinationLanguage範例](../assets/translation-rules-updatedestinationlanguage.png)

xml中的結果將如下所示：

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## 手動編輯規則檔案 {#editing-the-rules-file-manually}

此 `translation_rules.xml` 與AEM一起安裝的檔案包含一組預設的翻譯規則。 您可以編輯檔案以支援翻譯專案的需求。 例如，您可以新增規則，以便翻譯自訂元件的內容。

如果您編輯 `translation_rules.xml` 檔案中，在內容封裝中保留備份復本。 重新安裝某些AEM套件可取代目前的 `translation_rules.xml` 檔案與原始檔案。 若要在此情況下還原您的規則，您可以安裝包含備份復本的套件。

>[!NOTE]
>
>建立內容封裝後，每次編輯檔案時都會重新建置封裝。

## 範例翻譯規則檔案 {#example-translation-rules-file}

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
