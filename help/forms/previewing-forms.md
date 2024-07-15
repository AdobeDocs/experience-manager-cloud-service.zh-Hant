---
title: 如何預覽最適化表單？
description: 使用者可在發佈或啟用表單前預覽表單，以確保表單符合預期。 預覽選項可能因支援的表單型別而異。
topic-tags: author
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 72235277-6c34-4341-9a10-02afa753e7f5
source-git-commit: 05548d56d791584781606b02839c5602b4469f7b
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 4%

---

# 預覽表單 {#previewing-a-form}

## 概觀 {#overview}

在[!DNL AEM Forms]中，您可以預覽存放庫中呈現的表單和檔案。 預覽有助於瞭解表單發佈給使用者時的確切外觀和行為。

預覽表單時，表單會以互動式介面呈現，使用者可以使用資料填寫表單。 預覽檔案時，會以非互動模式呈現，使用者只能檢視檔案。 對於表單，還有一個自訂預覽選項可供使用。 使用此選項，您可以使用XML檔案中的資料來預覽表單。 資料會填滿正在預覽之表單的部分欄位或所有欄位。

下表列出不同支援表單型別可用的預覽選項：

<table>
 <tbody>
  <tr>
   <td><strong>資產型別</strong><br /> </td>
   <td><strong>可用的預覽選項</strong><br /> </td>
  </tr>
  <!--<tr>
   <td>Document</td>
   <td>PDF preview</td>
  </tr>-->
  <tr>
   <td>PDF表單</td>
   <td>PDF預覽和預覽資料<br /> </td>
  </tr>
  <tr>
   <td>最適化表單</td>
   <td>包含資料的HTML預覽和HTML預覽</td>
  </tr>
  <!--<tr>
   <td>Form Template</td>
   <td>PDF preview, PDF preview with Data, HTML preview, HTML preview with Data<br /> </td>
  </tr>-->
 </tbody>
</table>

## 預覽表單 {#previewing-a-form-1}

1. 選取您要預覽的資產，然後按一下動作工具列中的[預覽![aem6forms_preview](assets/aem6forms_preview.png)]。

   >[!NOTE]
   >
   >若要選取資產，請從預設的「卡片」檢視切換至「清單」檢視。 按一下![aem6forms_viewlist](assets/aem6forms_viewlist.png)或![aem6forms_viewcard](assets/aem6forms_viewcard.png)以切換檢視。

1. 按一下「預覽」會列出適用於所選資產型別的可能預覽選項。 按一下所需的選項，在新索引標籤中呈現選取的資產。

   您的選項有：

   * 以HTML預覽
   * 以資料預覽
     <!--* Preview as PDF (available for form templates)-->

## 以資料預覽 {#preview-with-data}

選取&#x200B;**使用資料預覽**&#x200B;時，您可以看到表單在輸入真實資料時的外觀。 使用資料預覽選項可讓您上傳包含範例使用者資料的XML。 範例使用者資料可用來以您選擇的格式填入預覽表單。

1. 選取資產，按一下「預覽![aem6forms_preview](assets/aem6forms_preview.png)」，然後選取「**使用資料預覽**」。
1. 在「預覽表單」對話方塊中，以XML檔案形式提供FormData。 按一下「預覽」，使用合併的來自XML的資料來呈現表單。
