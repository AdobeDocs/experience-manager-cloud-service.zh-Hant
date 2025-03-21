---
title: ' [!DNL Experience Manager Assets] 中的協助工具'
description: 瞭解 [!DNL Adobe Experience Manager] as a [!DNL Cloud Service] 中的協助工具功能如何協助殘障使用者。
contentOwner: AG
feature: Accessibility, Asset Management
role: User, Architect, Leader
exl-id: a6d24ba6-3cb1-42cb-9942-f78572c93358
source-git-commit: 188f60887a1904fbe4c69f644f6751ca7c9f1cc3
workflow-type: tm+mt
source-wordcount: '1969'
ht-degree: 3%

---

<!--
Possible topics to cover in this article are below.

* Compile a list of enhancements done in the last ~1 year.
* Showcase a few prominent use cases (search?) in a screencast.
* Top-level actions supported, such as clickable UI elements, keyboard shortcuts, pop-up dialogs, and so on.
* List all UIs that are keyboard navigable.
* Unified list of the product tasks supported, such as, search assets, download assets, add or editing metadata, use DM Viewers, and so on.
* Do we need to add support matrix of user tasks with browser and screen reader combinations. Everything may not work in all browsers and/or using all screen readers.
* Any exceptions that users should be aware of. It may help to call out (it may be done in ACR) what tasks are NOT supported.
* CTAs – what's next and more info from the team:
  * Link to ACRs on a.com.
  * Generic a11y info by Adobe to begin with.
  * Link to a11y-specific online methods to report issues, seek support, or request enhancements, if any. Asked the a11y team on Slack.
-->

# [!DNL Adobe Experience Manager Assets] as a [!DNL Cloud Service]中的協助工具功能 {#accessibility-in-aem-assets}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets與Edge Delivery Services整合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI擴充性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>啟用Dynamic Media Prime和Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜尋最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/metadata-best-practices.md"><b>中繼資料最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開發人員文件</b></a>
        </td>
    </tr>
</table>

[!DNL Adobe Experience Manager]可讓內容建立者和發佈者在網站上提供令人驚豔的體驗。 Adobe致力於改善[!DNL Experience Manager]的無障礙功能，以吸引身心障礙的創作者。 本軟體持續強化，以符合各類使用者的需求，並符合全球標準，包括視覺、聽覺、行動力或其他殘疾人士。

[!DNL Experience Manager]會發佈符合性資訊，說明其遵循的標準、概述產品中的協助工具功能，以及符合性等級。 協助工具符合性報告可協助[!DNL Experience Manager]使用者瞭解各項標準的遵守程度。 在[!DNL Assets]中完成的增強功能可讓所有使用者透過鍵盤、熒幕閱讀器、放大鏡和其他輔助技術輕鬆使用介面。

[!DNL Experience Manager]為下列標準提供不同等級的支援：

* [網頁內容可及性指引(WCAG) 2.1](https://www.w3.org/TR/WCAG/)。
* [修訂修復法案的第508節](https://www.access-board.gov/guidelines-and-standards/communications-and-it/about-the-ict-refresh/final-rule/text-of-the-standards-and-guidelines)。
* [協助工具計畫 — 由W3C](https://www.w3.org/WAI/standards-guidelines/aria/)協助工具的Rich Internet Applications (WAI-ARIA)。
* [EN 301 549](https://en.wikipedia.org/wiki/EN_301_549)。

若要閱讀包含詳細相容性層級的報表，請參閱[協助工具相容性報表](https://www.adobe.com/accessibility/compliance.html) (ACR)頁面。

<!-- TBD: Add link after release.
To know how [!DNL Dynamic Media] is accessible, see [accessibility in [!DNL Dynamic Media]](). 
-->

## 輔助技術 {#at-support}

殘障使用者經常依賴硬體與軟體來存取網頁內容及使用軟體產品。 這些工具稱為輔助技術。 使用軟體的核心功能時，[!DNL Experience Manager Assets]可以使用下列型別的輔助技術(AT)：

* 熒幕助讀程式和熒幕放大鏡。
* 語音辨識軟體。
* 鍵盤使用方式 — 導覽和捷徑。
* 輔助硬體，包括開關控制項、可重新整理的點字顯示器，以及其他電腦輸入裝置。
* UI放大工具。

## [!DNL Experience Manager Assets]個可存取的使用案例 {#accessible-assets-use-cases}

在[!DNL Experience Manager]中，協助工具功能可滿足[!DNL Experience Manager]使用者及其客戶的兩個主要需求。

* 對於內容設計人員和建立者而言，有建立及發佈無障礙內容的功能，可依次供其客戶和網站訪客使用。 在輔助技術的協助下，內容可供殘障人士使用。 如需詳細資訊，請參閱[網頁協助工具准則](/help/compliance/accessibility/quick-guide-wcag.md)。
* [!DNL Experience Manager]也可讓身心障礙的使用者和管理員存取使用者介面和控制項，以建立和管理內容。 殘障人士可使用輔助技術瀏覽、使用及管理[!DNL Assets]功能。

[!DNL Assets]中的核心功能比以前更容易存取，並且會定期更新以符合全球標準。 [!DNL Assets]中的CRUD作業具有某種內建的協助工具。 DAM工作流程例如新增、管理、搜尋和分發資產，都可透過鍵盤快速鍵、熒幕助讀程式文字、顏色對比等協助進行存取。

## 支援使用鍵盤 {#keyboard-use}

許多可使用指標點選或操作的使用者介面元素，也可以使用鍵盤來配合。 使用鍵盤時，使用者可專注於UI元素並採取適當的動作。 使用者可以直接使用鍵盤快速鍵來觸發命令或動作，而無需專注於UI元素並使用鍵盤來觸發。 例如，使用者可以使用鍵盤瀏覽至使用者介面控制項，並選取`Return`，然後選取`Alt + 2`鍵盤快速鍵，來開啟左側資產的時間軸。

<!-- TBD items:

* The button/menu to toggle between list view and card view exposes relevant info to the screen readers. What about column view option? This info can go into 'basic handling' info aka article to 'understand and use the workspace'.
* How to open and browse through the profile pop-up dialog in [!DNL Experience Manager] UI using a keyboard? The navigation does not match the order of visual display of options on the UI. This info can go into 'basic handling' info aka article to 'understand and use the workspace'. What about setting preferences and impersonating a user?
* Using the [!DNL Experience Manager] tag browser and operating the buttons like delete tag? This info can go into 'basic handling' info aka article to 'understand and use the workspace'.
* Read-only form fields can be focused with the keyboard. Can users tab to these fields to understand the contents and are they able to copy text from the fields?
-->

### [!DNL Assets]中的鍵盤快速鍵 {#keyboard-shortcuts}

[!DNL Assets]中的下列動作可搭配列出的鍵盤快速鍵使用。 大部分套用至[!DNL Experience Manager]主控台的鍵盤快速鍵也套用至[!DNL Assets]。 請參閱主控台](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md)的[鍵盤快速鍵。 瞭解如何[啟用或停用鍵盤快速鍵](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md)。

| 使用者介面或情境 | 鍵盤快速鍵 | 動作 |
|---|---|---|
| [!DNL Assets]使用者介面中的資料行檢視 | 向上鍵與向下鍵 | 導覽至相同階層內的檔案和資料夾。 |
| [!DNL Assets]使用者介面中的資料行檢視 | 向左鍵和向右鍵 | 導覽至目前資料夾上方或下方的檔案和資料夾。 |
| 瀏覽[!DNL Assets]中的資料夾 | `/` | 透過開啟Omnisearch方塊叫用搜尋。 |
| [!DNL Assets]主控台 |  | 切換邊欄 |
| [!DNL Assets]主控台 | `Alt + 1` | 開啟內容樹狀結構。 |
| [!DNL Assets]主控台 | `Alt + 2` | 開啟[!UICONTROL 導覽]左側邊欄。 |
| [!DNL Assets]主控台 | `Alt + 3` | 顯示選取資產的[!UICONTROL 時間表]。 |
| [!DNL Assets]主控台 | `Alt + 4` | 開啟所選資產的即時副本參考。 |
| [!DNL Assets]主控台 | `Alt + 5` | 叫用選取資料夾中的搜尋和搜尋。 |
| 已選取資產或資料夾 | 退格鍵 | 刪除選取的資產或資料夾。 |
| 已選取資產或資料夾 | `p` | 開啟所選資產的「屬性」頁面。 |
| 已選取資產或資料夾 | `e` | 編輯選取的資產。 |
| 已選取資產或資料夾 | `m` | 移動選取的資產。 |
| 已選取資產或資料夾 | `Ctrl + c` | 複製選取的資產。 |
| 已選取資產或資料夾 | `Esc` | 取消選取。 |
| 對話方塊開啟，並位於焦點中 | `Esc` | 關閉對話方塊。 |
| 在DAM的資料夾內 | `Ctrl + v` | 貼上複製的資產。 |
| [!DNL Assets]主控台 | `Ctrl + A` | 選取所有資產。 |
| 資產屬性頁面 | `Ctrl + S` | 儲存變更。 |
| [!DNL Assets]主控台 | `?` | 請參閱鍵盤快速鍵清單。 |

## 登入並導覽[!DNL Assets]使用者介面 {#login}

使用者可使用鍵盤導覽並填寫登入欄位以進行登入。 每次發生錯誤時，熒幕助讀程式都會通知由於登入頁面上錯誤的使用者名稱和密碼組合所導致的錯誤訊息。

登入後，DAM使用者可以使用鍵盤在[!DNL Assets]使用者介面中導覽。 使用者介面元素（如左側邊欄、功能表、使用者設定檔、搜尋列、檔案和資料夾以及管理和組態設定）可使用鍵盤瀏覽。 鍵盤導覽順序為由左至右、由上至下。 使用鍵盤導覽時，聚焦時可操作的選項會以較佳的色彩對比強調顯示，並由熒幕助讀程式提供旁白。 適當時，熒幕助讀程式會宣告功能表中焦點選項的狀態，例如展開、收合及混合狀態。 此外，熒幕助讀程式會宣佈可操作選項的用途，而不是外觀或UI位置。

如果使用者從功能表展開說明或使用者設定檔選項，熒幕助讀程式會宣告適當的選項或狀態。 如果使用者展開使用者設定檔選項，則可使用鍵盤選取可用的選項。 例如，管理員可以模擬其他使用者。 如果使用者從[!UICONTROL 說明]選項中搜尋字串，解說員會宣佈「搜尋說明」以表示搜尋正在進行中。

<!-- TBD: Removing for now. Add a more informative video later. Host it on tv.adobe

![Keyboard navigation of top options in [!DNL Experience Manager] user interface](assets/keyboard-navigation-in-aem.gif)

*Figure: Navigating through the options at the top of [!DNL Experience Manager] user interface using `Tab` key.*
-->

## 瀏覽資產並檢視相關資訊 {#browse}

在[!DNL Assets]使用者介面中，使用者可以使用鍵盤來瀏覽DAM存放庫中現有數位資產清單、預覽或下載資產、檢視產生的轉譯、切換檢視、檢視產生的轉譯、檢視時間軸和版本記錄、檢視註釋和參考，以及檢視和管理中繼資料。

<!-- TBD: Not sure about the following list items mean:

In [!DNL Experience Manager] header section, when navigating in browse mode, screen reader now announces,
  
  * Suggestions to search in Omnisearch.
  * The state as expanded or collapsed for Solutions, Help, Inbox and User options.
  * The Searching Help status message that is displayed when user enters a search string in Search for Help field under Help option
  * The error message if incorrect value is entered in Impersonate as field under User option and focus correctly moves to the text field (NPR-33804).

Review CQ-4282133 before adding - Close button in a coral-dialog box was not accessible through keyboard, due to which user cannot trigger close button through keyboard press in version preview dialog. After fix, user can close dialog through close button using keyboard.

* CQ-4273122 - Assets of video/audio type will have aria-label in format "Multimedia player: <Title>" so users relying on screen-reader will get to know that they are video/audio assets.
-->

瀏覽資產存放庫時，以下功能可改善協助工具：

* 熒幕助讀程式會朗讀描述圖示用途或功能的替代文字，而非圖示名稱。
* 使用者可使用鍵盤按鍵存取和聚焦資產參考清單中的互動式使用者介面選項。
* 清單檢視中每一列的元素會由熒幕助讀程式宣告為相同列的元素。
* 使用`Tab`鍵導覽時，焦點可以在版本預覽中移至關閉選項。
* 使用鍵盤瀏覽時，反白顯示的可操作使用者介面選項具有更突出的視覺焦點，並增強對比。 這可讓使用者更容易識別重點區域。
* 使用`Esc`鍵從縮圖檢視中移除快速動作圖示並不會從最後一個焦點專案移除鍵盤焦點。
* 選取資產後，選取`Alt + 4`鍵盤快速鍵會開啟左側邊欄中的[!UICONTROL 參考]清單。 使用`Tab`鍵，使用者可以瀏覽非零參考專案。 僅瀏覽非零參照專案，可節省工作量和按鍵動作。
* 資產時間軸中提供資產上的註解。 若使用鍵盤或鍵盤快速鍵存取左側邊欄，即可存取。
* [!DNL Experience Manager]中的[!UICONTROL 檢視設定]可使用鍵盤存取。 使用者可以使用方向鍵瀏覽可用的卡片大小，並選取和Tab鍵瀏覽，以瀏覽和設定現有「檢視設定」檢視中的其他元素。

<!-- TBD: Gradually, as more enhancements are done in these categories, add more content.

## Add and upload digital assets {#upload}

## Configure and administer [!DNL Assets] {#config-admin}

* List the a11y fixes in workflows to configure and administer [!DNL Experience Manager Assets]?
* Some enhancements in Processing profiles creation or application to a folder?
* Some enhancements to metadata properties UI?
-->

## 管理數位資產 {#manage-assets}

許多資產管理任務（例如CRUD操作、下載資產、新增中繼資料）都可不同程度的存取。 [!DNL Assets]可讓您使用各種輔助技術完成工作，特別是熒幕閱讀器和鍵盤。

觀看如何使用鍵盤來[瀏覽存放庫並下載資產](https://youtu.be/K3dgqMRQJys)的影片示範。

對於通常由行銷人員和管理員等角色完成的中繼資料操作，以下功能可改善協助工具：

* 現在可以使用鍵盤存取資產[!UICONTROL 屬性]頁面上的[!UICONTROL 儲存並關閉]選項。
* 熒幕助讀程式會朗讀在資產[!UICONTROL 屬性]的[!UICONTROL 基本]索引標籤中刪除選取的標籤的選項。
* 使用者可以使用鍵盤的「日期選擇器」彈出式對話方塊。 日期選擇器使用者介面元素可用來設定開啟時間和關閉時間，並選取日期。
* 使用鍵盤的拖曳功能在熒幕朗讀程式的瀏覽模式中，可在[!UICONTROL 中繼資料結構編輯器]中正確運作。
* 使用者可以使用鍵盤將焦點移至資料夾[!UICONTROL 屬性]的[!UICONTROL 許可權]索引標籤中[!UICONTROL 已關閉的使用者群組]下的[新增使用者或群組]欄位。

## 搜尋數位資產 {#search-assets}

快速且順暢的資產搜尋體驗可加快內容速度。 內容Velocity使用案例是核心[!DNL Assets]功能的一部分。 若要從Omnisearch列開始搜尋，使用者可以使用鍵盤快速鍵`/`或搭配熒幕助讀程式使用`Tab`來快速找到搜尋選項。 當焦點在搜尋選項![搜尋選項](assets/do-not-localize/search_icon.png)上時，熒幕助讀程式會將選項名稱旁白為「搜尋按鈕」。 使用者可以選取`Return`以開啟Omnisearch方塊。 熒幕助讀程式不僅會提供在搜尋方塊中輸入之關鍵字的旁白，也會提供[!DNL Experience Manager Assets]所提供之建議的旁白。 使用者可以使用方向鍵、`Return`和`Tab`的組合來存取各種選項以觸發搜尋。

搜尋功能可透過下列功能存取：

* 頁面標題（可供熒幕助讀程式使用）有助於將頁面識別為資產的搜尋頁面。
* 使用者可在Omnisearch欄位內搜尋資產。 使用者可以使用鍵盤導覽或鍵盤快速鍵`/`來開啟它。
* 使用者可以開始輸入搜尋關鍵字，然後使用方向鍵選取自動建議。 可使用`Return`索引鍵選取醒目提示的建議，並搜尋資產以尋找選取的建議。
* 熒幕助讀程式可以在篩選搜尋結果時，在「篩選器」面板中識別並朗讀混合狀態核取方塊（除非您選取所有巢狀述詞，否則不會選取並刪除第一層核取方塊）。
* 關閉Omnisearch方塊後，使用者焦點會移至搜尋選項。

篩選搜尋結果時：

* 搜尋結果頁面有一個資訊性的標題，可讓使用者更瞭解熒幕助讀程式。
* 熒幕助讀程式會朗讀搜尋篩選器中的選項，作為可展開的摺疊式功能表。
* 熒幕助讀程式會朗讀具有混合狀態選項的述詞。

## 共用資產 {#share-assets}

<!-- TBD: Anything about accessibility in DA, BP? AAL team confirmed that there's no content for AAL a11y on helpx.
-->

共用資產時，下列功能可改善協助工具：

* 使用者可以使用鍵盤在連結共用對話方塊中的搜尋和新增電子郵件位址列位中移動焦點。

* 在連結共用對話方塊中，以瀏覽模式導覽時，熒幕助讀程式會

   * 請勿在對話方塊載入後立即提供表格資訊旁白。
   * 可瀏覽至列出的所有建議。
   * 提供旁白來敘述新增電子郵件地址和搜尋欄位顯示的建議。

## 無障礙檔案 {#accessible-docs}

[!DNL Experience Manager]提供無障礙說明檔案，以供身心障礙人士使用。 以下內容有助於讓內容立即可供存取，同時Adobe會繼續改善範本和內容：

* 熒幕助讀程式可以閱讀文字。
* 影像和插圖有可用的替代文字。
* 可以使用鍵盤導覽。
* 對比率有助於強調說明檔案網站的某些部分。

**另請參閱**

* [翻譯資產](translate-assets.md)
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
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

## 提供回饋意見 {#a11y-feedback}

若要提供與協助工具相關的意見回饋、詢問問題並請求產品增強功能，請使用下列方法：

* 在[www.adobe.com/accessibility/feedback.html](https://www.adobe.com/accessibility/feedback.html)填寫表單。
* 寄電子郵件給我們：access@adobe.com。

>[!MORELIKETHIS]
>
>* [每個版本中完成的增強功能的發行說明](/help/release-notes/release-notes-cloud/release-notes-current.md)。
>* [[!DNL Adobe Experience Manager] 協助工具指引](/help/compliance/accessibility/web-accessibility.md)。
>* [Adobe解決方案的一致性報告(ACR)和VPAT清單](https://www.adobe.com/accessibility/compliance.html)。
