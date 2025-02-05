---
title: 管理分類資料
description: 了解如何管理分類資料，以便將標記與使用 Edge Delivery Services 網站的 AEM 結合運用。
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: 017982e4-a4c8-4097-8751-9619cc4639d0
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 65%

---


# 管理分類資料 {#managing-taxonomy-data}

了解如何管理分類資料，以便將標記與使用 Edge Delivery Services 網站的 AEM 結合運用。

## 簡介 {#introduction}

標記是一項重要功能，可協助貴組織和管理頁面。AEM 中的[標記主控台](/help/sites-cloud/administering/tags.md#tagging-console)可讓您建立豐富的標記分類來組織頁面。

這些標記不僅對您和您的作者在組織內容方面很實用，對您的讀者來說也很實用。標記及其分類可以在頁面的元件中使用，幫助您的讀者導覽您的內容。

通用編輯器僅適用於您標記的 ID。透過為內容建立分類頁面，您可以使用所有語言將這些標記的說明公開到通用編輯器，使其能夠在轉譯內容時使用該資訊。

## 建立分類頁面 {#creating}

分類法的建立方式與AEM](/help/sites-cloud/authoring/sites-console/creating-pages.md)中的[任何其他頁面相同。

1. 導覽至&#x200B;[**網站**&#x200B;主控台](/help/sites-cloud/authoring/sites-console/introduction.md)。

1. 選取您想要建立分類的位置。

1. 點選或按一下「**建立** -> **頁面**」。

   ![建立頁面](assets/taxonomy/create-page.png)

1. 在「**建立頁面**」精靈的「**範本**」索引標籤上，選取「**分類**」範本，然後點選或按一下「**下一步**」。

   ![分類範本](assets/taxonomy/taxonomy-template.png)

1. 在「**建立頁面**」精靈的「**屬性**」索引標籤上，提供有意義的頁面&#x200B;**標題**，然後在「**標記**」欄位中，[使用標記選擇器](/help/sites-cloud/authoring/sites-console/tags.md)選取您希望包含在分類中的標記或命名空間。

   ![分類屬性](assets/taxonomy/create-page-wizard-properties.png)

1. 點選或按一下「**建立**」。

分類頁面建立完成。在&#x200B;**成功**&#x200B;對話方塊中，您可以點選或按一下&#x200B;**完成**&#x200B;對話方塊以關閉訊息，或是&#x200B;**開啟**&#x200B;以在[頁面編輯器](/help/sites-cloud/authoring/page-editor/introduction.md)中編輯頁面。

記下分類頁面的結果頁面名稱，以便在以下步驟中使用。

## 編輯分類頁面 {#editing}

您會像編輯 AEM 中任何其他頁面一樣的方式來開始編輯分類頁面。

1. 導覽至&#x200B;[**網站**&#x200B;主控台](/help/sites-cloud/authoring/sites-console/introduction.md)。

1. 選取您要編輯的分類。

1. 點選或按一下動作列中的「**編輯**」。

1. 此時會開啟頁面編輯器，顯示出分類。

   * 分類頁面在頁面編輯器中是唯讀的。

   ![編輯分類](assets/taxonomy/edit-page.png)

1. 點選或按一下工具列中的「**頁面資訊**」圖示，並選取「**開啟屬性**」。

   ![開啟屬性](assets/taxonomy/open-properties.png)

1. 在「**頁面屬性**」視窗中，您可以更新頁面的名稱，並使用標記選擇器來更新分類中包含的標記和命名空間。

   ![編輯頁面屬性](assets/taxonomy/edit-properties.png)

1. 點選或按一下「**儲存並關閉**」。

頁面編輯器中顯示的頁面是唯讀的，因為分類內容是根據選定的標記和命名空間自動產生。它們就像篩選器一般，會自動產生分類內容。因此沒有理由直接在編輯器中編輯頁面。

當您更新根本的標記和命名空間時，AEM 會自動更新分類頁面的內容。不過，您必須在任何變更後[重新發佈分類](#publishing)，才能讓使用者可以使用這些變更。

## 更新 paths.json 以發佈分類 {#paths-json}

就像在[管理和發佈Edge Delivery Services網站](/help/edge/wysiwyg-authoring/tabular-data.md)的表格式資料時，您需要更新專案的`paths.json`檔案，以允許發佈分類資料。

1. 在 GitHub 中開啟專案的根目錄。

1. 點選或按一下 `paths.json` 檔案以開啟其詳細資訊，然後按一下「**編輯**」圖示。

   ![paths.json 檔案](assets/taxonomy/paths-json.png)

1. 新增一行以將新分類頁面對應到 `.json` 資源。

   ```json
   {
     "mappings": [
      "/content/<site-name>/:/",
      "/content/<site-name>/<taxonomy-page-name>:/<taxonomy-json-name>.json"
     ]
   }
   ```

   * `<taxonomy-page-name>`必須符合您建立的[分類頁面](#creating)的名稱。
   * `<taxonomy-json-name>` 可以是您選擇的任何有效名稱。

1. 按一下「**提交變更...**」，將變更儲存到 `main`。

   * 根據您的流程提交 `main` 或建立提取請求。

每個分類頁面只需執行一次此程序。完成後，您就可以發佈分類了。

>[!TIP]
>
>如需有關路徑對應的詳細資訊，請參閱檔案[Edge Delivery Services的路徑對應](/help/edge/wysiwyg-authoring/path-mapping.md)。

## 發佈分類 {#publishing}

在發佈之前，通用編輯器或您的使用者皆無法使用該分類。

[使用工具列](/help/sites-cloud/authoring/sites-console/publishing-pages.md)中的&#x200B;**快速Publish**&#x200B;或&#x200B;**管理出版物**&#x200B;圖示，像發佈其他任何頁面一樣發佈分類頁面。

每次您執行以下操作時，都必須重新發佈分類頁面：

* 編輯分類頁面。
* 編輯或新增至分類頁面中包含的標記和命名空間。

如果您建立新的分類頁面，您必須先將對應新增至專案](#paths-json)中的`paths.json`檔案[。

## 存取分類資訊 {#accessing}

一旦您的分類發佈，通用編輯器就可以運用其資訊，您的使用者也能夠看到這些資訊。

您可以透過以下網址，以 JSON 資料形式存取分類。

`https://<branch>--<repository>--<owner>.aem.page/<taxonomy-json-name>.json`

使用您在[將分類對應至專案](#paths-json)中的`paths.json`檔案時所定義的`<taxonomy-json-name>`。 如以下範例所示，分類資料會以JSON資料傳回。

```json
{
  "total": 3,
  "offset": 0,
  "limit": 3,
  "data": [
    {
      "tag": "default:",
      "title": "Standard Tags"
    },
    {
      "tag": "do-not-translate",
      "title": "Do Not Translate"
    },
    {
      "tag": "translate",
      "title": "Translate"
    }
  ],
  "columns": [
    "tag",
    "title"
  ],
  ":type": "sheet"
}
```

您更新分類並重新發佈時，此 JSON 資料會自動更新。您的應用程式可以透過程式設計方式為您的使用者存取此資訊。

[如果您維護多種語言的標籤](/help/sites-cloud/administering/tags.md#managing-tags-in-different-languages)，您可以將ISO2語言代碼作為`sheet=`引數的值傳入，以存取這些語言。

## 公開其他標籤屬性 {#additional-properties}

依預設，您的分類將包含`tag`和`title`值，如上一個範例](#accessing)中的[所示。 您可以設定分類法以公開其他標籤屬性。 在此範例中，我們將公開標籤說明。

1. 使用網站主控台選取您建立的分類法。
1. 點選或按一下工具列中的&#x200B;**屬性**&#x200B;圖示。
1. 在&#x200B;**其他屬性**&#x200B;區段中，點選或按一下&#x200B;**新增**&#x200B;以新增欄位。
1. 在新欄位中輸入要公開的JRC屬性名稱。 在此情況下，請輸入`jcr:description`作為標籤描述。
1. 點選或按一下「**儲存並關閉**」。
1. 在分類法仍被選取的情況下，點選或按一下工具列中的「快速Publish **」。**

現在[當您存取分類法](#accessing)時，標籤描述（或您選擇公開的任何屬性）會包含在JSON中。

```json
{
  "total": 3,
  "offset": 0,
  "limit": 3,
  "data": [
    {
      "tag": "default:",
      "title": "Standard Tags",
      "jcr:description": "These are the standard tags"
    },
    {
      "tag": "do-not-translate",
      "title": "Do Not Translate",
      "jcr:description": "Tag to mark pages that should not be translated"
    },
    {
      "tag": "translate",
      "title": "Translate",
      "jcr:description": "Tag to mark pages that should be translated"
    }
  ],
  "columns": [
    "tag",
    "title",
    "jcr:description"
  ],
  ":type": "sheet"
}
```
