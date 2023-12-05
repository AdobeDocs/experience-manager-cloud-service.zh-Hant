---
title: 預覽資產
description: 瞭解如何在Dynamic Media中預覽資產，以便檢視客戶在自己的網頁瀏覽器中如何檢視資產。
contentOwner: Rick Brough
feature: Asset Management
role: User
exl-id: 3928798d-352a-42a8-a544-7104fc9b3cf1
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 1%

---

# 預覽資產{#previewing-assets}

您可以使用「預覽」，檢視客戶在自己的Web瀏覽器中檢視您上傳的數位資產時，該資產會如何顯示。 指派給資產的預設內嵌跨裝置檢視器會用於預覽。

檢視器是各種設定或「預設集」的集合。 例如，檢視器的顯示大小、縮放行為、色彩配置、邊框和字型，可決定使用者在其電腦熒幕和行動裝置上檢視多媒體資產的方式。

除了針對視訊、迴轉集及影像集使用專用的預覽功能外，您也可以使用您建立的檢視器預設集來預覽資產。 或者，使用影像預設集來預覽影像的轉譯。

* [套用影像預設集](/help/assets/dynamic-media/image-presets.md)
* [套用檢視器預設集](/help/assets/dynamic-media/viewer-presets.md)

>[!NOTE]
>
>當您在Adobe Experience Manager的網頁（網站）上時，無法預覽資產 **[!UICONTROL 編輯]** 模式。 請改為選取「 」，以前往「預覽」模式 **[!UICONTROL 預覽]** 位於頁面的右上角。

若要在使用者介面中啟用或停用檢視器預設集，請參閱 [管理檢視器預設集](/help/assets/dynamic-media/managing-viewer-presets.md).

**若要預覽資產：**

1. 從 **[!UICONTROL Experience Manager]**，位於 **[!UICONTROL 導覽]** 頁面，選取 **[!UICONTROL 資產]**，然後 **[!UICONTROL 檔案]** 以存取資產。
1. 在頁面的右上角附近，從 **[!UICONTROL 檢視]** 下拉式清單，選取 **[!UICONTROL 清單檢視]**.
1. （選用）使用 **[!UICONTROL 型別]** 欄，依您要預覽的型別排序資產。
1. 在 **[!UICONTROL 標題]** 欄中，選取您要預覽之資產的標題名稱（而非縮圖影像）。
1. 請根據您選取的資產型別，執行下列任一項作業：

   <table>
    <tbody>
      <tr>
      <td><strong>您選取的資產型別</strong><br /> </td>
      <td><strong>是否能夠預覽特定轉譯中的資產？</strong></td>
      <td><strong>是否能在特定檢視器中預覽資產？</strong></td>
      </tr>
      <tr>
      <td><p>3D</p> </td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>若要在維度檢視器中預覽3D資產</strong></p>
      <ul>
      <li>在頁面左上角附近，選取圖示以顯示下拉式清單。 選取 <strong>檢視者</strong> 從清單中，然後選取「維度」檢視器。</li>
      <li>若要將影像還原為原始的縮放地圖，請選取 <strong>重設</strong>.</li>
      <li>若要最大化顯示裝置上的檢視器，請選取 <strong>全熒幕</strong>.</li>
      </ul>
      <p><strong>導覽3D場景</strong></p>
      <ul>
      <li><p><strong>轉動您的3D攝影機</strong>  — 讓檢視畫面在3D場景和物件周圍環繞。</p> 滑鼠：按一下左鍵+拖曳。</p> 觸控熒幕：按下+拖曳。</p></li>
      <li><p><strong>平移相機</strong>  — 上下左右平移檢視。</p> 滑鼠：按一下滑鼠右鍵+拖曳。</p> 觸控熒幕：雙指按下+拖曳。</p></li>
      <li><p><strong>縮放相機</strong>  — 如果要在3D場景中移入和移出區域，請縮放相機。</p> 滑鼠：捲動滾輪。</p> 觸控熒幕：手指捏合。</p></li>
      <li><p><strong>重新將相機置中</strong>  — 讓檢視畫面在3D場景和物件周圍環繞。</p> 滑鼠：按兩下。</p> 觸控熒幕：雙選。</li></ul></td>
      </tr>
      <tr>
      <td><p>影像</p> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>預覽特定轉譯中的資產</strong></p>
        <ul>
        <li>在頁面左上角附近，選取圖示以顯示下拉式清單。 選取 <strong>轉譯</strong> 從清單中，選取您要預覽的特定轉譯。</li>
        </ul> <p><strong>若要在特定檢視器中預覽資產</strong></p>
        <ul>
        <li>在頁面左上角附近，選取圖示以顯示下拉式清單。 選取 <strong>檢視者</strong> 從清單中，選取您要套用至資產的檢視器。</li>
        </ul><p>使用 <strong>+</strong> 和 <strong>-</strong>圖示可分別增加或減少所選影像的縮放。 若要將影像還原為原始縮放，請選取 <strong>重設</strong>.<br>如果您在觸控熒幕上，請按兩下要以步驟放大影像。 當您達到最大縮放時，請再次連按兩下影像以重設縮放狀態。 拖移過影像以平移。</p> </td>
      </tr>
      <tr>
      <td>多媒體</td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>預覽特定轉譯中的資產</strong></p>
        <ul>
        <li>在頁面左上角附近，選取圖示以顯示下拉式清單。 選取 <strong>轉譯</strong> 從清單中，選取您要預覽的特定轉譯。</li>
        </ul><p>選取較高解析度的視訊轉譯進行預覽，可能會導致視訊顯示為截斷。 原因在於，轉譯預覽會顯示客戶看到的確切解析度，而且全都位在用於預覽的內嵌檢視器內容中。</p><p>在資產層級預覽最適化視訊集時，轉譯會分組到一個播放體驗中。 也就是說，最適化視訊的大小適合檢視，並在您的檢視裝置和連線速度環境下使用最佳解析度進行播放。<br /></p><p><strong>在特定檢視器中預覽資產</strong></p>
        <ul>
        <li>在頁面左上角附近，選取圖示以顯示下拉式清單。 選取 <strong>檢視者</strong> 從清單中，選取您要套用至資產的檢視器。</li>
        </ul> </td>
      </tr>
      <tr>
      <td>影像集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定檢視器中預覽資產</strong></p>
        <ul>
        <li>在頁面左上角附近，選取圖示以顯示下拉式清單。 選取 <strong>檢視者</strong> 從清單中，選取您要套用至資產的檢視器。</li>
        </ul> <p>使用 <strong>+</strong> 和 <strong>- </strong>圖示可分別增加或減少所選影像的縮放。 若要將影像還原為原始縮放，請選取 <strong>重設</strong>.<br /> 如果您在觸控熒幕上，請按兩下要以步驟放大影像。 當您達到最大縮放時，請再次連按兩下影像以重設縮放狀態。 拖移過影像以平移。</p></td>
      </tr>
      <tr>
      <td>迴轉集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定檢視器中預覽資產</strong></p>
        <ul>
        <li>在頁面左上角附近，選取圖示以顯示下拉式清單。 選取 <strong>檢視者</strong> 從清單中，選取您要套用至資產的檢視器。</li>
        </ul><p>使用 <strong>+</strong> 和 <strong>- </strong>圖示可分別增加或減少所選影像的縮放。 若要將影像還原為原始縮放，請選取 <strong>重設</strong>.<br /> 如果您在觸控熒幕上，請按兩下要以步驟放大影像。 當您達到最大縮放時，請再次連按兩下影像以重設縮放狀態。 拖移過影像以平移。</p> </td>
      </tr>
      <tr>
      <td>混合媒體集</td>
      <td>否</td>
      <td>是</td>
      <td><p><strong>在特定檢視器中預覽資產</strong></p>
        <ul>
        <li>在頁面左上角附近，選取圖示以顯示下拉式清單。 選取 <strong>檢視者</strong> 從清單中，選取您要套用至資產的檢視器。</li>
        </ul> <p>使用 <strong>+</strong> 和 <strong>- </strong>圖示可分別增加或減少所選影像的縮放。 若要將影像還原為原始縮放，請選取 <strong>重設</strong>.<br /> 如果您在觸控熒幕上，請按兩下要以步驟放大影像。 當您達到最大縮放時，請再次連按兩下影像以重設縮放狀態。 拖移過影像以平移。</p> </td>
      </tr>
      <tr>
      <td>傳送集</td>
      <td>否</td>
      <td>是</td>
      <td><strong>在特定檢視器中預覽資產</strong>
        <ul>
        <li>在頁面左上角附近，選取圖示以顯示下拉式清單。 選取您要套用至資產的檢視器。</li>
        </ul> </td>
      </tr>
      <tr>
      <td>360度影片<br /> </td>
      <td>是</td>
      <td>是</td>
      <td><p><strong>預覽特定轉譯中的資產</strong></p>
        <ul>
        <li>在頁面左上角附近，選取圖示以顯示下拉式清單。 選取 <strong>轉譯</strong>，然後選取您要預覽的轉譯。</li>
        </ul> <p><strong>若要在特定檢視器中預覽資產</strong></p>
        <ul>
        <li>在頁面左上角附近，選取圖示以顯示下拉式清單。 選取 <strong>檢視者</strong>，然後選取您要套用至資產的檢視器。</li>
        </ul> <p>使用 <strong>+</strong> 和 <strong>- </strong>圖示可分別增加或減少所選影像的縮放。 若要將影像還原為原始縮放，請選取 <strong>重設</strong>.<br /> 如果您在觸控熒幕上，請按兩下要以步驟放大影像。 當您達到最大縮放時，請再次連按兩下影像以重設縮放狀態。 拖移過影像以平移。</p> </td>
      </tr>
    </tbody>
    </table>
