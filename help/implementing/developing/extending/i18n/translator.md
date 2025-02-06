---
title: 國際化使用者介面字串
description: AEM提供了一個主控台，用於管理元件UI中使用的各種文字翻譯。
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 14a6516872f842d099b902b9f633b1d6f984266d
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# 使用Translator管理字典{#using-translator-to-manage-dictionaries}

AEM提供了一個主控台，用於管理元件UI中使用的各種文字翻譯。 此主控台位於：

`https://<hostname>:<port-number>/libs/cq/i18n/gui/translator.html`

使用翻譯工具來管理英文字串及其翻譯。 字典是在存放庫中建立的，例如，`/apps/myproject/i18n`。

您管理的翻譯工具與字典用於以不同語言呈現元件UI。 若要翻譯頁面，請參閱[翻譯多語言網站的內容](/help/sites-cloud/administering/translation/overview.md)。

## 建立字典 {#creating-a-dictionary}

開發人員可以在AEM中建立i18n字典，以管理本地化的元件字串。 字典通常是`/apps`中元件程式碼的一部分。 以下是來自AEM WKND程式碼的範例，此程式碼有一個用於所有WKND元件的索引鍵/值組。

```
{
  "&copy; {0} WKND Site Site. All rights reserved." : "&copy; {0} WKND Site Site. Tous droits réservés."
}
```

開發人員可以新增根節點(`sling:Folder`)來建立其他字典，供新字典存放元件字串的語言定義。

```shell
/apps/myProject/i18n [sling:Folder]
    - de.json [nt:file] [mix:language]
        + jcr:language = de
    - fr.json [nt:file] [mix:language]
        + jcr:language = fr
```

>[!NOTE]
>
>這是[Sling i18n模組](https://sling.apache.org/site/internationalization-support.html)的結構。

在AEM GitHub存放庫中建立字典後，可透過AEM [CI/CD管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)部署。

## 字典位置 {#dictionary-locations}

開發人員可以在`/apps`或`/content/cq:i18n`中建立來源語言字典。 從AEM原型範常式式碼開始，初始字典通常位於`/apps`路徑中。 如果目標是要將對應的字典語言副本也儲存在`/apps`中，則開發人員必須在元件程式碼中手動建立和維護這些語言副本。

或者，i18n字典的新AEM執行階段翻譯程式將在`/content/cq:i18n/<projectName>`中建立翻譯字典，無論來源字典是否儲存在`/apps`或`/content`中。

應該使用下列條件來決定尋找i18n字典、來源和語言副本的位置：

* `/apps`
   * 具有元件字串轉譯、遵循AEM原型和WKND範常式式碼的字典預設位置
   * 最高演算順序，依Sling （[資源套件搜尋階層](https://sling.apache.org/documentation/bundles/internationalization-support-i18n.html#resourcebundle-hierarchies)）
   * 但字典的執行階段編輯或翻譯無法進行，因為`/apps`在AEM as a Cloud Service環境中不可變動

* `/content/cq:i18n`
   * i18n字典的替代位置，如果
      * 需要字典的執行階段翻譯
      * 需要在執行階段編輯字典的功能
   * 執行階段字典翻譯將建立語言副本的預設位置。

因為`/apps`在Sling轉譯順序中一律取代`/content`，請務必記住，`/apps`和`/content/cq:i18n`中不能同時存在索引鍵/值配對相同的字典，因為`/content/cq:i18n`中的字典永遠不會用於轉譯。 如果`/apps`中已存在字典語言副本（亦即翻譯目的地），且目標為使其可在AEM as a Cloud Service中於執行階段翻譯，則`/apps`中的原始字典語言副本必須移至`/content/cq:i18n`，或在`/apps`中刪除並透過翻譯來源字典在`/content/cq:i18n`中自動重新建立。 此翻譯程式會自動在`/content/cq:i18n`中建立語言副本。

## 自動建立字典 {#automatic-creation}

對於包含AEM核心元件的AEM頁面和體驗片段，新的字典翻譯程式也會掃描這些頁面或體驗片段，以尋找應翻譯的元件和元件字串。 然後，系統將在`/content/cq:i18n`中自動建立對應的新字典語言副本。 這不適用於內容片段，因為這些是純結構化的內容，沒有使用AEM核心元件。

## 匯出字典 {#exporting-a-dictionary}

雖然在AEM as a Cloud Service中無法對`/apps`或`/libs`位置中的i18n字典執行階段轉譯，因為這些位置不可變動，但您仍可在執行階段匯出這些字典，以便在AEM外部進行非同步轉譯。

若要將字典的來源語言字串匯出至XLIFF檔案：

1. 開啟翻譯工具`http://<host>:<port>/libs/cq/i18n/gui/translator.html`

   >[!NOTE]
   >
   >工具只能透過此URL使用，無法從AEM產品UI存取。

1. 使用字典下拉式選單來選取要匯出的字典。
1. 按一下「匯出XLIFF翻譯」，然後按一下「匯出完整的`<locale>` xliff」。

## 匯入字典 {#importing-a-dictionary}

將XLIFF檔案匯入字典以填入字典內容：

1. 開啟翻譯工具`http://<host>:<port>/libs/cq/i18n/gui/translator.html`
1. 按一下匯入，然後按一下XLIFF翻譯。
1. 選取要匯入的檔案，然後按一下「確定」。
