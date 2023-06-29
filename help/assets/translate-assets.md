---
title: 如何在AEM中翻譯資產？
description: 瞭解如何自動化工作流程，以將AEM中的資產（包括二進位檔、中繼資料和標籤）翻譯成多種語言。
contentOwner: AG
feature: Asset Management,Translation
role: Admin,User
exl-id: 98df1412-a957-48a3-81c2-7dfe1d5e6d31
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '2646'
ht-degree: 23%

---

# 在AEM中翻譯資產 {#multilingual-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/multilingual-assets.html?lang=en) |
| AEM as a Cloud Service  | 本文 |

多語言資產是指具有多語言二進位檔案、中繼資料和標籤的資產。 通常，資產的二進位檔案、中繼資料和標籤會以一種語言存在，然後會翻譯成其他語言以用於多語言專案。 Adobe Experience Manager Assets可讓您自動化翻譯資產（包括二進位檔案、中繼資料和標籤）的工作流程，以產生其他語言版本的資產，以用於多語言專案。

若要自動化AEM資產翻譯，您可以將翻譯服務提供商與Experience Manager整合，並建立專案以將資產翻譯成多種語言。 Experience Manager支援人工和機器翻譯工作流程。

AEM中的人力資產翻譯：已翻譯的資產會傳回並匯入至Experience Manager。 當您的翻譯提供者與Experience Manager整合時，資產會自動在Experience Manager和翻譯提供者之間傳送。

AEM中的機器資產翻譯：機器翻譯服務會立即翻譯資產的中繼資料和標籤。

<!--
We have multiple articles around translation of assets. For now, dumping all content in this article to remove others and create only ONE UBER article.

https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/translation-projects.html
https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/preparing-assets-for-translation.html
[Apply translation cloud services to folders](https://experienceleague.adobe.com/docs/experience-manager-65/assets/managing/transition-cloud-services.html)

One of these articles is a copy of [Preparing Content for Translation](https://experienceleague.adobe.com/docs/experience-manager-65/administering/introduction/tc-prep.html

-->

<!-- 
Translating assets includes the following:

1. [Connecting Experience Manager with the translation service provider](/help/sites-administering/tc-tic.md#connecting-to-a-translation-service-provider)
1. [Creating translation integration framework configurations](/help/sites-administering/tc-tic.md)
1. [Preparing assets for translation](prepare-assets-for-translation.md)
1. [Applying translation cloud services to folders](transition-cloud-services.md)
1. [Create translation projects](translation-projects.md)

If your translation service provider does not provide a connector to integrate with Experience Manager, use an [alternative process](/help/sites-administering/tc-manage.md#exporting-a-translation-job).

Also see, [Creating translation projects for content fragments](creating-translation-projects-for-content-fragments.md).

-->

## 準備翻譯資產 {#prepare-to-translate-assets}

多語言資產是指具有多語言二進位檔案、中繼資料和標籤的資產。 通常，資產的二進位檔案、中繼資料和標籤會以一種語言存在，然後會翻譯成其他語言以用於多語言專案。

在Adobe Experience Manager資產中，多語言資產包含在資料夾中，其中每個資料夾都包含不同語言的資產。

每個語言資料夾都稱為語言副本。 語言副本的根資料夾（稱為語言根）可識別語言副本中內容的語言。 例如， `/content/dam/it` 是義大利文語言副本的義大利文語言根。 語言副本必須使用 [已正確設定的語言根目錄](#create-a-language-root) 以便在翻譯來源資產時鎖定正確的語言。

您最初新增資產的語言副本為主要語言。 主要語言是翻譯成其他語言的來源。 範例資料夾階層包含數個語言根：

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

執行以下步驟以準備翻譯資產：

1. 建立主要語言的語言根。 例如，範例資料夾階層中英文副本的語言根為 `/content/dam/en`. 請確定已根據中的資訊正確設定語言根 [建立語言根](#create-a-language-root).

1. 將資產新增至您的主要語言。
1. 建立您需要語言副本的每個目標語言的語言根。

### 建立語言根 {#create-a-language-root}

若要建立語言根，請建立資料夾，並使用ISO語言代碼作為Name屬性的值。 建立語言根後，您可以在語言根內的任何層級建立語言副本。

例如，範例階層的義大利文語言副本的根頁面有 `it` 作為Name屬性。 Name屬性會用作存放庫中資產節點的名稱，從而決定資產的路徑。 (*&lt;server>：&lt;port>/assets.html/content/dam/it/*)

1. 在「資產」主控台中，按一下/點選「 **[!UICONTROL 建立]** 」，然後從 **[!UICONTROL 選單選擇「資料夾]** 」。
1. 在「名稱」欄位中，輸入國家/地區代碼，格式為 `<language-code>`.
1. 按一下或點選 **[!UICONTROL 建立]**. 語言根會在Assets主控台中建立。

### 檢視語言根 {#view-language-roots}

觸控最佳化的UI提供「參考」面板，顯示已在其中建立的語言根清單 [!DNL Assets].

1. 在Assets控制檯中，選取您要建立語言副本的主要語言。
1. 按一下或點選「全域導覽」圖示，然後選擇 **[!UICONTROL 引用]** 以開啟「參考」窗格。
1. 在「參照」窗格中，按一下或點選 **[!UICONTROL 語言副本]**. 「語言副本」面板會顯示資產的語言副本。

### 建立新的翻譯專案 {#create-a-new-translation-project}

如果您使用此選項，要翻譯的資產會複製到您要翻譯之語言的語言根目錄中。 系統會根據您選擇的選項，在「專案」主控台中建立資產的翻譯專案。 根據設定，翻譯專案可以手動啟動，或在建立翻譯專案後立即自動執行。

1. 在「資產」UI中，選取您要建立語言副本的來源資料夾。
1. 開啟「參 **[!UICONTROL 考」窗格]** ，然後按一下「復本」下的「語言復本 **[!UICONTROL 」(Language Copies]****[!UICONTROL )]**。
1. 按一下/點選 **[!UICONTROL 建立並翻譯]** 在底部。
1. 從「目 **[!UICONTROL 標語言]** 」清單中，選取您要建立檔案夾結構的語言。
1. 從 **[!UICONTROL 專案]** 清單，選取 **[!UICONTROL 建立新的翻譯專案]**.
1. 在「專 **[!UICONTROL 案標題]** 」欄位中，輸入專案標題。
1. 按一下/點選 **[!UICONTROL 建立]**. 來源資料夾中的資產會複製到您在步驟4中所選地區設定的目標資料夾。
1. 若要導覽至資料夾，請選取語言副本，然後按一下 **[!UICONTROL 在資產中顯示]**.
1. 導覽至「專案」主控台。 翻譯資料夾會複製到專案主控台。
1. 開啟資料夾以檢視翻譯專案。
1. 按一下/點選專案以開啟詳細資訊頁面。
1. 若要檢視翻譯工作的狀態，請按一下 **[!UICONTROL 翻譯工作]** 圖磚。 <!-- For more details around job statuses, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. 在Assets使用者介面中，開啟每個已翻譯資產的「屬性」頁面，以檢視已翻譯的中繼資料。

>[!NOTE]
>
>資產和資料夾皆可使用此功能。 選取資產而非資料夾時，會複製至語言根目錄為止的資料夾整個階層，以建立資產的語言副本。

### 新增至現有翻譯專案 {#add-to-existing-translation-project}

如果您使用此選項，則會在執行先前的翻譯工作流程後，為您新增至來源資料夾的資產執行翻譯工作流程。 只有新新增的資產會複製到包含先前翻譯的資產的目標資料夾。 在此情況下不會建立新的翻譯專案。

1. 在「資產」UI中，導覽至包含未翻譯資產的來源資料夾。
1. 選取您要轉換的資產，並開啟「參考」 **[!UICONTROL 窗格]**。「語 **[!UICONTROL 言副本]** 」部分顯示當前可用的翻譯副本數。
1. 按一下/點選「 **[!UICONTROL 復本」下的]** 「語言 **[!UICONTROL 復本」]**。將顯示可用翻譯副本的清單。
1. 按一下/點選 **[!UICONTROL 建立並翻譯]** 在底部。
1. 從「目 **[!UICONTROL 標語言]** 」清單中，選取您要建立檔案夾結構的語言。
1. 從「項 **[!UICONTROL 目]** 」清單中，選擇「 **[!UICONTROL 添加到現有翻譯項目」]** ，以在資料夾中運行翻譯工作流。
   >[!NOTE]
   >
   >如果您選擇 **[!UICONTROL 新增至現有翻譯專案]** 選項，則僅當您的專案設定完全符合預先存在的專案的設定時，才會將翻譯專案新增至預先存在的專案。 否則，會建立新專案。
1. 從 **[!UICONTROL 現有翻譯專案]** 清單中，選取要新增資產以進行翻譯的專案。
1. 按一下/點選「 **[!UICONTROL 建立]**」。要翻譯的資產會新增至目標資料夾。更新的資料夾會列在「語言復 **[!UICONTROL 本」區段下]** 。
1. 導覽至「專案」主控台，並開啟您新增的現有翻譯專案。
1. 按一下/點選翻譯專案，檢視專案詳細資訊頁面。
1. 按一下/點選「 」底部的省略符號 **翻譯工作** 並排顯示，以在翻譯工作流程中檢視資產。 翻譯工作清單也會顯示資產中繼資料和標記項目。這些項目表示資產中繼資料和標記也已翻譯。

   >[!NOTE]
   >
   >* 如果您刪除標籤或中繼資料的專案，則不會為任何資產翻譯標籤或中繼資料。
   >* 如果您使用機器翻譯，資產二進位檔將不會翻譯。
   >* 如果您新增至翻譯工作的資產包含子資產，請選取子資產並移除它們，翻譯才能順利進行。

1. 若要開始資產的翻譯，請按一下/點選 **[!UICONTROL 翻譯工作]** 並選取 **[!UICONTROL 開始]** 從清單中。 訊息會通知翻譯工作已開始。
1. 若要檢視翻譯工作的狀態，請按一下/點選「 」底部的省略符號 **[!UICONTROL 翻譯工作]** 圖磚。 <!-- For more details, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job). -->
1. 翻譯完成後，狀態會變更為「準備好檢閱」。 導覽至「資產」UI，然後開啟每個已翻譯資產的「屬性」頁面，以檢視已翻譯的中繼資料。

### 更新語言副本 {#update-language-copies}

執行此工作流程可翻譯任何其他資產集，並將其納入特定地區設定的語言副本中。 在此情況下，已翻譯的資產會新增至已包含先前已翻譯資產的目標資料夾。 根據選項選擇，會建立翻譯專案或更新新資產的現有翻譯專案。 更新語言副本工作流程包含以下選項：

* 建立新的翻譯專案
* 新增至現有翻譯專案

### 新增至現有翻譯專案 {#add-to-existing-translation-project-1}

如果您使用此選項，資產集會新增至現有的翻譯專案，以更新您選擇之地區設定的語言副本。

1. 從「資產」UI中，選取您新增資產資料夾的來源資料夾。
1. 開啟「參 **[!UICONTROL 考」窗格]**，然後按一下/點選「復本」下的「語言復本 ******** 」，以顯示語言復本清單。
1. 在「語言副本」之前選 **[!UICONTROL 取核取方塊]**，以選取所有語言副本。取消選擇與要翻譯的語言環境相對應的語言副本 (副本) 以外的其他副本。
1. 按一下/點選 **[!UICONTROL 更新語言副本]** 在底部。
1. 從 **[!UICONTROL 專案]** 清單，選擇 **[!UICONTROL 新增至現有翻譯專案]**.
1. 從 **[!UICONTROL 現有翻譯專案]** 清單中，選取要新增資產以進行翻譯的專案。
1. 按一下/點選「 **[!UICONTROL 開始]**」。
1. 請參閱步驟9-14 / [新增至現有翻譯專案](#add-to-existing-translation-project) 以完成其餘程式。

### 建立暫存語言副本 {#creating-temporary-language-copies}

當您執行翻譯工作流程，以使用原始資產的編輯版本更新語言副本時，現有的語言副本會保留，直到您核准翻譯的資產為止。 [!DNL Assets] 會將新翻譯的資產儲存在暫存位置，並在您明確核准資產後更新現有的語言副本。 如果您拒絕資產，則語言副本保持不變。

1. 按一下/點選下方的來源根資料夾 **[!UICONTROL 語言副本]** 您已為其建立語言副本，然後按一下/點選 **[!UICONTROL 在資產中顯示]** 以開啟資料夾 [!DNL Assets].
1. 從「資產」UI中，選取您已翻譯的資產，然後按一下/點選 **[!UICONTROL 編輯]** 圖示來在編輯模式下開啟資產。
1. 編輯資產，然後儲存變更。
1. 執行步驟2-14 [新增至現有翻譯專案](#add-to-existing-translation-project) 更新語言副本的程式。
1. 按一下/點選「 」底部的省略符號 **[!UICONTROL 翻譯工作]** 圖磚。 從「 」中的資產清單 **[!UICONTROL 翻譯工作]** 頁面，您可以清楚檢視儲存資產翻譯版本的暫時位置。
1. 選取旁邊的核取方塊 **[!UICONTROL 標題]**.
1. 在工具列中，按一下/點選「 **[!UICONTROL Accept Translation]** 」 (接受翻譯)，然後在對話方塊中按一下/點選「 **[!UICONTROL Accept]** 」 (接受)，以使用已編輯資產的翻譯版本覆寫目標資料夾中的翻譯資產。

   >[!NOTE]
   >
   >若要啟用翻譯工作流程以更新目標資產，請接受資產和中繼資料。

   按一下/點選 **[!UICONTROL 拒絕翻譯]** 保留目標地區設定根目錄中資產的原始翻譯版本，並拒絕編輯的版本。

1. 導覽至「資產」主控台，然後開啟每個已翻譯資產的「屬性」頁面，以檢視已翻譯的中繼資料。

<!-- TBD: Possibly this blog was not migrated. Still try to find from the author. Old one is archived at https://web.archive.org/web/20180423042713/https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/

For tips on translating metadata for assets efficiently, see [5 Steps to efficiently translate metadata](https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/). 
-->

## 建立翻譯專案 {#creating-translation-projects}

若要建立語言副本，請觸發Assets UI中參考邊欄下可用的以下語言副本工作流程之一：

**建立並翻譯**

在此工作流程中，要翻譯的資產會複製到您要翻譯之語言的語言根目錄中。 此外，系統會根據您選擇的選項，在「專案」主控台中建立資產的翻譯專案。 根據設定，翻譯專案可以手動啟動，或允許在建立翻譯專案後立即自動執行。

**更新語言副本**

您可以執行此工作流程來翻譯其他資產群組，並將其包含在特定地區設定的語言副本中。 在此情況下，已翻譯的資產會新增至已包含先前已翻譯資產的目標資料夾。

>[!NOTE]
>
>只有當翻譯服務提供者支援二進位檔翻譯時，才會翻譯資產二進位檔。

>[!NOTE]
>
>如果您啟動複雜資產(例如PDF檔案和Adobe InDesign檔案)的翻譯工作流程，其子資產或轉譯（如果有的話）將不會提交以進行翻譯。

### 建立及翻譯工作流程 {#create-and-translate-workflow}

您可使用建立及翻譯工作流程，首次產生特定語言的語言副本。 工作流程提供下列選項：

* 僅建立結構
* 建立新的翻譯專案
* 新增至現有翻譯專案

### 僅建立結構 {#create-structure-only}

使用「 **僅建立結構** 」選項，在目標語言根目錄中建立目標資料夾層次結構，以匹配源語言根目錄中源資料夾的層次結構。在這種情況下，來源資產會複製到目標資料夾。但是，不會生成任何翻譯項目。

1. 在Assets UI中，選取您要在目標語言根中建立結構的來源資料夾。
1. 開啟「參 **[!UICONTROL 考」窗格]** ，然後按一下「復本」下的「語言復本 **[!UICONTROL 」(Language Copies]****[!UICONTROL )]**。
1. 按一下/點選 **[!UICONTROL 建立並翻譯]** 在底部。
1. 從 **[!UICONTROL 目標語言]** 清單中，選取您要建立資料夾結構的語言。
1. 從「專 **[!UICONTROL 案]** 」清單中，選 **[!UICONTROL 擇「僅建立結構」]**。
1. 按一下/點選「 **[!UICONTROL 建立]**」。目標語言的新結構會列在 **[!UICONTROL 語言副本]**.
1. 按一下/點選清單中的結構，然後按一下/點選 **[!UICONTROL 在資產中顯示]** 導覽至目標語言中的資料夾結構。

## 將翻譯雲端服務套用至資料夾 {#applying-translation-cloud-services-to-folders}

Adobe Experience Manager可讓您使用所選翻譯提供者提供的雲端型翻譯服務，確保根據您的需求翻譯資產。

您可以將翻譯雲端服務直接套用至資產資料夾，以便在翻譯工作流程期間使用這些服務。

### 套用翻譯服務 {#applying-the-translation-services}

將翻譯雲端服務直接套用至您的資產資料夾，讓您在建立或更新翻譯工作流程時無需設定翻譯服務。

1. 從Assets使用者介面中，選取您要套用翻譯服務的資料夾。
1. 在工具列中，按一下/點選「屬 **[!UICONTROL 性」圖示]** ，以顯示「資 **** 料夾屬性」頁面。

   ![chlimage_1-215](assets/chlimage_1-215.png)

1. 導覽至「 **[!UICONTROL 雲端服務]** 」標籤。
1. 從「Cloud Service設定」清單中，選擇所需的翻譯提供者。 例如，如果您想從Microsoft使用翻譯服務，請選擇 **[!UICONTROL Microsoft Translator]**.

   ![chlimage_1-216](assets/chlimage_1-216.png)

1. 選擇翻譯提供者的聯結器。

   ![chlimage_1-217](assets/chlimage_1-217.png)

1. 在工具列中，按一下/點選「 **[!UICONTROL 儲存]**」，然後按一下「確定 **** 」以關閉對話方塊。轉譯服務會套用至資料夾。

### 套用自訂翻譯聯結器 {#applying-custom-translation-connector}

如果要為要用於翻譯工作流的翻譯服務應用自定義連接器。若要套用自訂聯結器，請先從以下位置安裝聯結器 [封裝管理員](/help/implementing/developing/tools/package-manager.md). 然後，從雲端服務主控台設定連接器。在您設定連接器後，「套用轉譯服務」中所述的「雲端服務」標籤中的連接器清 [單中會顯示此連接器](#applying-the-translation-services)。在您應用自定義連接器並運行翻譯工作流後，翻譯項目的「 **[!UICONTROL Translation Summary]** 」 (翻譯摘要) 表徵圖會在heads **[!UICONTROL Provider]** and **[!UICONTROL Method下顯示連接器詳細資訊]**。

1. 從安裝聯結器 [封裝管理員](/help/implementing/developing/tools/package-manager.md).
1. 按一下/點選Experience Manager標誌，然後導覽至 **[!UICONTROL 「工具>部署>Cloud Services」]**.
1. 在「雲端服務」頁面的「 **[!UICONTROL 協力廠商服務]** 」下，找 **[!UICONTROL 出您安裝的連接器]** 。

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. 按一下/點選 **[!UICONTROL 立即設定]** 開啟「 」的連結 **[!UICONTROL 建立設定]** 對話方塊。

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. 指定連接器的標題和名稱，然後按一下/點選「建 **[!UICONTROL 立」]**。自訂連接器位於「套用轉譯服務」步驟5中所述「 **[!UICONTROL 雲端服務]** 」標籤的連 [接器清單中](#applying-the-translation-services)。
1. 在套用自訂連接器後，執行建立翻譯專案中說明的任何翻譯工作流程。驗證「項目」控制台中翻譯項 **[!UICONTROL 目的「翻譯摘要]** 」表徵圖中連接器的詳 **[!UICONTROL 細資訊]** 。

   ![chlimage_1-220](assets/chlimage_1-220.png)

**另請參閱**

* [Assets HTTP API](mac-api-assets.md)
* [資產支援的檔案格式](file-format-support.md)
* [搜尋資產](search-assets.md)
* [連接的資產](use-assets-across-connected-assets-instances.md)
* [資產報表](asset-reports.md)
* [中繼資料結構描述](metadata-schemas.md)
* [下載資產](download-assets-from-aem.md)
* [管理中繼資料](manage-metadata.md)
* [搜尋 Facet](search-facets.md)
* [管理收藏集](manage-collections.md)
* [大量中繼資料匯入](metadata-import-export.md)
