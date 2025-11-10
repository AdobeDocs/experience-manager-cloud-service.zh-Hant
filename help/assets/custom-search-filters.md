---
title: 自訂搜尋篩選器
description: 瞭解如何自訂搜尋篩選器表單
role: User, Leader, Developer
exl-id: 383e8165-439e-447b-a19d-d5446238a13f
source-git-commit: 836805b4eac5ab940dff5c66ec0dcf1ca8652837
workflow-type: tm+mt
source-wordcount: '1425'
ht-degree: 12%

---


# 自訂搜尋篩選器 {#customize-search-filters}

搜尋篩選器可讓您根據各種引數（例如日期、檔案型別、標籤和相關性）來縮小搜尋結果，從而提高搜尋查詢的精確度。 透過套用篩選器，您可以快速篩選出最相關的結果。 這不僅可節省時間，還能根據特定偏好和需求定製結果，進而改善整體搜尋體驗。
檢視有關[搜尋](search-assets-view.md)的更多資訊。

自訂搜尋篩選器AEM Assets只能對應至您的可搜尋屬性索引中的專案。 在設定自訂篩選器體驗之前，請確定包含任何自訂中繼資料。 [!DNL Assets view]協助自訂搜尋篩選器，以簡化搜尋程式。 若要自訂AEM Assets自訂搜尋篩選器，請執行以下步驟：

1. 瀏覽至&#x200B;**[!UICONTROL 設定]** > **[!UICONTROL 一般設定]** > **[!UICONTROL 搜尋]**。

   <!--1. Go to the **[!UICONTROL Search]** tab. Click **[!UICONTROL Customize]** to configure your search form.-->

   ![自訂搜尋篩選設定](assets/custom-search-filter.png)

1. 在&#x200B;**[!UICONTROL 篩選器]**&#x200B;區段中，您可以設定下列專案：

   * **[!UICONTROL 檔案]：**&#x200B;設定檔案涉及檔案型別、檔案格式、資產狀態、檔案大小、影像尺寸、建立日期、修改日期等。
   * **[!UICONTROL 資料夾]：**&#x200B;設定資料夾涉及建立日期、捨棄日期、捨棄者等等。
   * **[!UICONTROL 集合]：**&#x200B;設定集合涉及集合可見性、集合型別、建立日期等。

1. 您可以預覽檔案、資料夾或集合可用的預設&#x200B;**[!UICONTROL 預設篩選器]**&#x200B;表單。 然而，您無法自訂或刪除此預先存在的表單。 或者，若要建立自訂的篩選表單，請按一下&#x200B;**[!UICONTROL 新增表單]**。

   >[!NOTE]
   >
   >每個類別（檔案、資料夾或集合）只能建立一個自訂的篩選表單。

1. 按一下「**[!UICONTROL 儲存]**」以儲存變更。

## 已設定表單上的動作 {#Actions-on-configured-form}

您可以在已設定的篩選表單上使用下列動作：

* **[!UICONTROL 自訂]：**&#x200B;按一下以新增或修改表單。 您可以將[自訂篩選器](#available-custom-filters)中的篩選器元素拖放到畫布上，或視需要重新排序。

* **[!UICONTROL 預覽]：**&#x200B;按一下以檢閱變更。

* **[!UICONTROL 設定為預設值]：**&#x200B;按一下以將選取的表單設定為您的預設值。

* **[!UICONTROL 刪除表單]：**&#x200B;按一下更多選項![更多選項](assets/do-not-localize/more-icon.svg)並選取&#x200B;**[!UICONTROL 刪除表單]**&#x200B;以刪除選取的篩選表單。

* **[!UICONTROL 編輯表單標籤]：**&#x200B;按一下更多選項![更多選項](assets/do-not-localize/more-icon.svg)，並將新的標籤和說明新增至自訂的篩選表單。

  ![編輯表單標籤](assets/edit-form-labels.png)

## 可用的自訂篩選器 {#available-custom-filters}

Assets檢視提供下列可依需求重新配置的自訂篩選器：

* [篩選元素](#filter-elements)
* [預先設定的篩選器](#preconfigured-filters)

### 篩選元素 {#filter-elements}

自訂篩選器AEM Assets可讓您在自訂搜尋篩選器畫布上使用篩選器元素的集合。 這些元素會根據搜尋屬性屬性的可用性來重新配置。 不過，您可以根據自己的需求自訂[篩選器屬性](#filter-properties)。 [!DNL Assets view]中有以下篩選元素：

<table>
    <tr>
        <th>篩選元素</th>
        <th>說明</th>
        <th>屬性</th>
    </tr>
    <tr>
        <td>文字</td>
        <td>文字欄位是輸入區域，您可以在其中輸入與篩選器相關的資訊。</td>
        <td>
            <ul>
                <li>標籤
                <li>後設資料
                <li>值
                <li>說明
            </ul>
        </td>
    </tr>
    <tr>
        <td>選項</td>
        <td>選項是指從清單中選取偏好專案的可用替代方案。</td>
        <td>
            <ul>
                <li>標籤
                <li>後設資料
                <li>值
                <li>選項
                <li>說明
            </ul>
        </td>
    </tr>
    <tr>
        <td>布林值</td>
        <td>布林值代表一個True值。 您可以將其用於特定位置，以選擇其中一個選項。</td>
        <td>
            <ul>
                <li>標籤
                <li>後設資料
                <li>說明
            </ul>
        </td>
    </tr>
    <tr>
        <td>數字</td>
        <td>使用此篩選元素來表示數值。</td>
        <td>
            <ul>
                <li>標籤
                <li>後設資料
                <li>選擇類型
                <li>步進器
                <li>步進器值
                <li>說明
            </ul>
        </td>
    </tr>
    <tr>
        <td>下拉式清單</td>
        <td>在選項清單中顯示的各種選項中進行選擇。</td>
        <td>
            <ul>
                <li>標籤
                <li>後設資料
                <li>選項
                <li>值
                <li>說明
            </ul>
        </td>
    </tr>
    <tr>
        <td>日期</td>
        <td>用於指定日期。</td>
        <td>
            <ul>
                <li>標籤
                <li>後設資料
                <li>選擇類型
                <li>說明
            </ul>
        </td>
    </tr>
    <tr>
        <td>路徑瀏覽器</td>
        <td>用於瀏覽Experience Manager存放庫中的檔案或資料夾。</td>
        <td>
            <ul>
                <li>標籤
                <li>後設資料
                <li>路徑總管
                <li>說明
            </ul>
        </td>
    </tr>
    <tr>
        <td>標記</td>
        <td>用於從可用選項中選取標籤。 標籤提供有關資產的更具體資訊，並增強其可發現性。 已套用至所選資產的標籤會顯示在<b>屬性</b>面板中。 如果您將標籤儲存在自訂中繼資料屬性上，並使用根路徑將其限製為階層，則可以在搜尋篩選器中利用相同的設定。 如果您找不到相關標籤，請建立這些標籤，並將其指派給選取的資產。 如需建立和指派標籤給資產的詳細資訊，請參閱Assets檢視<a href = "tagging-management-assets-view.md">中的</a>管理標籤。</td>
        <td>
            <ul>
                <li>標籤
                <li>後設資料
                <li>標籤選取器
                <li>說明
            </ul>
        </td>
    </tr>
    <tr>
        <td>使用者</td>
        <td>用於指定管理員、一般和消費者使用者之間的使用者型別。</td>
        <td>
            <ul>
                <li>標籤
                <li>後設資料
                <li>說明
            </ul>
        </td>
    </tr>
</table>

### 預先設定的篩選器 {#preconfigured-filters}

預先設定的濾鏡是預設設定，可讓您直接在畫布上使用它們。 不過，您可以根據自己的需求自訂[篩選器屬性](#filter-properties)。 已在[!DNL Assets view]中預先設定下列篩選器：

<table>
    <tr>
        <th>預先設定的篩選器</th>
        <th>說明</th>
        <th>屬性</th>
    </tr>
    <tr>
        <td>檔案類型</td>
        <td>依支援的檔案型別篩選搜尋結果，包括「影像」、「檔案」和「影片」。</td>
        <td>
            <ul>
                <li>標籤
                <li>後設資料
                <li>選擇類型
                <li>選項
                <li>值
                <li>說明
            </ul>
        </td>
    </tr>
    <tr>
        <td>檔案格式</td>
        <td>Assets檢視支援任何二進位檔案格式和基本服務，例如儲存、上傳、複製、移動、刪除和新增中繼資料。</td>
        <td>
            <ul>
                <li>標籤
                <li>後設資料
                <li>選擇類型
                <li>說明
            </ul>
        </td>
    </tr>
    <tr>
        <td>影像大小</td>
        <td>提供一個或多個最小和最大尺寸，以篩選影像。 以尺寸 (像素) 提供大小，而非影像的檔案大小。</td>
        <td>
            <ul>
                <li>標籤
                <li>後設資料
                <li>選擇類型
                <li>步進器
                <li>步進器值
                <li>說明
            </ul>
        </td>
    </tr>
    <tr>
        <td>影像寬度</td>
        <td>影像的垂直尺寸。</td>
        <td>
            <ul>
                <li>標籤
                <li>後設資料
                <li>選擇類型
                <li>步進器
                <li>步進器值
                <li>說明
            </ul>
        </td>
    </tr>
    <tr>
        <td>影像高度</td>
        <td>影像的水準尺寸。</td>
        <td>
            <ul>
                <li>標籤
                <li>後設資料
                <li>選擇類型
                <li>步進器
                <li>步進器值
                <li>說明
            </ul>
        </td>
    </tr>
    <tr>
        <td>建立日期</td>
        <td>建立資產的日期範圍。</td>
        <td>
            <ul>
                <li>標籤
                <li>後設資料
                <li>選擇類型
                <li>說明
            </ul>
        </td>
    </tr>
    <tr>
        <td>修改日期</td>
        <td>修改資產的日期範圍。</td>
        <td>
            <ul>
                <li>標籤
                <li>後設資料
                <li>選擇類型
                <li>說明
            </ul>
        </td>
    </tr>
    <tr>
        <td>資產狀態</td>
        <td>Assets檢視可讓您對存放庫中可用的資產設定狀態。 設定資產狀態以更有效地控管和管理下游的數位資產消耗。 從<b>已核准、已拒絕或無狀態</b>中選擇。</td>
        <td>
            <ul>
                <li>標籤
                <li>後設資料
                <li>選擇類型
                <li>說明
            </ul>
        </td>
    </tr>
    <tr>
        <td>智慧標記</td>
        <td>使用Experience Manager存放庫中新增的智慧標籤來篩選資產。</td>
        <td>
            <ul>
                <li>標籤
                <li>後設資料
                <li>選擇類型
                <li>Delimeter支援
                <li>說明
            </ul>
        </td>
    </tr>
    <tr>
        <td>動態媒體狀態</td>
        <td>選擇介於已發佈或未發佈之間的資產狀態。</td>
        <td>
            <ul>
                <li>標籤
                <li>後設資料
                <li>選擇類型
                <li>選項
                <li>值
                <li>說明
            </ul>
        </td>
    </tr>
    <tr>
        <td>過期日期</td>
        <td>篩選資產，指定不再有效或需要的資產日期範圍。 </td>
        <td>
            <ul>
                <li>標籤
                <li>後設資料
                <li>選擇類型
                <li>說明
            </ul>
        </td>
    </tr>
    <tr>
        <td>標記 (分類法)</td>
        <td>此系統使用標籤來組織和分類數位資產，本質上建立關鍵字的階層結構，讓使用者可藉由套用特定標籤至每個資產來輕鬆搜尋和尋找相關內容。 </td>
        <td>
            <ul>
                <li>標籤
                <li>後設資料
                <li>標籤選取器
                <li>說明
            </ul>
        </td>
    </tr>
</table>

#### 篩選器屬性 {#filter-properties}

每個篩選元素都與一組屬性相關聯。 AEM Assets自訂搜尋篩選器在篩選器和預先設定的元素中使用以下屬性：

<table>
    <tr>
        <th>屬性</th>
        <th>值</th>
        <th>說明</th>
    </tr>
    <tr>
        <td>標籤</td>
        <td>文字</td>
        <td>這是您使用之篩選器的識別碼。</td>
    </tr>
    <tr>
        <td>後設資料</td>
        <td>下拉式清單</td>
        <td>中繼資料屬性是用來對應來自Adobe Experience Manager Assets存放庫的已核准中繼資料。 您可以從下拉式選單中選擇需要與篩選元素對應的中繼資料值。 </td>
    </tr>
    <tr>
        <td>選擇類型</td> 
        <td>單一、多個、精確或範圍 </td>
        <td>
            <ul>
                <li><b>單一選取範圍</b>允許一次選擇一個專案，這非常適合不同的選擇。
                <li><b>多個選取專案</b>允許同時選擇多個專案，這對於選取多個選項很有用。 
                <li><b>完全選取</b>可讓您從各種選項中選擇精確的單一專案。
                <li><b>範圍選取</b>允許選擇定義範圍內的連續值集，適合用來選取日期或數值範圍。
            </ul>
        </td>   
    </tr>
    <tr>
        <td>選項</td>
        <td>手動、JSON路徑或CSV上傳</td>
        <td>
            <ul>
                <li>如果要手動新增選項，請選擇<b>手動</b>。 
                <li>選擇<b>JSON路徑</b>以從JSON檔案新增選項。 
                <li>選擇<b>CSV上傳</b>以匯入包含要新增至選項的值的CSV檔案。
            </ul>
        </td>
    </tr>
    <tr>
       <td>值</td>
        <td>新增或編輯</td>
        <td>
        <ul>
        <li>按一下<b>新增</b>以新增值。 
        <li>按一下<span>✎</span>以編輯標籤。 
        <li>按一下<span>??</span>刪除選項值。 
        <li>按一下<b>編輯</b>以修改編輯選項。 
        <li>您也可以透過保留選項來變更選項的順序。
        </td>
    </tr>
    <tr>
        <td>Delimeter支援</td>
        <td>啟用或停用</td>
        <td>分隔符號是用來分隔文字中不同元素的符號。 例如逗號、空格或分號。</td>
    </tr>
    <tr>
        <td>步進器</td>
        <td>值</td>
        <td>啟用「數字」欄位的「步進器」按鈕，在每次按一下時遞增或遞減值。 </td>
    </tr>
    <tr>
        <td>步進器值 </td>
        <td>數字</td>
        <td>它表示使用步進器按鈕時的增量/減量值。 它會在步進器啟用時顯示。</td>
    </tr>
    <tr>
        <td>說明</td>
        <td>文字</td>
        <td>新增詳細說明，以提供有關篩選元素的其他資訊。</td>
    </tr>
</table>

>[!VIDEO](https://video.tv.adobe.com/v/3443080)

## 刪除篩選元素 {#delete-a-filter-element}

若要刪除搜尋篩選器，請依照下列步驟執行：

1. 瀏覽至「**[!UICONTROL 設定]**」>「**[!UICONTROL 一般設定]**」。
1. 前往&#x200B;**[!UICONTROL 搜尋]**&#x200B;標籤。 按一下&#x200B;**[!UICONTROL 自訂]**&#x200B;設定您的搜尋表單。
1. [!UICONTROL 設定篩選器]表單出現。 確保您處於編輯模式，以便您可以在範本中進行修改。
1. 選取您要刪除的篩選元素。 例如，選取&#x200B;**[!UICONTROL 影像高度]**。
1. 按一下&#x200B;**[!UICONTROL 刪除類別]**&#x200B;以刪除篩選元素。 已從畫布移除&#x200B;**[!UICONTROL 影像高度]**&#x200B;元素。
1. 按一下&#x200B;**[!UICONTROL 確認]**&#x200B;以儲存表單。

## 使用自訂搜尋篩選器{#using-custom-search-filters}

設定搜尋篩選器後，您可以使用篩選器在存放庫中搜尋資產。

![使用自訂搜尋篩選器](assets/using-custom-search-filters.png)

>[!MORELIKETHIS]
>
>* [搜尋資產](search-assets-view.md)
