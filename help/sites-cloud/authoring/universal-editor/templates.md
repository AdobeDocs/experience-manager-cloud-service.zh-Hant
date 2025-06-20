---
title: 建立可透過通用編輯器編輯的頁面的範本
description: 瞭解如何建立可用來建立可透過通用編輯器編輯的頁面的範本，以節省時間並確保品牌的一致性。
solution: Experience Manager Sites
feature: Authoring
role: User
exl-id: f0d60086-e92e-4492-ad50-bef84fed2a82
source-git-commit: 3238b11cdd891cf18048199d4103397e3af75edf
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 26%

---


# 建立可透過通用編輯器編輯的頁面的範本 {#page-templates}

瞭解如何建立可用來建立可透過通用編輯器編輯的頁面的範本，以節省時間並確保品牌的一致性。

>[!NOTE]
>
>[範本也可用於建立可使用頁面編輯器](/help/sites-cloud/authoring/page-editor/templates.md)編輯的頁面。

## 什麼是頁面範本？ {#what-are}

品牌化和行銷指導方針通常會規定內容頁面的特定版面。同樣常見的情況是，許多頁面會共用相同的結構與版面。若要為內容作者節省時間，可以從範本來建立頁面。

頁面範本會用作頁面版面的主版副本。當您從範本建立頁面時，範本的初始內容會複製到新頁面，有助於為內容作者預先定義頁面的基本版面和內容，為他們節省時間。

## 啟用頁面範本 {#enabling-templates}

若要使用範本來建立可透過通用編輯器編輯的頁面，您必須啟用選項。

首先啟用網站組態的可編輯範本。

1. 使用&#x200B;**網站**&#x200B;主控台，並[選取網站的根目錄](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources)。
1. 選取網站根目錄後，點選或按一下工具列中的&#x200B;[**屬性**&#x200B;圖示](/help/sites-cloud/authoring/sites-console/page-properties.md)。
1. 在屬性對話方塊的&#x200B;**進階**&#x200B;索引標籤上，記下&#x200B;**雲端設定**&#x200B;欄位中的值。
1. 從主要導覽選擇&#x200B;**工具** -> **一般** -> **設定瀏覽器**。
1. 在&#x200B;**[組態瀏覽器](/help/implementing/developing/introduction/configurations.md)**&#x200B;中，選取您在上一步中注意到的組態，然後點選或按一下工具列中的&#x200B;**屬性**。
1. 在&#x200B;**組態屬性**&#x200B;視窗中，核取選項&#x200B;**可編輯的範本**。
1. 點選或按一下「**儲存並關閉**」。

啟用設定後，您必須允許網站的範本。

1. 使用&#x200B;**網站**&#x200B;主控台，並[選取網站的根目錄](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources)。
1. 選取網站根目錄後，點選或按一下工具列中的&#x200B;[**屬性**&#x200B;圖示](/help/sites-cloud/authoring/sites-console/page-properties.md)。
1. 在&#x200B;**範本設定**&#x200B;區段下內容對話方塊的&#x200B;**進階**&#x200B;標籤上，點選或按一下&#x200B;**新增**&#x200B;按鈕。
1. 在&#x200B;**允許的範本**&#x200B;下方出現的新空白欄位中，新增路徑`/conf/<site>/settings/wcm/templates/.*`。
1. 點選或按一下「**儲存並關閉**」。

您現在可以使用範本建立網站的頁面。 此工作僅能在每個您想要使用範本的網站/設定中執行一次，才能建立可透過通用編輯器編輯的頁面。

## 建立新的範本 {#create-new}

您可以[建立新頁面](/help/sites-cloud/authoring/sites-console/creating-pages.md)做為範本，或使用現有頁面做為範本的基礎。

1. 使用&#x200B;**Sites**&#x200B;主控台來[導覽至您想要用作範本的新頁面或現有頁面](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources)，然後點選或按一下以選取它。

1. 選取頁面後，點選或按一下工具列中的&#x200B;[**屬性**&#x200B;圖示](/help/sites-cloud/authoring/sites-console/edit-page-properties.md)。

1. 在&#x200B;**範本設定**&#x200B;區段下內容對話方塊的&#x200B;**進階**&#x200B;標籤上，選取切換&#x200B;**將頁面用作範本**。

1. 點選或按一下「**儲存並關閉**」。

您的新頁面現在可以在建立新頁面時作為範本使用了。

## 從範本建立頁面 {#creating-from-template}

從範本建立可透過Universal Editor編輯的頁面，與建立任何其他頁面[&#128279;](/help/sites-cloud/authoring/sites-console/creating-pages.md)的工作流程相同。

1. 使用 **Sites** 主控台[導覽到您希望在其中建立新頁面的位置](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources)。

1. 點選或按一下「**建立**」->「**頁面**」。

1. 在「**建立頁面**」精靈的「**範本**」索引標籤上，您可以選取要以哪個範本作為基礎來建立新頁面。點選或按一下以選取想要使用的範本，然後點選或按一下「**下一步**」。

就像處理任何其他頁面一樣完成精靈，您就會根據所選的範本完成新頁面的建立。

## 頁面和範本 {#pages-vs-templates}

頁面範本只會定義頁面的初始內容。 然後可以使用通用編輯器完全編輯頁面。

* 從頁面範本建立的頁面是範本的獨立副本。
* 如果範本變更，根據該範本的現有頁面不會變更。
* 內容作者可以根據需要修改和更新結果頁面的內容，不會受到範本的限制。

## 可編輯的範本 {#editable-templates}

使用[頁面編輯器](/help/sites-cloud/authoring/page-editor/introduction.md)建立的頁面也可以以範本為基礎。 用來為通用編輯器和頁面編輯器建立頁面的範本都運用AEM的[可編輯範本](/help/implementing/developing/components/templates.md)。

用來建立可透過頁面編輯器編輯的頁面的範本，會使用可編輯範本的所有功能。 用來建立可透過通用編輯器編輯的頁面的範本只會使用初始內容功能。
