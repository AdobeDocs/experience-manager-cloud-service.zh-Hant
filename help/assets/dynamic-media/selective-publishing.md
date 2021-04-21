---
title: 在 Dynamic Media 中使用選擇性發佈
description: 瞭解如何在Dynamic Media使用Selective Publish。
contentOwner: Rick Brough
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: Business Practitioner
exl-id: a5a2df68-be13-45a6-ad80-09fbd2fea8f2
translation-type: tm+mt
source-git-commit: e94289bccc09ceed89a2f8b926817507eaa19968
workflow-type: tm+mt
source-wordcount: '2935'
ht-degree: 3%

---

# 在Dynamic Media{#selective-publish-configure-folder}的資料夾級別配置選擇性發佈

您可以使用&#x200B;**[!UICONTROL 管理出版物]**&#x200B;或&#x200B;**[!UICONTROL 快速發佈]**，選擇在資料夾層級將資產發佈或從Adobe Experience Manager或Dynamic Media取消發佈。 此發佈方法很有用，因為它不僅依賴於&#x200B;**[!UICONTROL Dynamic Media配置]**，其設定對Dynamic Media實例中的所有資料夾都是全局的。

例如，透過選擇性發佈，您可以針對尚未上線的產品處理資產。 在這種情況下，行銷團隊可以存取與Dynamic Media同步的智慧型裁切影像和動態轉譯。 他們可以製作宣傳材料，完全不需要將這些資產發佈到Dynamic Media，以便在全球進行交付。

<!-- 
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>*復* 制資產至資料夾和從資料夾複製資產會清除這些資產的發佈狀態。但是，當&#x200B;*將*&#x200B;資產移至資料夾屬性設為&#x200B;**[!UICONTROL 選擇性發佈]**&#x200B;的資料夾時，這些資產的發佈狀態會維持。

如果您稍後決定變更資料夾中的&#x200B;**[!UICONTROL 選擇性發佈]**&#x200B;設定，這些變更只會影響您從該點開始上傳至該資料夾的新資產。 資料夾中現有資產的發佈狀態會維持原狀，直到您從「快速發佈」(**[!UICONTROL Quick Publish)或「管理出版物」(Manage Publication)對話方塊手動變更資產。]******

資料夾層級&#x200B;**[!UICONTROL Dynamic Media發佈模式]**&#x200B;選項一律預設為&#x200B;**[!UICONTROL Dynamic Media組態]**&#x200B;中&#x200B;**[!UICONTROL 發佈資產]**&#x200B;設定中的值。 但是，本主題中的下列步驟將顯示如何手動更改資料夾級別的此預設值（如以下步驟所述）以覆蓋&#x200B;**[!UICONTROL Dynamic Media配置]**&#x200B;值。

無論您是否依賴：

* 在&#x200B;**[!UICONTROL Dynamic Media配置]**&#x200B;中設定的&#x200B;**[!UICONTROL 發佈資產]**&#x200B;值
* 或者，在資料夾層級屬性中設定的&#x200B;**[!UICONTROL Dynamic Media發佈模式]**&#x200B;值

您仍然可以選擇「啟動時立即」(**[!UICONTROL Immedialed]**)、「啟動時」(]**)或「選擇性發佈」(**[!UICONTROL )。 ****&#x200B;例如，您可以將&#x200B;**[!UICONTROL Dynamic Media配置]**&#x200B;中的&#x200B;**[!UICONTROL 發佈資產]**&#x200B;值設為&#x200B;**[!UICONTROL 在啟動時]**。 此外，您可將資料夾層級的&#x200B;**[!UICONTROL Dynamic Media發佈]**&#x200B;模式值設為&#x200B;**[!UICONTROL 選擇性發佈]**，依此類推。

在資料夾中設定選擇性發佈後，您可以執行下列任一項作業：

* [使用「管理出版物」，選擇性地將資產發佈至Dynamic Media或Experience Manager](#selective-publish-manage-publication)。
* [使用「管理出版物」從Dynamic Media或Experience Manager選擇性地取消發佈資產](#selective-unpublish-manage-publication)。
* [使用「快速發佈」將資產發佈至Dynamic Media或Experience Manager](#quick-publish-aem-dm)。
* [透過搜尋結果，選擇性地發佈或取消發佈資產](#selective-publish-unpublish-search-results)。

**在Dynamic Media的資料夾級別配置選擇性發佈**

1. 在Experience Manager中，點選Experience Manager標誌以存取全域導覽主控台。 在左側，點選「導覽」圖示（就在「工具」圖示上方），然後點選「**[!UICONTROL 資產>檔案]**」。
1. 執行下列任一項作業：
   * 編輯現有資料夾的屬性——在&#x200B;**[!UICONTROL 卡片視圖]**、**[!UICONTROL 列視圖]**&#x200B;或&#x200B;**[!UICONTROL 清單視圖]**&#x200B;中，導航到要編輯其屬性的資料夾。 選擇資料夾，然後在工具欄上，按一下&#x200B;**[!UICONTROL 屬性]**。
   * 編輯新資料夾的屬性——在&#x200B;**[!UICONTROL 卡片視圖]**、**[!UICONTROL 列視圖]**&#x200B;或&#x200B;**[!UICONTROL 清單視圖]**&#x200B;中，在頁面右上角附近，按一下&#x200B;**[!UICONTROL 建立>資料夾]**。 在&#x200B;**[!UICONTROL 建立資料夾]**&#x200B;對話方塊中，輸入資料夾的標題（必要），然後點選&#x200B;**[!UICONTROL 建立]**。 選擇資料夾，然後在工具欄上，按一下&#x200B;**[!UICONTROL 屬性]**。

1. 在&#x200B;**[!UICONTROL 同步模式]**&#x200B;下拉式清單中，選取下列其中一項：

   | 同步模式 | 說明 |
   | --- | --- |
   | **[!UICONTROL 已繼承]** | 資料夾上沒有明確的同步值；相反，資料夾會繼承其中一個祖先資料夾或&#x200B;**[!UICONTROL Dynamic Media配置]**&#x200B;中設定的預設模式的同步值。 **[!UICONTROL Inherited]**&#x200B;的詳細狀態會透過工具提示顯示。 |
   | **[!UICONTROL 將此資料夾子樹中的所有內容同步到Dynamic Media]** | 為了發佈至Dynamic Media成功，資產必須同步至Dynamic Media。 選取此選項會包含此子樹中要同步至Dynamic Media的所有資產。 資料夾特定設定覆蓋&#x200B;**[!UICONTROL Dynamic Media配置]**&#x200B;中的預設設定。 |
   | **[!UICONTROL 從Dynamic Media同步中排除此資料夾子樹中的所有內容]** | 排除此子樹中的所有資產，使其不能同步至Dynamic Media。 |

   ![資料夾層級選擇性發佈](/help/assets/assets-dm/createfolder-properties-selectivepublish.png)

1. 在&#x200B;**[!UICONTROL Dynamic Media發佈模式]**&#x200B;下拉式清單中，選取一個選項。 **[!UICONTROL Dynamic Media發佈模式]**&#x200B;選項始終預設為在&#x200B;**[!UICONTROL Dynamic Media配置]**&#x200B;中設定的值。 不過，您可以使用下列其中一個選項手動覆寫此預設的&#x200B;**[!UICONTROL Dynamic Media組態]**&#x200B;值。

   >[!IMPORTANT]
   >
   >無論您選取的「Dynamic Media發佈」模式選項、您稍後對已發佈&#x200B;*的資產所做的任何更新，這些更新都會立即發佈，而不需執行任何使用者動作。*

   | Dynamic Media發佈模式選項 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 當資產上傳至此檔案夾時，系統會將資產收錄至Experience Manager，並立即提供URL/內嵌。 此選項僅系結至Experience Manager發佈，而且發佈資產不需要使用者干預。<br>如果在上一步 ** 中選擇了「從Dynamic Media同步同步模 **[!UICONTROL 式中排除此資料夾子樹中的所有內容」，則]** 此選 **** 項不可用。 |
   | **[!UICONTROL 啟動時]** | 資產上傳至此檔案夾時，您必須先明確發佈資產，才能提供URL/內嵌連結。 此選項僅系結至Experience Manager發佈。<br>如果在上一步 ** 中選擇了「從Dynamic Media同步同步模 **[!UICONTROL 式中排除此資料夾子樹中的所有內容」，則]** 此選 **** 項不可用。 |
   | **[!UICONTROL 選擇性發佈]** | 資產會發佈至您選擇的Experience Manager或Dynamic Media，以便在公共網域中傳送。 兩種發佈方式互斥。 也就是說，您可以將資產發佈到DMS7，以便使用智慧型裁切或動態轉譯等功能。 或者，您可以將資產獨家發佈至Experience Manager，以進行安全預覽；這些相同的資產&#x200B;*not*&#x200B;會發佈到DMS7，以便在公共域中交付。 如果在上一步中選擇了「從&#x200B;**[!UICONTROL 同步模式]**&#x200B;中的Dynamic Media同步&#x200B;]**中排除此資料夾子樹中的所有內容」，則此選項不可用。**[!UICONTROL  |

1. 在頁面的右上角，點選&#x200B;**[!UICONTROL 儲存並關閉]**，然後點選&#x200B;**[!UICONTROL 確定]**&#x200B;以返回Experience Manager資產。

## 使用「管理出版物」將資產選擇性發佈至Dynamic Media或Experience Manager做為Cloud Service{#selective-publish-manage-publication}

使用&#x200B;**[!UICONTROL 管理出版物]**&#x200B;來選擇性地將資產發佈至Dynamic Media或Experience Manager之前，請確定您已執行下列任一項作業：

* 將&#x200B;**[!UICONTROL Dynamic Media配置]**&#x200B;中的&#x200B;**[!UICONTROL 發佈資產]**&#x200B;選項設定為&#x200B;**[!UICONTROL 選擇性發佈]**。
* 或者，在資料夾層級設定選擇性發佈。

請參閱[建立Dynamic Media配置](#configuring-dynamic-media-cloud-services)或[在Dynamic Media的資料夾級別配置選擇性發佈](#selective-publish-configure-folder)

<!--
>[!IMPORTANT]
>
>Selective Publish is only available in Dynamic Media - Scene7 mode.
-->

>[!NOTE]
>
>*復* 制資產至資料夾和從資料夾複製資產會清除這些資產的發佈狀態。但是，當&#x200B;*將*&#x200B;資產移至資料夾屬性設為&#x200B;**[!UICONTROL 選擇性發佈]**&#x200B;的資料夾時，這些資產的發佈狀態會維持。

**使用「管理出版物」將資產選擇性地發佈至Dynamic Media或Experience Manager做為Cloud Service**

1. 在Experience Manager中，點選Experience Manager標誌以存取全域導覽主控台。 在左側，點選「導覽」圖示（就在「工具」圖示上方），然後點選「**[!UICONTROL 資產>檔案]**」。
1. 在&#x200B;**[!UICONTROL 卡片檢視]**、**[!UICONTROL 欄檢視]**&#x200B;或&#x200B;**[!UICONTROL 清單檢視]**&#x200B;中，執行下列其中一項作業：
   * 導覽至您要發佈其資產的檔案夾。 選擇資料夾，然後在工具欄上，按一下「管理出版物」。 ****&#x200B;使用&#x200B;**[!UICONTROL 清單檢視]**，讓您更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要發佈其資產的檔案夾。 開啟檔案夾，然後選取一或多個資產。 在工具列上，點選&#x200B;**[!UICONTROL 管理出版物]**。 使用&#x200B;**[!UICONTROL 清單檢視]**，讓您更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >如果工具列上未顯示「管理出版物」，請改為點選省略號按鈕，然後從清單選單中選取「管理出版物」。********

1. 在&#x200B;**[!UICONTROL 管理出版物——選項]**&#x200B;頁面的&#x200B;**[!UICONTROL Action]**&#x200B;下，選取您想要的啟動類型。

   | 動作 | 說明 |
   | --- | --- |
   | **[!UICONTROL 發佈]** (至Experience Manager) | 若要將資產發佈至Experience Manager以進行安全預覽，請選取此選項。 |
   | **[!UICONTROL 發佈至 Dynamic Media]** | 若要將資產發佈至Dynamic Media以便在公共網域中傳送，或讓您可以使用智慧型裁切或動態轉譯等功能，請選取此選項。<br>此選項僅在將「 **[!UICONTROL Dynamic Media發佈」]** 模式設定為 **[!UICONTROL 「選擇]** 發佈」資料夾屬性時可用。 |

1. 在「**[!UICONTROL 排程]**」下方，設定發佈的時間。

   | 計劃 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 選取以立即發佈資產。 |
   | **[!UICONTROL 稍後]** | 選擇以在特定日期和時間發佈資產。 |

1. 在&#x200B;**[!UICONTROL 管理出版物]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL Next]**。
1. 在&#x200B;**[!UICONTROL 管理出版物——範圍]**&#x200B;頁中，執行下列操作之一：
   * 視需要，選取一或多個您要從發佈中移除的資產。
   * 在&#x200B;**[!UICONTROL 管理出版物——範圍]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL 發佈]**&#x200B;或&#x200B;**[!UICONTROL 發佈至Dynamic Media]**。
1. 點選&#x200B;**[!UICONTROL 確定]**。

### 使用管理出版物{#selective-unpublish-manage-publication}從Dynamic Media或Experience Manager選擇性地取消發佈資產

1. 在Experience Manager中，點選Experience Manager標誌以存取全域導覽主控台。 在左側，點選「導覽」圖示（就在「工具」圖示上方），然後點選「**[!UICONTROL 資產>檔案]**」。
1. 在&#x200B;**[!UICONTROL 卡片檢視]**、**[!UICONTROL 欄檢視]**&#x200B;或&#x200B;**[!UICONTROL 清單檢視]**&#x200B;中，執行下列其中一項作業：
   * 導覽至您要解除發佈其資產的檔案夾。 選擇資料夾，然後在工具欄上，按一下「管理出版物」。 ****&#x200B;使用&#x200B;**[!UICONTROL 清單檢視]**，讓您更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要解除發佈其資產的檔案夾。 開啟檔案夾，然後選取一或多個資產。 在工具列上，點選&#x200B;**[!UICONTROL 管理出版物]**。 使用&#x200B;**[!UICONTROL 清單檢視]**，讓您更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >如果工具列上未顯示「管理出版物」，請改為點選省略號按鈕，然後從清單選單中選取「管理出版物」。********

1. 在&#x200B;**[!UICONTROL 管理出版物——選項]**&#x200B;頁面的&#x200B;**[!UICONTROL Action]**&#x200B;下，選取您想要的取消啟動類型。

   | 動作 | 說明 |
   | --- | --- |
   | **[!UICONTROL 取消發佈]** (從Experience Manager) | 若要從Experience Manager中取消發佈資產，請選取此選項。 |
   | **[!UICONTROL 從 Dynamic Media 取消發佈]** | 若要從Dynamic Media取消發佈資產，請選取此選項。<br>此選項僅在將「 **[!UICONTROL Dynamic Media發佈」]** 模式設定為 **[!UICONTROL 「選擇]** 發佈」資料夾屬性時可用。 |

1. 在&#x200B;**[!UICONTROL Schedule]**&#x200B;下，設定取消激活的時間。

   | 計劃 | 說明 |
   | --- | --- |
   | **[!UICONTROL 立即]** | 選取以立即取消發佈資產。 |
   | **[!UICONTROL 稍後]** | 選取以取消發佈特定日期和時間的資產。 |

1. 在&#x200B;**[!UICONTROL 管理出版物]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL Next]**。
1. 在&#x200B;**[!UICONTROL 管理出版物——範圍]**&#x200B;頁中，執行下列操作之一：
   * 選取一或多個要從取消發佈移除的資產。
   * 在&#x200B;**[!UICONTROL 管理出版物——範圍]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL 取消發佈]**&#x200B;或&#x200B;**[!UICONTROL 取消發佈從Dynamic Media]**。
1. 點選&#x200B;**[!UICONTROL 確定]**。

## 使用快速發佈{#quick-publish-aem-dm}將資產發佈至Dynamic Media或Experience Manager

您可以使用&#x200B;**[!UICONTROL Quick Publish]**&#x200B;來啟動資產。 **[!UICONTROL 「快速發]** 布」會立即發佈選取的資產，而不需進一步的使用者互動。任何未發佈的參考也會自動發佈。

>[!NOTE]
>
>若要使用&#x200B;**[!UICONTROL 快速發佈]**&#x200B;將資產發佈至Dynamic Media或Experience Manager，請確定&#x200B;**[!UICONTROL 選擇性發佈]**&#x200B;已在您的&#x200B;**[!UICONTROL Dynamic Media設定]**&#x200B;或所選資料夾的資料夾屬性中啟用。

**若要使用「快速發佈」將資產發佈至Dynamic Media或Experience Manager:**

1. 在Experience Manager中，點選Experience Manager標誌以存取全域導覽主控台。 在頁面的左側，點選「導覽」圖示（就在「工具」圖示上方），然後在頁面的右側點選「**[!UICONTROL 資產>檔案]**」。
1. 在&#x200B;**[!UICONTROL 卡片檢視]**、**[!UICONTROL 欄檢視]**&#x200B;或&#x200B;**[!UICONTROL 清單檢視]**&#x200B;中，執行下列其中一項作業：
   * 導覽至您要發佈其資產的檔案夾。 選取資料夾，然後在工具列上，點選&#x200B;**[!UICONTROL 快速發佈]**。 使用&#x200B;**[!UICONTROL 清單檢視]**，讓您更輕鬆地檢查特定資料夾的發佈狀態。
   * 導覽至您要發佈其資產的檔案夾。 開啟檔案夾，然後選取一或多個資產。 在工具列上，點選&#x200B;**[!UICONTROL 快速發佈]**。 使用&#x200B;**[!UICONTROL 清單檢視]**，讓您更輕鬆地檢查特定資產的發佈狀態。

      >[!NOTE]
      >
      >如果工具列上未顯示「快速發佈」(**[!UICONTROL Quick Publish)]**，請改為點選省略號按鈕，然後從清單選單中選取「快速發佈」(**[!UICONTROL Quick Publish)]**。

      ![資料夾層級快速發佈至Dynamic Media](/help/assets/assets-dm/selective-publish-folder-quick-publish-to-dm.png)

1. 從&#x200B;**[!UICONTROL 快速發佈]**&#x200B;功能表清單中，選擇下列選項之一。

   | 快速發佈選項 | 它的功能 |
   | --- | --- | 
   | 發佈至Experience Manager | 將選取的資產立即發佈至Experience Manager。 |
   | 發佈至 Brand Portal 網站 | 將選取的資產立即發佈至&#x200B;**[!UICONTROL 品牌入口網站]**。<br>只有在您的Experience Manager資產實例已配置品牌端 **[!UICONTROL 口]** 時，此選項才可用。 |
   | 發佈至 Dynamic Media | 將選定資產立即發佈至Dynamic Media。<br>資產必須已經同步到Dynamic Media。如有必要，請確定資料夾屬性中的&#x200B;**[!UICONTROL 同步模式]**&#x200B;已設定為&#x200B;**[!UICONTROL 將此資料夾子樹中的所有內容同步到Dynamic Media]**。 |

1. 點選&#x200B;**[!UICONTROL 確定，]**&#x200B;然後點選&#x200B;**[!UICONTROL 關閉]**。

## 透過搜尋結果{#selective-publish-unpublish-search-results}選擇性地發佈或取消發佈資產

搜尋結果可顯示不同Dynamic Media發佈設定之資產資料夾中的資產。 如果您已從搜尋結果中選取一或多個資產，而資產具有不同的Dynamic Media發佈模式設定，您可以從工具列觸發&#x200B;**[!UICONTROL 管理出版物]**&#x200B;以發佈或取消發佈。

另請參閱[Experience Manager](/help/assets/search-assets.md)中的搜尋資產。

**若要透過搜尋結果選擇性地發佈或取消發佈資產**

1. 在Experience Manager中，在頁面的左上角，點選Experience Manager標誌以存取全域導覽主控台。 在頁面的左側，點選「導覽」圖示（就在「工具」圖示上方），然後點選「**[!UICONTROL 資產>檔案]**」。
1. 在工具列上，在頁面右上角附近點選「搜尋」圖示（放大鏡）。
1. 在&#x200B;**[!UICONTROL Type to search]**&#x200B;文字欄位中，輸入關鍵字，然後按&#x200B;**[!UICONTROL Enter]**。
1. 在頁面的右上角，點選「**[!UICONTROL 清單檢視]**」圖示。
1. 在頁面的左上角附近，點選&#x200B;**[!UICONTROL Filters]**&#x200B;圖示。

   ![搜尋結果中的清單檢視和篩選](/help/assets/assets-dm/select-publish-search-result.png)

1. 在左側面板中，展開&#x200B;**[!UICONTROL Status]**，然後展開&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;搜尋述詞。
1. 使用&#x200B;**[!UICONTROL Published]**&#x200B;和&#x200B;**[!UICONTROL Unpublished]**核取方塊，根據Dynamic Media資產的發佈狀態進一步調整搜尋結果。
或者，您可以將這些核取方塊與**[!UICONTROL Publish]**&#x200B;搜尋述詞搭配使用，以細化&#x200B;**[!UICONTROL Published]**&#x200B;和&#x200B;**[!UICONTROL Unpublished]** Experience Manager資產的搜尋結果。
1. 執行下列任一項作業：
   * 選取一或多個您要發佈或取消發佈的資產。
   * 在&#x200B;**[!UICONTROL 搜尋結果]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL 全選]**。
1. 在工具列上，點選&#x200B;**[!UICONTROL 管理出版物]**。 如有必要，請點選工具列上的省略號圖示，以查看「管理出版物」。****
1. 在&#x200B;**[!UICONTROL 管理出版物——選項]**&#x200B;頁面上，選擇所要的動作。

   | 選取的動作 | 在Dynamic Media配置中發佈資產設定 | 資產是 |
   | --- | --- | --- |
   | 發佈 | 立即或在啟動時 | 出版給Experience Manager和Dynamic Media。 |
   | 發佈 | 選擇性發佈 | 僅發佈至Experience Manager。 |
   | 未發佈 | 立即或在啟動時 | 未發表於Experience Manager和Dynamic Media。 |
   | 未發佈 | 選擇性發佈 | 僅未從Experience Manager發佈。 |
   | 發佈至 Dynamic Media | 立即或在啟動時 | 不發佈給Experience Manager或Dynamic Media或兩者。 |
   | 發佈至 Dynamic Media | 選擇性發佈 | 僅發佈給Dynamic Media。 |
   | 從 Dynamic Media 取消發佈 | 立即或在啟動時 | 未從Experience Manager或Dynamic Media或兩者中解除發佈。 |
   | 從 Dynamic Media 取消發佈 | 選擇性發佈 | 僅從Dynamic Media發佈。 |

1. 在&#x200B;**[!UICONTROL Schedule]**&#x200B;下，設定取消激活的時間。

   | 選定的計畫 | 發生的事 |
   | --- | --- |
   | 立即 | 會立即執行選取的動作。 |
   | 稍後 | 所選動作會在選取的特定日期和時間執行。 |

1. 在&#x200B;**[!UICONTROL 管理出版物——選項]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL Next]**。
1. （可選）在&#x200B;**[!UICONTROL 管理出版物——範圍]**&#x200B;頁面中，查看選定資產表格中的&#x200B;**[!UICONTROL 發佈目標]**&#x200B;欄。

   | 在Dynamic Media配置中發佈資產設定 | 選取的動作 | 發佈目標 |
   | --- | --- | --- |
   | 啟動時立即或<br> | 發佈 | Experience Manager和Dynamic Media |
   | 啟動時立即或<br> | 發佈至 Dynamic Media | 無 |
   | 選擇性發佈 | 發佈 | Experience Manager |
   | 選擇性發佈 | 發佈至 Dynamic Media | Dynamic Media |
   | 啟動時立即或<br> | 未發佈 | Experience Manager和Dynamic Media |
   | 啟動時立即或<br> | 從 Dynamic Media 取消發佈 | 無 |
   | 選擇性發佈 | 未發佈 | Experience Manager |
   | 選擇性發佈 | 從 Dynamic Media 取消發佈 | Dynamic Media |

1. 在&#x200B;**[!UICONTROL 管理出版物——範圍]**&#x200B;頁中，執行下列操作之一：
   * 選取一或多個要從發佈或取消發佈移除的資產。
   * 在&#x200B;**[!UICONTROL 管理出版物——範圍]**&#x200B;頁面的右上角，點選&#x200B;**[!UICONTROL 發佈]**&#x200B;或&#x200B;**[!UICONTROL 取消發佈]**&#x200B;以開始動作。
1. 點選&#x200B;**[!UICONTROL 確定]**。

## 檢查資產{#check-publish-status-of-asset}的發佈狀態

您可以在Experience Manager中使用&#x200B;**[!UICONTROL 時間軸]**&#x200B;與&#x200B;**[!UICONTROL 卡片檢視]**、**[!UICONTROL 欄檢視]**&#x200B;或&#x200B;**[!UICONTROL 清單檢視]**&#x200B;搭配使用，以快速檢查資產的發佈狀態。

**若要檢查資產的發佈狀態**

1. 在Experience Manager中，在頁面的左上角，點選Experience Manager標誌以存取全域導覽主控台。 在頁面的左側，點選「導覽」圖示（就在「工具」圖示上方），然後點選「**[!UICONTROL 資產>檔案]**」。
1. 在&#x200B;**[!UICONTROL 卡片檢視]**、**[!UICONTROL 欄檢視]**&#x200B;或&#x200B;**[!UICONTROL 清單檢視]**（下方的螢幕擷取顯示&#x200B;**[!UICONTROL 清單檢視]**）中，開啟包含您已發佈或未發佈之資產的檔案夾。
1. 選取資產，以便以勾號顯示。 請參閱以下螢幕擷取範例。
1. 在頁面左上角附近，從下拉式選單中選擇&#x200B;**[!UICONTROL 時間軸]**。 左側面板中的&#x200B;**[!UICONTROL Status]**區域會顯示所選資產的發佈狀態。
當您使用**[!UICONTROL 清單檢視]**&#x200B;時，會出現&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;發佈狀態的額外欄。
   * 配置為與Dynamic Media同步的資料夾預設顯示&#x200B;**[!UICONTROL Dynamic Media]**&#x200B;列。
   * 配置為與Dynamic Media同步的&#x200B;*not*資料夾不顯示Dynamic Media列。
      ![清單檢視和時間軸](/help/assets/assets-dm/selective-publish-status-timeline.png)

## 疑難排解選擇性發佈{#selective-publish-troubleshoot}

未同步至Dynamic Media但在其上觸發Dynamic Media發佈動作的資產會產生下列錯誤訊息和解決方案：

![選擇性發佈錯誤](/help/assets/assets-dm/selective-publish-error.png)
