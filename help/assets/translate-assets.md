---
title: 以多種語言建立和管理數位資產
description: 了解如何自動將資產（包括二進位檔、中繼資料和標籤）轉譯為多種語言的工作流程。
contentOwner: AG
feature: 資產管理，翻譯
role: Admin,User
exl-id: 98df1412-a957-48a3-81c2-7dfe1d5e6d31
source-git-commit: 00bea8b6a32bab358dae6a8c30aa807cf4586d84
workflow-type: tm+mt
source-wordcount: '2590'
ht-degree: 23%

---

# 多語言資產 {#multilingual-assets}

多語言資產是指具有多種語言的二進位檔、中繼資料和標籤的資產。 資產的二進位檔、中繼資料和標籤通常以一種語言存在，然後轉譯為其他語言，以用於多語言專案。 Adobe Experience Manager(AEM)Assets可讓您自動處理資產的翻譯工作流程（包括二進位檔、中繼資料和標籤），以產生其他語言的資產，以便用於多語言專案。

為了自動化翻譯工作流程，您將翻譯服務提供者與AEM整合，並建立專案，將資產翻譯成多種語言。 AEM支援人工和機器翻譯工作流程。

人類翻譯：翻譯的資產會傳回並匯入AEM。 當您的翻譯提供者與AEM整合時，資產會自動在AEM和翻譯提供者之間傳送。

機器翻譯：機器翻譯服務會立即轉譯資產的中繼資料和標籤。

<!--
We have multiple articles around translation of assets. For now, dumping all content in this article to remove others and create only ONE UBER article.

https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/translation-projects.html
https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/preparing-assets-for-translation.html
[Apply translation cloud services to folders](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/transition-cloud-services.html)

One of these articles is a copy of [Preparing Content for Translation](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/tc-prep.html

-->

<!-- 
Translating assets includes the following:

1. [Connecting AEM with the translation service provider](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [Creating translation integration framework configurations](/help/sites-administering/tc-tic.md)
1. [Preparing assets for translation](prepare-assets-for-translation.md)
1. [Applying translation cloud services to folders](transition-cloud-services.md)
1. [Create translation projects](translation-projects.md)

If your translation service provider does not provide a connector to integrate with AEM, use an [alternative process](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

Also see, [Creating translation projects for content fragments](creating-translation-projects-for-content-fragments.md).

-->

## 準備翻譯資產 {#prepare-assets-for-translation}

多語言資產是指具有多種語言的二進位檔、中繼資料和標籤的資產。 資產的二進位檔、中繼資料和標籤通常以一種語言存在，然後轉譯為其他語言，以用於多語言專案。

在Adobe Experience Manager(AEM)資產中，多語言資產會包含在資料夾中，每個資料夾都包含不同語言的資產。

每個語言資料夾都稱為語言副本。 語言副本的根資料夾（稱為語言根）標識語言副本中內容的語言。 例如，`/content/dam/it`是義大利語語言副本的義大利語根。 語言副本必須使用[正確配置的語言根](#create-a-language-root)，以便在執行源資產翻譯時定位正確的語言。

您最初新增資產的語言副本是語言主要。 語言主要是翻譯成其他語言的源。 範例資料夾階層包含數種語言根：

```shell
/content
    /- dam
        |- en
        |- fr
        |- de
        |- es
        |- it
        |- ja
        |- zh
```

執行下列步驟準備翻譯資產：

1. 建立語言主要的語言根。 例如，範例資料夾階層中英文副本的語言根目錄為`/content/dam/en`。 確保根據[建立語言根](#create-a-language-root)中的資訊正確配置語言根。

1. 將資產新增至您的語言主要版本。
1. 建立您需要語言副本的每種目標語言的語言根。

### 建立語言根 {#create-a-language-root}

要建立語言根，請建立資料夾並使用ISO語言代碼作為Name屬性的值。 建立語言根後，您就可以在語言根的任何層級建立語言副本。

例如，範例階層的義大利語言副本的根頁面會以`it`作為Name屬性。 Name屬性會作為存放庫中資產節點的名稱，因此會決定資產的路徑。 (*&lt;server>:&lt;port>/assets.html/content/dam/it/*)

1. 在「資產」主控台中，按一下/點選「 **[!UICONTROL 建立]** 」，然後從 **[!UICONTROL 選單選擇「資料夾]** 」。
1. 在「名稱」欄位中，以`<language-code>`格式輸入國家/地區代碼。
1. 按一下或點選&#x200B;**[!UICONTROL 建立]**。 語言根目錄會在Assets主控台中建立。

### 查看語言根 {#view-language-roots}

觸控最佳化UI提供「參考」面板，顯示已在AEM Assets中建立的語言根清單。

1. 在Assets控制台中，選取您要建立語言副本的主要語言。
1. 按一下或點選GlobalNav表徵圖，然後選擇&#x200B;**[!UICONTROL References]**&#x200B;以開啟「Reference」窗格。
1. 在「參考」窗格中，按一下或點選「語言副本」****。 「語言復本」面板會顯示資產的語言復本。

### 建立新的翻譯專案 {#create-a-new-translation-project}

如果您使用此選項，要翻譯的資產會複製到您要翻譯之語言的語言根目錄。 系統會根據您選擇的選項，在「專案」主控台中為資產建立翻譯專案。 視設定而定，翻譯專案可以手動啟動，或在建立翻譯專案後立即自動執行。

1. 在「資產」UI中，選取您要建立語言副本的來源資料夾。
1. 開啟「參 **[!UICONTROL 考」窗格]** ，然後按一下「復本」下的「語言復本 **[!UICONTROL 」(Language Copies]****[!UICONTROL )]**。
1. 按一下/點選底部的「建立並翻譯」]**。**[!UICONTROL 
1. 從「目 **[!UICONTROL 標語言]** 」清單中，選取您要建立檔案夾結構的語言。
1. 從&#x200B;**[!UICONTROL 項目]**&#x200B;清單中，選擇&#x200B;**[!UICONTROL 建立新翻譯項目]**。
1. 在「專 **[!UICONTROL 案標題]** 」欄位中，輸入專案標題。
1. 按一下/點選&#x200B;**[!UICONTROL 「建立」]**。 來源資料夾中的資產會複製到您在步驟4中選取的地區設定的目標資料夾。
1. 若要導覽至資料夾，請選取語言副本，然後按一下「在資產中顯現」**[!UICONTROL 。]**
1. 導覽至「專案」主控台。 翻譯資料夾會複製到「專案」主控台。
1. 開啟資料夾以檢視翻譯專案。
1. 按一下/點選專案以開啟詳細資訊頁面。
1. 要查看翻譯作業的狀態，請按一下&#x200B;**[!UICONTROL 翻譯作業]**&#x200B;表徵圖底部的刪節號。<!-- For more details around job statuses, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. 在「資產」使用者介面中，開啟每個翻譯資產的「屬性」頁面，以檢視翻譯的中繼資料。

>[!NOTE]
>
>此功能可供資產和資料夾使用。 選取資產而非資料夾時，系統會複製資料夾的整個階層（直至語言根目錄），以建立資產的語言副本。

### 新增至現有的翻譯專案 {#add-to-existing-translation-project}

如果您使用此選項，則會在執行先前的翻譯工作流程後，針對您新增至來源資料夾的資產執行翻譯工作流程。 只會將新增的資產複製到目標資料夾中，該資料夾包含先前翻譯的資產。 在此情況下不會建立新的翻譯專案。

1. 在「資產」UI中，導覽至包含未翻譯資產的來源資料夾。
1. 選取您要轉換的資產，並開啟「參考」 **[!UICONTROL 窗格]**。「語 **[!UICONTROL 言副本]** 」部分顯示當前可用的翻譯副本數。
1. 按一下/點選「 **[!UICONTROL 復本」下的]** 「語言 **[!UICONTROL 復本」]**。將顯示可用翻譯副本的清單。
1. 按一下/點選底部的「建立並翻譯」]**。**[!UICONTROL 
1. 從「目 **[!UICONTROL 標語言]** 」清單中，選取您要建立檔案夾結構的語言。
1. 從「項 **[!UICONTROL 目]** 」清單中，選擇「 **[!UICONTROL 添加到現有翻譯項目」]** ，以在資料夾中運行翻譯工作流。
   >[!NOTE]
   >
   >如果選擇「**[!UICONTROL 添加到現有翻譯項目]**」選項，則只有在項目設定與現有項目的設定完全匹配時，您的翻譯項目才會添加到預先存在的項目。 否則，會建立新專案。
1. 從&#x200B;**[!UICONTROL 現有翻譯專案]**&#x200B;清單中，選取要新增翻譯資產的專案。
1. 按一下/點選「 **[!UICONTROL 建立]**」。要翻譯的資產會新增至目標資料夾。更新的資料夾會列在「語言復 **[!UICONTROL 本」區段下]** 。
1. 導覽至「專案」主控台，並開啟您新增至的現有翻譯專案。
1. 按一下/點選翻譯專案檢視專案詳細資訊頁面。
1. 按一下/點選&#x200B;**翻譯工作**&#x200B;圖磚底部的刪節號，以檢視翻譯工作流程中的資產。 翻譯工作清單也會顯示資產中繼資料和標籤的項目。 這些項目表示資產的中繼資料和標籤也會翻譯。

   >[!NOTE]
   >
   >* 如果您刪除標籤或中繼資料的項目，則不會為任何資產翻譯任何標籤或中繼資料。
   >* 如果您使用機器翻譯，資產二進位檔將不會翻譯。
   >* 如果您新增至翻譯工作的資產包含子資產，請選取子資產並移除這些子資產，以便翻譯繼續，不會有任何問題。


1. 若要開始資產的翻譯，請按一下/點選「翻譯工作&#x200B;]**」方塊上的箭頭，然後從清單中選取「**[!UICONTROL &#x200B;開始&#x200B;]**」。**[!UICONTROL &#x200B;訊息會通知翻譯工作開始。
1. 要查看翻譯作業的狀態，請按一下/點選&#x200B;**[!UICONTROL 翻譯作業]**&#x200B;表徵圖底部的省略號。<!-- For more details, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. 翻譯完成後，狀態會變更為「準備檢閱」。 導覽至「資產」UI，並開啟每個翻譯資產的「屬性」頁面以檢視翻譯的中繼資料。

### 更新語言副本 {#update-language-copies}

執行此工作流程以翻譯任何其他資產集，並將其納入特定地區的語言副本中。 在此情況下，翻譯的資產會新增至已包含先前翻譯資產的目標資料夾。 系統會根據選項的選擇，建立翻譯專案，或為新資產更新現有的翻譯專案。 「更新語言副本」工作流包含以下選項：

* 建立新的翻譯專案
* 新增至現有翻譯專案

### 新增至現有翻譯專案 {#add-to-existing-translation-project-1}

如果使用此選項，則資產集將添加到現有翻譯項目中，以更新所選地區的語言副本。

1. 從資產UI中，選取您新增資產資料夾的來源資料夾。
1. 開啟「參 **[!UICONTROL 考」窗格]**，然後按一下/點選「復本」下的「語言復本 ******** 」，以顯示語言復本清單。
1. 在「語言副本」之前選 **[!UICONTROL 取核取方塊]**，以選取所有語言副本。取消選擇與要翻譯的語言環境相對應的語言副本 (副本) 以外的其他副本。
1. 按一下/點選底部的「更新語言副本&#x200B;]**」。**[!UICONTROL 
1. 從&#x200B;**[!UICONTROL 項目]**&#x200B;清單中，選擇&#x200B;**[!UICONTROL 添加到現有翻譯項目]**。
1. 從&#x200B;**[!UICONTROL 現有翻譯專案]**&#x200B;清單中，選取要新增翻譯資產的專案。
1. 按一下/點選「 **[!UICONTROL 開始]**」。
1. 請參閱[添加到現有翻譯項目](#add-to-existing-translation-project)的步驟9-14以完成其餘步驟。

### 建立臨時語言副本 {#creating-temporary-language-copies}

當您執行翻譯工作流程以使用原始資產的編輯版本更新語言副本時，會保留現有語言副本，直到您核准翻譯的資產為止。 AEM Assets會將新翻譯的資產儲存在臨時位置，並在您明確核准資產後更新現有的語言副本。 如果您拒絕資產，語言副本將維持不變。

1. 按一下/點選「語言副本」下方的「來源根」檔案夾( **[!UICONTROL Language Copies]** )，然後按一下/點選「 **[!UICONTROL Reveal in Assets]** 」 (在資產中顯現) 以開啟「AEM Assets」(AEM Assets)中的檔案夾。
1. 從「資產」UI中，選取您已翻譯的資產，然後按一下/點選工具列中的&#x200B;**[!UICONTROL Edit]**&#x200B;圖示，以在編輯模式中開啟資產。
1. 編輯資產，然後儲存變更。
1. 執行[添加到現有翻譯項目](#add-to-existing-translation-project)過程的步驟2-14以更新語言副本。
1. 按一下/點選&#x200B;**[!UICONTROL 翻譯工作]**&#x200B;圖磚底部的刪節號。 從&#x200B;**[!UICONTROL 翻譯工作]**&#x200B;頁面中的資產清單中，您可以清楚查看儲存資產翻譯版本的臨時位置。
1. 選取&#x200B;**[!UICONTROL Title]**&#x200B;旁的核取方塊。
1. 在工具列中，按一下/點選「 **[!UICONTROL Accept Translation]** 」 (接受翻譯)，然後在對話方塊中按一下/點選「 **[!UICONTROL Accept]** 」 (接受)，以使用已編輯資產的翻譯版本覆寫目標資料夾中的翻譯資產。

   >[!NOTE]
   >
   >若要啟用翻譯工作流程以更新目標資產，請接受資產和中繼資料。

   按一下/點選&#x200B;**[!UICONTROL 拒絕翻譯]**&#x200B;以保留目標地區根中資產的原始翻譯版本，並拒絕編輯的版本。

1. 導覽至「資產」主控台，並開啟每個翻譯資產的「屬性」頁面，以檢視翻譯的中繼資料。

<!-- TBD: Possibly this blog wasn't migrated. Still try to find from the author. Old one is archived at https://web.archive.org/web/20180423042713/https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/

For tips on translating metadata for assets efficiently, see [5 Steps to efficiently translate metadata](https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/). 
-->

## 建立翻譯專案 {#creating-translation-projects}

若要建立語言副本，請觸發Assets UI中「參考」邊欄下方可用的下列語言副本工作流程之一：

**建立和翻譯**

在此工作流程中，要翻譯的資產會複製到您要翻譯之語言的語言根目錄。 此外，系統會根據您選擇的選項，在「專案」主控台中為資產建立翻譯專案。 視設定而定，翻譯專案可以手動啟動，或在建立翻譯專案後立即自動執行。

**更新語言副本**

您可以執行此工作流程來翻譯其他資產群組，並將其納入特定地區的語言副本中。 在此情況下，翻譯的資產會新增至已包含先前翻譯資產的目標資料夾。

>[!NOTE]
>
>只有翻譯服務提供者支援二進位檔的翻譯，資產二進位檔才會翻譯。

>[!NOTE]
>
>如果您啟動複雜資產(例如PDF檔案和Adobe InDesign檔案)的翻譯工作流程，則不會提交其子資產或轉譯（如果有）以進行翻譯。

### 建立和翻譯工作流程 {#create-and-translate-workflow}

您可以使用建立和翻譯工作流程來首次為特定語言產生語言副本。 工作流程提供下列選項：

* 僅建立結構
* 建立新的翻譯專案
* 新增至現有翻譯專案

### 僅建立結構 {#create-structure-only}

使用「 **僅建立結構** 」選項，在目標語言根目錄中建立目標資料夾層次結構，以匹配源語言根目錄中源資料夾的層次結構。在這種情況下，來源資產會複製到目標資料夾。但是，不會生成任何翻譯項目。

1. 在「資產」UI中，選取您要在目標語言根目錄中建立結構的來源資料夾。
1. 開啟「參 **[!UICONTROL 考」窗格]** ，然後按一下「復本」下的「語言復本 **[!UICONTROL 」(Language Copies]****[!UICONTROL )]**。
1. 按一下/點選底部的「建立並翻譯」]**。**[!UICONTROL 
1. 從&#x200B;**[!UICONTROL 目標語言]**&#x200B;清單中，選擇要為其建立資料夾結構的語言。
1. 從「專 **[!UICONTROL 案]** 」清單中，選 **[!UICONTROL 擇「僅建立結構」]**。
1. 按一下/點選「 **[!UICONTROL 建立]**」。目標語言的新結構列在&#x200B;**[!UICONTROL 語言副本]**&#x200B;下。
1. 按一下/點選清單中的結構，然後按一下/點選「在資產中顯現」]**以導覽至目標語言內的資料夾結構。**[!UICONTROL 

## 將翻譯雲服務應用於資料夾 {#applying-translation-cloud-services-to-folders}

Adobe Experience Manager(AEM)可讓您從所選翻譯提供者取得雲端型翻譯服務，確保資產能根據您的需求進行翻譯。

您可以直接將翻譯雲端服務套用至資產資料夾，以便在翻譯工作流程中使用。

### 應用翻譯服務 {#applying-the-translation-services}

直接將翻譯雲端服務套用至您的資產資料夾，無需在您建立或更新翻譯工作流程時設定翻譯服務。

1. 從「資產」使用者介面中，選取您要套用翻譯服務的資料夾。
1. 在工具列中，按一下/點選「屬 **[!UICONTROL 性」圖示]** ，以顯示「資 **** 料夾屬性」頁面。

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. 導覽至「 **[!UICONTROL 雲端服務]** 」標籤。
1. 從「Cloud Service配置」清單中，選擇所需的翻譯提供程式。 例如，如果要從Microsoft獲得翻譯服務，請選擇&#x200B;**[!UICONTROL Microsoft Translator]**。

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. 選擇翻譯提供程式的連接器。

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. 在工具列中，按一下/點選「 **[!UICONTROL 儲存]**」，然後按一下「確定 **** 」以關閉對話方塊。轉譯服務會套用至資料夾。

### 套用自訂翻譯連接器 {#applying-custom-translation-connector}

如果要為要用於翻譯工作流的翻譯服務應用自定義連接器。若要套用自訂連接器，請先從「封裝管理員」安裝連接器。然後，從雲端服務主控台設定連接器。在您設定連接器後，「套用轉譯服務」中所述的「雲端服務」標籤中的連接器清 [單中會顯示此連接器](#applying-the-translation-services)。在您應用自定義連接器並運行翻譯工作流後，翻譯項目的「 **[!UICONTROL Translation Summary]** 」 (翻譯摘要) 表徵圖會在heads **[!UICONTROL Provider]** and **[!UICONTROL Method下顯示連接器詳細資訊]**。

1. 從「封裝管理器」安裝連接器。
1. 按一下/點選AEM標誌，然後導覽至「**[!UICONTROL 工具>部署>Cloud Services」]**。
1. 在「雲端服務」頁面的「 **[!UICONTROL 協力廠商服務]** 」下，找 **[!UICONTROL 出您安裝的連接器]** 。

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. 按一下/點選&#x200B;**[!UICONTROL 立即設定]**&#x200B;連結以開啟&#x200B;**[!UICONTROL 建立設定]**&#x200B;對話方塊。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. 指定連接器的標題和名稱，然後按一下/點選「建 **[!UICONTROL 立」]**。自訂連接器位於「套用轉譯服務」步驟5中所述「 **[!UICONTROL 雲端服務]** 」標籤的連 [接器清單中](#applying-the-translation-services)。
1. 在套用自訂連接器後，執行建立翻譯專案中說明的任何翻譯工作流程。驗證「項目」控制台中翻譯項 **[!UICONTROL 目的「翻譯摘要]** 」表徵圖中連接器的詳 **[!UICONTROL 細資訊]** 。

   ![chlimage_1-220](assets/chlimage_1-220.png)
