---
title: 建立 Headless 內容
description: 使用您先前建立的內容片段模式來建立可用來編寫頁面的內容，或作為 Headless 內容的依據。
hidefromtoc: true
index: false
exl-id: d74cf5fb-4c4a-4363-a500-6e2ef6811e60
source-git-commit: ac94981e477e1fe8b883460ed9be009b4c1c088d
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 100%

---


# 建立 Headless 內容 {#create-content}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_create_content"
>title="建立新內容"
>abstract="使用您在上一個單元中建立的模式，您將瞭解如何建立可用於編寫頁面或作為 Headless 內容基礎的內容。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_create_content_guide"
>title="啟動內容片段主控台"
>abstract="建立可在您的應用程式和網站上無縫執行的高品質一致內容，能帶來出色的客戶體驗。本單元將引導您建立您的第一個內容片段，以說明如何實際操作。<br><br>點選下方按鈕，在新標籤中啟動此單元，然後按照本指南進行操作。"

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_admin_content_fragments_create_content_guide_footer"
>title="做得好！在本單元中，您已瞭解如何根據先前建立的模式建立內容片段。您現在瞭解內容團隊能如何建立和管理應用程式和網站的內容，不受開發週期的限制。"
>abstract=""

## 建立內容片段 {#create-fragment}

內容片段代表您的 Headless 內容，且以預先定義的結構為基礎，稱為內容片段模式。您已經在前面的單元建立模型。

在本單元中，您將使用內容片段主控台根據該模型建立新的內容片段。將內容片段主控台視為您的 Headless 內容資料庫。使用該控制台來建立新的內容片段並管理現有片段。

1. 在主控台右上方，點選或按一下&#x200B;**建立**&#x200B;按鈕。

1. **新內容片段**&#x200B;對話框隨即開啟，您可以在此處開始建立新的內容片段。**位置**&#x200B;會自動填入新內容的儲存位置。

1. 在「**內容片段模型**」下拉式清單中，選取您先前建立的「**冒險**」內容片段模型。

1. 新增 `Tuscany` 做為內容片段的描述性&#x200B;**標題**。這是為了在主控台中識別您的片段。

1. 點選或按一下&#x200B;**建立並開啟**。

![正在建立新內容片段](assets/do-not-localize/create-content.png)

>[!TIP]
>
>根據您的瀏覽器設定，新的瀏覽器索引標籤可能會被快顯視窗封鎖程式禁止。如果您的新片段在按一下「**建立並開啟**」後未開啟，請檢查您的瀏覽器設定。

## 新增內容至您的內容片段 {#add-content}

儲存並開啟新內容片段後，內容片段編輯器將在新標籤上開啟。您可以在此處新增新片段的內容。

1. 內容片段編輯器會顯示您在所選模式中定義的欄位。 您可以在此處向每個欄位新增內容，以完成您的內容片段。 您的進度會自動儲存。

1. 輸入 `Tuscan Adventure`，為您的片段提供&#x200B;**標題**。

1. 貼上以下文字，為您的片段提供&#x200B;**描述**。

   ```text
   Visiting Tuscany on a bicycle is about experiencing the old world charm of Italy on your own terms. Your efforts on the climbs of Italy's rolling hills during this tour will be rewarded with sunny Mediterranean landscapes and unmatched Italian hospitality.  Tuscany’s natural wonders have always been a well of inspiration for arts and culture. Find out why as you explore the Italian countryside and coastline on bicycle.
   ```

1. 輸入 `$700`，為您的片段提供&#x200B;**價格**。

1. 在「**影像**」欄位中，點選或按一下「**新增資產**」，提供代表旅行的&#x200B;**影像**。

1. 在資產快顯視窗中，點選或按一下「**瀏覽資產**」，從資產庫中選取現有資產。

   ![新增資產](assets/do-not-localize/add-asset.png)

1. 「**選擇資產**」對話框隨即開啟。使用左側面板中的樹狀導覽器，導覽到「**所有資產** > **aem-demo-assets** > **en** > **adventures** > **cycling-tuscany**」。

1. **cycling-tuscany** 資料夾的內容顯示在右側。選取影像 `ADOBESTOCK_141786166.JPEG`。

1. 點選或按一下「**選取**」。

   ![選取資產](assets/do-not-localize/select-asset.png)

1. 所選影像顯示在內容片段中。編輯器會自動儲存這些變更。

1. 新增完內容後，點選或按一下編輯器右上角的「**發佈**」按鈕。這可讓您的內容片段供外部應用程式使用。然後從下拉式清單中選取「**立即**」。您還可以安排在以後發佈。

   ![發佈內容](assets/do-not-localize/publish.png)

1. **發佈內容片段**&#x200B;對話框隨即出現。AEM 會自動執行參考檢查，以確保為您的內容片段發佈所有必要的資源。 在這種情況下，您還需要發佈您建立的模式。 點選或按一下&#x200B;**發佈**。

   ![發布和引用檢查](assets/do-not-localize/publish-confirm.png)

1. 這項內容發佈會在橫幅中確認。

您的內容已發佈，並準備好作為內容片段傳送到您的應用程式或網站。
