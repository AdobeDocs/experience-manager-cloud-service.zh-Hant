---
title: 在動態媒體中使用選擇性發佈
description: 有關如何在動態媒體中使用選擇性發佈的資訊。
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
docset: aem65
translation-type: tm+mt
source-git-commit: 04f40452ca89bc5298341b4338bc1d7762b908c2
workflow-type: tm+mt
source-wordcount: '2922'
ht-degree: 3%

---


# 在動態媒體{#selective-publish-configure-folder}的資料夾層級設定選擇性發佈

您可以選擇使用&#x200B;**[!UICONTROL 管理出版物]**&#x200B;或&#x200B;**[!UICONTROL 快速發佈]**，將資產發佈或從AEM或動態媒體中取消發佈，而不是只依賴設定對動態媒體例項中所有資料夾全域的&#x200B;**[!UICONTROL 動態媒體設定]**。

例如，透過選擇性發佈，您可以針對尚未上線的產品處理資產。 在這種情況下，行銷團隊可以存取與動態媒體同步的智慧型裁切影像和動態轉譯，以便建立促銷文宣，完全不需要將這些資產發佈至動態媒體以進行全域傳送。

<!-- 
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>*復* 制資產至資料夾和從資料夾複製資產會清除這些資產的發佈狀態。但是，當&#x200B;*將*&#x200B;資產移至資料夾屬性設為&#x200B;**[!UICONTROL 選擇性發佈]**&#x200B;的資料夾時，這些資產的發佈狀態會維持。

如果您稍後決定變更資料夾中的&#x200B;**[!UICONTROL 選擇性發佈]**&#x200B;設定，這些變更只會影響您從該點開始上傳至該資料夾的新資產。 資料夾中現有資產的發佈狀態會維持原狀，直到您從「快速發佈」(**[!UICONTROL Quick Publish)或「管理出版物」(Manage Publication)對話方塊手動變更資產。]******

資料夾層級&#x200B;**[!UICONTROL 動態媒體發佈模式]**&#x200B;選項一律預設為&#x200B;**[!UICONTROL 動態媒體設定中的**[!UICONTROL &#x200B;發佈資產&#x200B;]**設定中的值。]** 但是，本主題中的下列步驟將顯示如何在資料夾級別手動更改此預設值（如以下步驟所述）以覆蓋 **[!UICONTROL 動態媒體配]** 置值。

無論您是依賴&#x200B;**[!UICONTROL 動態媒體設定]**&#x200B;中設定的&#x200B;**[!UICONTROL 發佈資產]**&#x200B;值，還是依賴資料夾層級屬性中設定的&#x200B;**[!UICONTROL 動態媒體發佈模式]**&#x200B;值，啟動&lt;a9/時，您仍能選擇&#x200B;**[!UICONTROL 立即]**、**[!UICONTROL >或**[!UICONTROL &#x200B;選擇性發佈。]**]** 例如，您可以在啟動後將 **[!UICONTROL Dynamic]** Publish  **[!UICONTROL Media中的「發佈資產」值設定為「啟動後發佈」，但將]**  **** ****  **** Dynamic Media Publish模式的資料夾級別設定為「選擇性發佈」，反之亦然，或者選擇性發佈(Publish Vice)。

在資料夾中設定選擇性發佈後，您可以執行下列任一項作業：

* [使用「管理出版物」，選擇性地將資產發佈至動態媒體或AEM。](#selective-publish-manage-publication)
* [使用「管理出版物」，從動態媒體或AEM選擇性地取消發佈資產。](#selective-unpublish-manage-publication)
* [使用「快速發佈」將資產發佈至動態媒體或AEM。](#quick-publish-aem-dm)
* [透過搜尋結果，選擇性地發佈或取消發佈資產。](#selective-publish-unpublish-search-results)

**若要在動態媒體的資料夾層級設定選擇性發佈**

1. 在AEM中，點選AEM標誌以存取全域導覽主控台。 在左側，點選「導覽」圖示（就在「工具」圖示上方），然後點選「**[!UICONTROL 資產>檔案」。]**
1. 執行下列任一項作業：
   * 編輯現有資料夾的屬性——在&#x200B;**[!UICONTROL 卡片視圖]**、**[!UICONTROL 列視圖]**&#x200B;或&#x200B;**[!UICONTROL 清單視圖]**&#x200B;中，導航到要編輯其屬性的資料夾。 選擇資料夾，然後在工具欄上，按一下「**[!UICONTROL 屬性」。]**
   * 編輯新資料夾的屬性——在&#x200B;**[!UICONTROL 卡片檢視]**、**[!UICONTROL 欄檢視]**&#x200B;或&#x200B;**[!UICONTROL 清單檢視]**&#x200B;中，在頁面右上角點選&#x200B;**[!UICONTROL 建立>資料夾。]** 在「建 **[!UICONTROL 立檔]** 案夾」對話方塊中，輸入檔案夾的標題（必要），然後點選「 **[!UICONTROL 建立」。]** 選擇資料夾，然後在工具欄上按一下「 **[!UICONTROL Properties」。]**

1. 在&#x200B;**[!UICONTROL 同步模式]**&#x200B;下拉式清單中，選取下列其中一項：

   | 同步模式 | 說明 |
   | --- | --- |
   | **[!UICONTROL 已繼承]** | 資料夾上沒有明確的同步值；而是從&#x200B;**[!UICONTROL 動態媒體配置中設定的其中一個祖先資料夾或預設模式繼承同步值。]** 通過工具提 **** 示顯示「繼承」的詳細狀態。 |
   | **[!UICONTROL 將此子樹狀結構資料夾的所有項目同步至 dynamicmedia]** | 若要發佈至動態媒體才能成功，資產必須同步至動態媒體。 選取此選項，會在此子樹狀結構中包含所有資產，以同步至動態媒體。 資料夾特定的設定會覆寫&#x200B;**[!UICONTROL 動態媒體設定中的預設設定。]** |
   | **[!UICONTROL 從動態媒體同步中排除此資料夾子樹狀結構中的所有項目]** | 排除此子樹狀結構中的所有資產，使其無法同步至動態媒體。 |

   ![資料夾層級選擇性發佈](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. 在&#x200B;**[!UICONTROL 動態媒體發佈模式]**&#x200B;下拉式清單中，選取一個選項。 請注意，**[!UICONTROL 動態媒體發佈模式]**&#x200B;選項一律預設為在&#x200B;**[!UICONTROL 動態媒體設定中設定的值。]** 不過，您可以使用下列其中一個選 **[!UICONTROL 項，手]** 動覆寫此預設的動態媒體設定值。

   >[!IMPORTANT]
   >
   >請注意，無論您選取的「動態媒體發佈」模式選項為何，您稍後對已發佈&#x200B;*的資產所做的任何更新，都會立即發佈這些更新，而不需執行任何使用者動作。*

   | 動態媒體發佈模式選項 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 當資產上傳至此檔案夾時，系統會將資產收錄至AEM並立即提供URL/內嵌。 此選項僅系結至AEM發佈，而且不需要使用者干預來發佈資產。<br>如果您在上 ** 一步驟中選取「從動態媒體同步 **[!UICONTROL 同步模式排除此資料夾子樹狀]** 結構中的所有項目」，則此選 **[!UICONTROL 項不]** 可用。 |
   | **[!UICONTROL 啟動時]** | 資產上傳至此檔案夾時，您必須先明確發佈資產，才能提供URL/內嵌連結。 此選項僅系結至AEM發佈。<br>如果您在上 ** 一步驟中選取「從動態媒體同步 **[!UICONTROL 同步模式排除此資料夾子樹狀]** 結構中的所有項目」，則此選 **[!UICONTROL 項不]** 可用。 |
   | **[!UICONTROL 選擇性發佈]** | 資產會發佈至您選擇的AEM或Dynamic Media，以便在公共網域中傳送。 兩種發佈方式互斥。  也就是說，您可以將資產發佈到DMS7，以便使用智慧型裁切或動態轉譯等功能。 或者，您可以將資產獨家發佈至AEM，以進行安全預覽；這些相同的資產&#x200B;*not*&#x200B;會發佈到DMS7，以便在公共域中交付。 如果您在上一步驟的「同步模式」中選擇「從動態媒體同步&#x200B;**[!UICONTROL 中排除此資料夾子樹中的所有內容」，則此選項不可用。]**]****[!UICONTROL  |

1. 在頁面的右上角，點選「**[!UICONTROL 儲存並關閉]**」，然後點選「**[!UICONTROL 確定]**」以返回AEM Assets。

## 使用「管理出版物」將資產選擇性地發佈至動態媒體或AEM做為雲端服務{#selective-publish-manage-publication}

使用&#x200B;**[!UICONTROL 管理出版物]**&#x200B;來選擇性發佈資產至動態媒體或AEM之前，請確定您已將&#x200B;**[!UICONTROL 動態媒體設定]**&#x200B;中的&#x200B;**[!UICONTROL 發佈資產]**&#x200B;選項設為&#x200B;**[!UICONTROL 選擇性發佈]**，或在資料夾層級設定選擇性發佈。

請參閱[建立動態媒體設定](#configuring-dynamic-media-cloud-services)或[在動態媒體中的資料夾層級設定選擇性發佈](#selective-publish-configure-folder)

<!--
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>*復* 制資產至資料夾和從資料夾複製資產會清除這些資產的發佈狀態。但是，當&#x200B;*將*&#x200B;資產移至資料夾屬性設為&#x200B;**[!UICONTROL 選擇性發佈]**&#x200B;的資料夾時，這些資產的發佈狀態會維持。

**若要使用「管理出版物」將資產選擇性地發佈至動態媒體或AEM做為雲端服務**

1. 在AEM中，點選AEM標誌以存取全域導覽主控台。 在左側，點選「導覽」圖示（就在「工具」圖示上方），然後點選「**[!UICONTROL 資產>檔案」。]**
1. 在&#x200B;**[!UICONTROL 卡片檢視]**、**[!UICONTROL 欄檢視]**&#x200B;或&#x200B;**[!UICONTROL 清單檢視]**&#x200B;中，執行下列其中一項作業：
   * 導覽至您要發佈其資產的檔案夾。 選擇資料夾，然後在工具欄上，按一下「管理出版物」。****  您可能會發現使用「清單檢 **[!UICONTROL 視」]** 會很有幫助，因此您可以更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要發佈其資產的檔案夾。 開啟檔案夾，然後選取一或多個資產。 在工具列上，點選「管理出版物」。**** 您可能會發現使用清單檢 **[!UICONTROL 視]** 器很有幫助，因此您可以更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >如果工具列上未顯示「管理出版物」，請改為點選省略號按鈕，然後從清單選單中選取「管理出版物」。**[!UICONTROL ****]**

1. 在&#x200B;**[!UICONTROL 管理出版物——選項]**&#x200B;頁面的&#x200B;**[!UICONTROL Action]**&#x200B;下，選取您想要的啟動類型。

   | 動作 | 說明 |
   | --- | --- |
   | **[!UICONTROL 發佈]** （至AEM） | 選取這個選項，將資產發佈至AEM以進行安全預覽。 |
   | **[!UICONTROL 發佈至 Dynamic Media]** | 選取此選項，將資產發佈至動態媒體，以便在公用網域中傳送，或者您可以使用智慧型裁切或動態轉譯等功能。<br>只有在「動態媒體發佈」 **[!UICONTROL 模式設為「選]** 擇性發佈」檔案 **[!UICONTROL 夾的屬]** 性時，此選項才可用。 |

1. 在「**[!UICONTROL 排程]**」下方，設定發佈的時間。

   | 計劃 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 選取以立即發佈資產。 |
   | **[!UICONTROL 稍後]** | 選擇以在特定日期和時間發佈資產。 |

1. 在&#x200B;**[!UICONTROL 管理出版物]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL 下一步。]**
1. 在&#x200B;**[!UICONTROL 管理出版物——範圍]**&#x200B;頁中，執行下列操作之一：
   * 視需要，選取一或多個您要從發佈中移除的資產。
   * 在&#x200B;**[!UICONTROL 管理出版物——範圍]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL 發佈]**&#x200B;或&#x200B;**[!UICONTROL 發佈至動態媒體。]**
1. 點選&#x200B;**[!UICONTROL 確定。]**

### 使用「管理出版物{#selective-unpublish-manage-publication}」從動態媒體或AEM選擇性地取消發佈資產

1. 在AEM中，點選AEM標誌以存取全域導覽主控台。 在左側，點選「導覽」圖示（就在「工具」圖示上方），然後點選「**[!UICONTROL 資產>檔案」。]**
1. 在&#x200B;**[!UICONTROL 卡片檢視]**、**[!UICONTROL 欄檢視]**&#x200B;或&#x200B;**[!UICONTROL 清單檢視]**&#x200B;中，執行下列其中一項作業：
   * 導覽至您要解除發佈其資產的檔案夾。 選擇資料夾，然後在工具欄上，按一下「管理出版物」。****  您可能會發現使用「清單檢 **[!UICONTROL 視」]** 會很有幫助，因此您可以更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要解除發佈其資產的檔案夾。 開啟檔案夾，然後選取一或多個資產。 在工具列上，點選「管理出版物」。**** 您可能會發現使用清單檢 **[!UICONTROL 視]** 器很有幫助，因此您可以更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >如果工具列上未顯示「管理出版物」，請改為點選省略號按鈕，然後從清單選單中選取「管理出版物」。**[!UICONTROL ****]**

1. 在&#x200B;**[!UICONTROL 管理出版物——選項]**&#x200B;頁面的&#x200B;**[!UICONTROL Action]**&#x200B;下，選取您想要的取消啟動類型。

   | 動作 | 說明 |
   | --- | --- |
   | **[!UICONTROL 取消發佈]** （從AEM） | 選取這個選項，可從AEM取消發佈資產。 |
   | **[!UICONTROL 從 Dynamic Media 取消發佈]** | 選取此選項，可從動態媒體取消發佈資產。<br>只有在「動態媒體發佈」 **[!UICONTROL 模式設為「選]** 擇性發佈」檔案 **[!UICONTROL 夾的屬]** 性時，此選項才可用。 |

1. 在&#x200B;**[!UICONTROL Schedule]**&#x200B;下，設定取消激活的時間。

   | 計劃 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 選取以立即取消發佈資產。 |
   | **[!UICONTROL 稍後]** | 選取以取消發佈特定日期和時間的資產。 |

1. 在&#x200B;**[!UICONTROL 管理出版物]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL 下一步。]**
1. 在&#x200B;**[!UICONTROL 管理出版物——範圍]**&#x200B;頁中，執行下列操作之一：
   * 選取一或多個要從取消發佈移除的資產。
   * 在&#x200B;**[!UICONTROL 管理出版物——範圍]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL 取消發佈]**&#x200B;或&#x200B;**[!UICONTROL 從動態媒體取消發佈。]**
1. 點選&#x200B;**[!UICONTROL 確定。]**

## 使用「快速發佈」將資產發佈至動態媒體或AEM {#quick-publish-aem-dm}

您可以使用&#x200B;**[!UICONTROL Quick Publish]**&#x200B;來啟動資產。 **[!UICONTROL 「快速發]** 布」會立即發佈選取的資產，而不需進一步的使用者互動。因此，任何未發佈的參照也會自動發佈。

>[!NOTE]
>
>若要使用&#x200B;**[!UICONTROL 快速發佈]**&#x200B;將資產發佈至動態媒體或AEM，請務必在&#x200B;**[!UICONTROL 動態媒體設定]**&#x200B;或選取資料夾的資料夾屬性中啟用&#x200B;**[!UICONTROL 選擇性發佈]**。

**若要使用「快速發佈」將資產發佈至動態媒體或AEM**

1. 在AEM中，點選AEM標誌以存取全域導覽主控台。 在頁面的左側，點選「導覽」圖示（就在「工具」圖示上方），然後在頁面的右側點選「**[!UICONTROL 資產>檔案」。]**
1. 在&#x200B;**[!UICONTROL 卡片檢視]**、**[!UICONTROL 欄檢視]**&#x200B;或&#x200B;**[!UICONTROL 清單檢視]**&#x200B;中，執行下列其中一項作業：
   * 導覽至您要發佈其資產的檔案夾。 選取資料夾，然後在工具列上，點選「快速發佈」。****  您可能會發現使用「清單檢 **[!UICONTROL 視」]** 會很有幫助，因此您可以更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要發佈其資產的檔案夾。 開啟檔案夾，然後選取一或多個資產。 在工具列上，點選「**[!UICONTROL 快速發佈」。]** 您可能會發現使用清單檢 **[!UICONTROL 視]** 器很有幫助，因此您可以更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >如果工具列上未顯示「快速發佈」(**[!UICONTROL Quick Publish)]**，請改為點選省略號按鈕，然後從清單選單中選取「快速發佈」(**[!UICONTROL Quick Publish)]**。

      ![資料夾層級快速發佈至動態媒體](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. 從&#x200B;**[!UICONTROL 快速發佈]**&#x200B;功能表清單中，選擇下列選項之一。

   | 快速發佈選項 | 它的功能 |
   | --- | --- | 
   | 發佈至 AEM | 將選取的資產立即發佈至AEM。 |
   | 發佈至 Brand Portal 網站 | 將選取的資產立即發佈至&#x200B;**[!UICONTROL 品牌入口網站。]**<br>只有在您的AEM Assets例項已設定品牌**[!UICONTROL &#x200B;端&#x200B;]**口時，此選項才可用。 |
   | 發佈至 Dynamic Media | 立即將選取的資產發佈至動態媒體。<br>資產必須已同步至動態媒體。如有必要，請確定資料夾屬性中的&#x200B;**[!UICONTROL 同步模式]**&#x200B;已設定為&#x200B;**[!UICONTROL 將此資料夾子樹中的所有內容同步到動態媒體。]** |

1. 點選&#x200B;**[!UICONTROL 確定，]**，然後點選&#x200B;**[!UICONTROL 關閉，]**

## 透過搜尋結果{#selective-publish-unpublish-search-results}選擇性地發佈或取消發佈資產

搜尋結果可顯示不同動態媒體發佈設定之資產檔案夾中的資產。 如果您已從搜尋結果中選取一或多個資產，而資產具有不同的動態媒體發佈模式設定，您可以從工具列觸發&#x200B;**[!UICONTROL 管理出版物]**&#x200B;以發佈或取消發佈。

另請參閱[在AEM中搜尋資產。](/help/assets/search-assets.md)

**若要透過搜尋結果選擇性地發佈或取消發佈資產**

1. 在AEM中，在頁面的左上角，點選AEM標誌以存取全域導覽主控台。 在頁面的左側，點選「導覽」圖示（就在「工具」圖示上方），然後點選「**[!UICONTROL 資產>檔案」。]**
1. 在工具列上，在頁面右上角附近點選「搜尋」圖示（放大鏡）。
1. 在&#x200B;**[!UICONTROL Type to search]**&#x200B;文字欄位中，輸入關鍵字，然後按&#x200B;**[!UICONTROL Enter。]**
1. 在頁面的右上角，點選「**[!UICONTROL 清單檢視]**」圖示。
1. 在頁面的左上角附近，點選&#x200B;**[!UICONTROL Filters]**&#x200B;圖示。

   ![搜尋結果中的清單檢視和篩選](/help/assets/assets-dm/select-publish-search-result.png)

1. 在左側面板中，展開&#x200B;**[!UICONTROL Status]**，然後展開&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;搜尋述詞。
1. 使用&#x200B;**[!UICONTROL Published]**&#x200B;和&#x200B;**[!UICONTROL Unpublished]**核取方塊，根據動態媒體資產的發佈狀態進一步調整搜尋結果。
或者，您可搭配使用這些核取方塊與**[!UICONTROL Publish]**&#x200B;搜尋述詞，以調整&#x200B;**[!UICONTROL Published]**&#x200B;和&#x200B;**[!UICONTROL Unpublished]** AEM資產的搜尋結果。
1. 執行下列任一項作業：
   * 選取一或多個您要發佈或取消發佈的資產。
   * 在&#x200B;**[!UICONTROL 搜尋結果]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL 全選。]**
1. 在工具列上，點選「管理出版物」。**** 您可能需要點選工具列上的省略號圖示，才能查看「管 **[!UICONTROL 理出版物」。]**
1. 在&#x200B;**[!UICONTROL 管理出版物——選項]**&#x200B;頁面上，選擇所要的動作。

   | 選取的動作 | 動態媒體設定中的發佈資產設定 | 資產是 |
   | --- | --- | --- |
   | 發佈 | 立即或在啟動時 | 發佈至AEM和動態媒體。 |
   | 發佈 | 選擇性發佈 | 僅發佈至AEM。 |
   | 未發佈 | 立即或在啟動時 | 未從AEM和動態媒體發佈。 |
   | 未發佈 | 選擇性發佈 | 僅從AEM取消發佈。 |
   | 發佈至 Dynamic Media | 立即或在啟動時 | 未發佈至AEM或Dynamic Media，或兩者。 |
   | 發佈至 Dynamic Media | 選擇性發佈 | 僅發佈至動態媒體。 |
   | 從 Dynamic Media 取消發佈 | 立即或在啟動時 | 未從AEM或Dynamic Media或兩者取消發佈。 |
   | 從 Dynamic Media 取消發佈 | 選擇性發佈 | 僅從動態媒體取消發佈。 |

1. 在&#x200B;**[!UICONTROL Schedule]**&#x200B;下，設定取消激活的時間。

   | 選定的計畫 | 發生的事 |
   | --- | --- |
   | 立即 | 會立即執行選取的動作。 |
   | 稍後 | 所選動作會在選取的特定日期和時間執行。 |

1. 在&#x200B;**[!UICONTROL 管理出版物——選項]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL 下一頁。]**
1. （可選）在&#x200B;**[!UICONTROL 管理出版物——範圍]**&#x200B;頁面中，查看選定資產表格中的&#x200B;**[!UICONTROL 發佈目標]**&#x200B;欄。

   | 動態媒體設定中的發佈資產設定 | 選取的動作 | 發佈目標 |
   | --- | --- | --- |
   | 啟動時立即或<br> | 發佈 | AEM和Dynamic Media |
   | 啟動時立即或<br> | 發佈至 Dynamic Media | 無 |
   | 選擇性發佈 | 發佈 | AEM |
   | 選擇性發佈 | 發佈至 Dynamic Media | Dynamic Media |
   | 啟動時立即或<br> | 未發佈 | AEM和Dynamic Media |
   | 啟動時立即或<br> | 從 Dynamic Media 取消發佈 | 無 |
   | 選擇性發佈 | 未發佈 | AEM |
   | 選擇性發佈 | 從 Dynamic Media 取消發佈 | 動態媒體 |

1. 在&#x200B;**[!UICONTROL 管理出版物——範圍]**&#x200B;頁中，執行下列操作之一：
   * 選取一或多個要從發佈或取消發佈移除的資產。
   * 在&#x200B;**[!UICONTROL 管理出版物——範圍]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL 發佈]**&#x200B;或&#x200B;**[!UICONTROL 取消發佈]**&#x200B;以開始動作。
1. 點選&#x200B;**[!UICONTROL 確定。]**

## 檢查資產{#check-publish-status-of-asset}的發佈狀態

您可以在AEM中將&#x200B;**[!UICONTROL Timeline]**&#x200B;與&#x200B;**[!UICONTROL Card view]**、**[!UICONTROL Column View]**&#x200B;或&#x200B;**[!UICONTROL List View]**&#x200B;搭配使用，以快速檢查資產的發佈狀態。

**若要檢查資產的發佈狀態**

1. 在AEM中，在頁面的左上角，點選AEM標誌以存取全域導覽主控台。 在頁面的左側，點選「導覽」圖示（就在「工具」圖示上方），然後點選「**[!UICONTROL 資產>檔案」。]**
1. 在&#x200B;**[!UICONTROL 卡片檢視]**、**[!UICONTROL 欄檢視]**&#x200B;或&#x200B;**[!UICONTROL 清單檢視]**（下方的螢幕擷取顯示&#x200B;**[!UICONTROL 清單檢視]**）中，開啟包含您已發佈或未發佈之資產的檔案夾。
1. 選取資產，以便以勾號顯示。 請參閱以下螢幕擷取範例。
1. 在頁面左上角附近，從下拉式選單中選取「**[!UICONTROL 時間軸」。]** 左側 **** 面板中的「狀態」區域會顯示所選資產的發佈狀態。當您使用&#x200B;**[!UICONTROL 清單檢視]**&#x200B;時，會出現另一欄，顯示&#x200B;**[!UICONTROL 動態媒體]**&#x200B;發佈狀態。
   * 配置為同步至動態媒體的資料夾將預設顯示&#x200B;**[!UICONTROL 動態媒體]**&#x200B;列。
   * 將&#x200B;*not*設定為同步至動態媒體的資料夾，將不會顯示動態媒體欄。
      ![清單檢視和時間軸](/help/assets/assets-dm/selective-publish-status-timeline.png)

## 疑難排解選擇性發佈{#selective-publish-troubleshoot}

未同步至動態媒體但在其上觸發動態媒體發佈動作的資產會產生下列錯誤訊息和解決方案：

![選擇性發佈錯誤](/help/assets/assets-dm/selective-publish-error.png)

