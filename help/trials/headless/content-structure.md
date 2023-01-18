---
title: 為您的應用程式建立內容結構
description: 了解如何使用 AEM 的內容片段模式來建立結構，使其成為所有 Headless 內容的基礎。
hidefromtoc: true
index: false
exl-id: ace9b9f3-8bc6-4a36-a51c-ff60cdd339ce
source-git-commit: bcab02cbd84955ecdc239d4166ae38e5f79b3264
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 38%

---


# 為您的應用程式建立內容結構 {#content-structure}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview"
>title="為您的應用程式建立內容結構"
>abstract="依照這系列互動式指南，您將學習如何建立結構（稱為內容片段模型），此結構可作為無頭式內容的基礎。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide"
>title="啟動模型控制台"
>abstract="讓我們來探索如何為Adobe Experience Manager as a Cloud Service中的內容建立可重複使用的架構（稱為內容片段模型）。 觀看影片以了解這是重要步驟的原因。 <br><br>按一下下方的按鈕，然後依照本指南操作，在新索引標籤中啟動此模組。"
>additional-url="https://video.tv.adobe.com/v/3413261" text="內容結構介紹影片"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_overview_guide_footer"
>title="恭喜！您學習了如何建立內容片段模型以呈現無頭資料的結構，並採取第一步，以縮放和標準的方式傳送全頻道內容。"
>abstract=""

## 建立一個模式 {#create-model}

按一下 **啟動模型控制台** 按鈕會在新索引標籤中開啟內容片段模型主控台。

![內容片段模式控制台](assets/content-structure/content-fragment-model-console.png)

將內容片段模型主控台想像成您的模型程式庫，您可在其中建立新模型並管理現有模型。 您的控制台一開始是空的，所以我們來建立一個新模式！

1. 在內容片段控制台的螢幕右上方，點選「**建立**」按鈕，即可開始建立一個內容片段模式。

1. 「建立模型」嚮導將啟動，該嚮導將引導您。

   ![內容片段模式精靈](assets/content-structure/model-wizard.png)

   提供必填資訊。

   * **模型標題**  — 這是模型的簡要描述，通常指明模型的目的。
   * **啟用模型**  — 預設會核取此選項，且必須勾選此選項才能根據此模型建立內容片段。

1. 填入必填欄位後，按一下 **建立** ，以建立模型。

1. 「**成功** 」對話框會確認模式已建立。

   ![建立新內容片段模式的成功對話框](assets/content-structure/success.png)

## 新增欄位至模式 {#configure-model}

使用模型之前，需要定義其資料的結構。

1. 按一下 **開啟** 在 **成功** 對話方塊，以在「內容片段模型編輯器」中開啟新模型，您可在此定義其欄位。

1. 從拖曳欄位 **資料類型** 面板，並將其拖放至內容片段模型。

   ![新增資料類型](assets/content-structure/drop-fields.png)

1. 放好資料類型後，「**資料類型**」欄會自動變更為「**屬性**」標籤，您可以在其中定義您剛剛放好的詳細資料類型。

   ![資料欄位的「屬性」標籤](assets/content-structure/data-type-properties.png)

1. 新增內容片段模式所需的所有欄位後，在視窗右上方按一下「**儲存**」。

模型會儲存，您會返回「內容片段模型控制台」，視需要可在其中新增更多模型。

![模組完成](assets/content-structure/content-fragment-model-console-populated.png)
