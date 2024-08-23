---
title: 透過通用編輯器使用頁面範本
description: 瞭解如何透過Universal Editor建立和使用頁面範本。
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 773ce75975f4dcc2c5310422bcc377b487ebec25
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 2%

---


# 透過通用編輯器使用頁面範本 {#page-templates}

瞭解如何透過Universal Editor建立和使用頁面範本。

>[!NOTE]
>
>此功能將在即將發行的AEM as a Cloud Service中提供。

## 什麼是頁面範本？ {#what-are}

品牌和行銷指導方針通常會指定內容頁面的特定版面配置。 許多頁面會共用相同的結構和版面，這也是現實情況。 為了節省內容作者時間，可以從範本建立頁面。

頁面範本可作為頁面配置的主版副本。 當您從範本建立頁面時，範本的內容會複製到新頁面，有助於為內容作者預先定義頁面的版面配置和初始內容，節省他們的時間。

## 建立頁面範本 {#creating}

您可以建立新頁面，或使用現有頁面作為範本，來建立頁面範本。 在這兩種情況下，您都使用&#x200B;[**Sites**&#x200B;主控台。](/help/sites-cloud/authoring/sites-console/introduction.md)

### 建立新範本 {#create-new}

1. 使用&#x200B;**Sites**&#x200B;主控台來導覽至您要建立新頁面的位置，此新頁面將做為您的範本，並[像建立任何其他頁面一樣建立頁面。](/help/sites-cloud/authoring/sites-console/creating-pages.md)

1. 建立頁面並返回主控台後，請選取頁面，然後點選或按一下工具列中的&#x200B;[**屬性**&#x200B;圖示](/help/sites-cloud/authoring/sites-console/page-properties.md)。

1. 在&#x200B;**範本設定**&#x200B;區段下內容對話方塊的&#x200B;**進階**&#x200B;標籤上，選取切換&#x200B;**使用作為範本**。

1. 在&#x200B;**範本名稱**&#x200B;欄位中，提供描述性名稱。

   * 這是將顯示建立新內容頁面以及選取新頁面所依據之範本的名稱。

1. 點選或按一下&#x200B;**儲存並關閉**。

您的新頁面現在可以在建立新頁面時作為範本使用。

### 使用現有頁面作為範本 {#existing-page}

1. 使用&#x200B;**Sites**&#x200B;主控台來[導覽至您要用作範本的頁面](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources)的位置。

1. 選取頁面，然後點選或按一下工具列中的&#x200B;[**屬性**&#x200B;圖示](/help/sites-cloud/authoring/sites-console/page-properties.md)。

1. 在&#x200B;**範本設定**&#x200B;區段下內容對話方塊的&#x200B;**進階**&#x200B;標籤上，選取切換&#x200B;**使用作為範本**。

1. 在&#x200B;**範本名稱**&#x200B;欄位中，提供描述性名稱。

   * 這是將顯示建立新內容頁面以及選取新頁面所依據之範本的名稱。

1. 點選或按一下&#x200B;**儲存並關閉**。

現在建立新頁面時，可將選取的頁面當作範本使用。

## 從範本建立頁面 {#creating-from-template}

從範本建立頁面以與Universal Editor搭配使用時，與[建立頁面的工作流程相同。](/help/sites-cloud/authoring/sites-console/creating-pages.md)

1. 使用&#x200B;**Sites**&#x200B;主控台來[導覽至您要建立新頁面的位置](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources)。

1. 點選或按一下「**建立** -> **頁面**」。

1. 在&#x200B;**建立頁面**&#x200B;精靈的&#x200B;**範本**&#x200B;索引標籤上，您可以選取您新頁面要依據的範本。 點選或按一下所需的範本以選取它，然後點選或按一下&#x200B;**下一步**。

完成精靈，就像處理任何其他頁面一樣，而且您已根據選取的範本建立新頁面。

## 通用編輯器和頁面編輯器 {#page-vs-universal}

通用編輯器的頁面範本解決了AEM頁面編輯器](/help/sites-cloud/authoring/page-editor/templates.md)的[頁面範本相同的問題，以便能夠重複使用內容，根據一組預先定義的版面快速建立頁面。 但它們解決問題的方式大不相同。 如果您是頁面編輯器的使用者，請注意這些差異。

* 從用於「通用編輯器」的頁面範本建立的頁面是範本的獨立副本。
* 因此，如果範本變更，產生的頁面不會變更。
* 內容作者可視需要修改和更新產生頁面的內容，對範本沒有限制。
