---
title: 識別要翻譯的內容
description: 瞭解翻譯規則如何識別需要翻譯的內容。
feature: Language Copy
role: Admin
exl-id: 24cc6aa6-5b3c-462b-a10a-8b25277229dc
solution: Experience Manager Sites
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1288'
ht-degree: 1%

---

# 識別要翻譯的內容 {#identifying-content-to-translate}

翻譯規則會針對翻譯專案中包含或排除的頁面、元件和資產，識別要翻譯的內容。 在翻譯頁面或資產時，AEM會擷取此內容，以便將其傳送至翻譯服務。

>[!TIP]
>
>如果不熟悉如何翻譯內容，請參閱[網站翻譯歷程](/help/journey-sites/translation/overview.md)，此歷程將引導您使用AEM強大的翻譯工具來翻譯您的AEM Sites內容，非常適合沒有AEM或翻譯經驗的人士。

## 內容片段和翻譯規則 {#content-fragments}

只有在[翻譯整合架構組態層級](integration-framework.md#assets-configuration-properties)尚未啟用&#x200B;**啟用翻譯的內容模型欄位**&#x200B;選項時，本檔案描述的翻譯規則才會套用至內容片段。

如果&#x200B;**啟用翻譯的內容模型欄位**&#x200B;選項作用中，AEM將會使用[內容片段模型](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#properties)上的&#x200B;**可翻譯**&#x200B;欄位來決定是否要翻譯該欄位並相應地自動建立翻譯規則。 此選項會取代您可能已建立的任何翻譯規則，而且不需要介入或額外的步驟。

如果要使用翻譯規則來翻譯您的內容片段，必須停用翻譯整合框架設定上的&#x200B;**啟用翻譯的內容模型欄位**&#x200B;選項，而且您必須依照下列步驟建立規則。

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

例如，您可以建立規則來轉譯作者新增至您頁面上所有文字元件的內容。 此規則可以識別`core/wcm/components/text/v2/text`元件的`/content`節點和`text`屬性。

已新增一個[主控台](#translation-rules-ui)來設定翻譯規則。 UI中的定義將為您填入檔案。

如需AEM內容翻譯功能的概述，請參閱[翻譯多語言網站的內容](overview.md)。

>[!NOTE]
>
>AEM支援資源型別和參考屬性之間的一對一對應，以便翻譯頁面上的參考內容。

## 頁面、元件和Assets的規則語法 {#rule-syntax-for-pages-components-and-assets}

規則是`node`元素，包含一或多個子`property`元素以及零個或多個子`node`元素：

```xml
<node path="content path">
          <property name="property name" [translate="false"]/>
          <node resourceType="component path" >
               <property name="property name" [translate="false"]/>
          </node>
</node>
```

這些`node`元素中的每一個都具有下列特性：

* `path`屬性包含套用規則之分支的根節點的路徑。
* 子項`property`元素為所有資源型別識別要翻譯的節點屬性：
   * `name`屬性包含屬性名稱。
   * 如果屬性未轉譯，則選用的`translate`屬性等於`false`。 預設值為`true`。 覆寫先前的規則時，此屬性相當實用。
* 子項`node`元素會識別特定資源型別要翻譯的節點屬性：
   * `resourceType`屬性包含解析為實作資源型別的元件的路徑。
   * 子項`property`元素識別要翻譯的節點屬性。 以與節點規則的子`property`元素相同的方式使用此節點。

下列範例規則會為`/content`節點下的所有頁面轉譯所有`text`屬性的內容。 此規則適用於任何將內容儲存在`text`屬性中的元件，例如文字元件。

```xml
<node path="/content">
          <property name="text"/>
</node>
```

下列範例會轉譯所有`text`屬性的內容，也會轉譯影像元件的其他屬性。 如果其他元件具有同名屬性，則規則不適用於它們。

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

## 從頁面擷取Assets的規則語法  {#rule-syntax-for-extracting-assets-from-pages}

使用下列規則語法來包含內嵌在元件中或從元件參照的資產：

```xml
<assetNode resourceType="path to component" assetReferenceAttribute="property that stores asset"/>
```

每個`assetNode`元素都有下列特性：

* 一個`resourceType`屬性，代表解析為元件的路徑
* 一個`assetReferenceAttribute`屬性，代表儲存資產二進位檔（用於內嵌資產）的屬性名稱或參考資產的路徑

下列範例會從影像元件中擷取影像：

```xml
<assetNode resourceType="core/wcm/components/image/v2/image" assetReferenceAttribute="fileReference"/>
```

## 覆寫規則 {#overriding-rules}

`translation_rules.xml`檔案包含具有數個子項`node`專案的`nodelist`專案。 AEM會從上到下讀取節點清單。 如果有多個規則鎖定同一個節點，系統會使用檔案中較低位置的規則。 例如，下列規則會翻譯`text`屬性中的所有內容，但頁面的`/content/mysite/en`分支除外：

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

您可以使用`filter`元素來篩選具有特定屬性的節點。

例如，下列規則會翻譯`text`屬性中的所有內容，但屬性`draft`設定為`true`的節點除外。

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

1. 導覽至&#x200B;**工具**，然後導覽至&#x200B;**一般**。

1. 選取「**翻譯設定**」。

在翻譯規則UI中，您可以：

1. **新增內容**，讓您新增路徑。

   ![新增翻譯內容](../assets/add-translation-context.png)

1. 使用路徑瀏覽器選取必要的內容，並選取&#x200B;**確認**&#x200B;按鈕以儲存。

   ![選取內容](../assets/select-context.png)

1. 接著您必須選取內容，然後按一下[編輯]。**** 如此將可開啟翻譯規則編輯器。

   ![翻譯規則編輯器](../assets/translation-rules-editor.png)

您可以透過UI變更四個屬性：

* `isDeep`
* `inherit`
* `translate`
* `updateDestinationLanguage`

### isDeep {#isdeep}

**`isDeep`**&#x200B;適用於節點篩選器，預設為true。 它會檢查節點（或其上階）是否在篩選器中包含具有指定屬性值的屬性。 若為false，則僅檢查目前節點。

例如，即使父節點將屬性`draftOnly`設定為true以標幟草稿內容，子節點也會新增至翻譯工作。 此時`isDeep`就會發揮作用，並檢查父節點是否已將屬性`draftOnly`設為true並排除這些子節點。

在編輯器中，您可以在&#x200B;**篩選器**&#x200B;索引標籤中核取/取消核取&#x200B;**Is Deep**。

![篩選規則](../assets/translation-rules-editor-filters.png)

以下是在UI中取消勾選&#x200B;**Is Deep**&#x200B;時產生的XML範例：

```xml
 <filter>
    <node containsProperty="draftOnly" isDeep="false" propertyValue="true"/>
</filter>
```

### 繼承 {#inherit}

**`inherit`**&#x200B;適用於屬性。 依預設，每個屬性都會被繼承，但如果您希望某個屬性不被子項繼承，則可以將此屬性標示為false，使其僅套用至該特定節點。

在UI中，您可以在&#x200B;**屬性**&#x200B;索引標籤中核取/取消核取&#x200B;**繼承**。

### translate {#translate}

**`translate`**&#x200B;僅用於指定是否翻譯屬性。

在UI中，您可以在&#x200B;**屬性**&#x200B;索引標籤中勾選/取消勾選&#x200B;**Translate**。

### updatedestinationlanguage {#updatedestinationlanguage}

**`updateDestinationLanguage`**&#x200B;用於沒有文字但有語言代碼的屬性，例如`jcr:language`。 使用者不會翻譯文字，而是從來源到目的地的語言地區設定。 不會傳送此類屬性以供翻譯。

在UI中，您可以在&#x200B;**屬性**&#x200B;索引標籤中勾選/取消勾選&#x200B;**Translate**&#x200B;來修改此值，但針對將語言程式碼作為值的特定屬性。

為協助釐清`updateDestinationLanguage`與`translate`之間的差異，以下提供僅有兩個規則之內容的簡單範例：

![updateDestinationLanguage範例](../assets/translation-rules-updatedestinationlanguage.png)

xml中的結果將如下所示：

```xml
<property inherit="true" name="text" translate="true" updateDestinationLanguage="false"/>
<property inherit="true" name="jcr:language" translate="false" updateDestinationLanguage="true"/>
```

## 手動編輯規則檔案 {#editing-the-rules-file-manually}

與AEM一起安裝的`translation_rules.xml`檔案包含一組預設的翻譯規則。 您可以編輯檔案以支援翻譯專案的需求。 例如，您可以新增規則，以便翻譯自訂元件的內容。

如果您編輯`translation_rules.xml`檔案，請在內容封裝中保留備份復本。 重新安裝某些AEM套件可將目前的`translation_rules.xml`檔案取代為原始檔案。 若要在此情況下還原您的規則，您可以安裝包含備份復本的套件。

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
