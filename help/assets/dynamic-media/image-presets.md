---
title: 套用 Dynamic Media 影像預設集
description: 瞭解如何在Dynamic Media套用影像預設集。
contentOwner: Rick Brough
feature: Image Presets,Viewers,Renditions
role: User
exl-id: ad21b52e-594f-4421-9b5a-2382d032ec5a
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 10%

---

# 套用 Dynamic Media 影像預設集 {#applying-image-presets}

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

影像預設集可讓資產動態傳送不同大小、不同格式的影像，或以其動態產生的其他影像屬性傳送。 匯出時，您可以選擇預設集，將影像重新格式化為管理員已概述的規格。

此外，您可以選擇有回應的影像預設集（在選取後由&#x200B;**[!UICONTROL RESS]**&#x200B;按鈕指定）。

[管理員可以建立和設定影像預設集](managing-image-presets.md)。

>[!NOTE]
>
>智慧型影像可與您現有的影像預設集搭配使用。 它會在傳送的最後一毫秒內運用智慧，根據瀏覽器或網路連線速度進一步縮小影像檔案大小。 如需詳細資訊，請參閱[智慧型影像](imaging-faq.md)。

您可以在任何時候預覽影像時，將影像預設集套用至影像。

**若要套用Dynamic Media影像預設集：**

1. 開啟資產，然後在左側邊欄中選取下拉式清單，然後選取&#x200B;**[!UICONTROL 轉譯]**。

   >[!NOTE]
   >
   >* 靜態轉譯會顯示在窗格的上半部。 動態轉譯會顯示在下半部。 若僅使用動態轉譯，您可以使用URL來顯示影像。 **[!UICONTROL URL]**&#x200B;按鈕只會在您選取動態轉譯時顯示。 **[!UICONTROL RESS]**&#x200B;按鈕只有在您選取回應式影像預設集時才會出現。
   >
   >* 當您在資產的詳細資料檢視中選取&#x200B;**[!UICONTROL 轉譯]**&#x200B;時，系統會顯示許多轉譯。 您可以增加所檢視的預設集數目。請參閱[增加顯示的影像預設集數目](managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display)。

   ![chlimage_1-208](assets/chlimage_1-208.png)

1. 執行下列任一項作業：

   * 若要預覽影像預設集，請選取動態轉譯。
   * 若要顯示快顯視窗，請選取&#x200B;**[!UICONTROL URL]**、**[!UICONTROL 內嵌]**&#x200B;或&#x200B;**[!UICONTROL RESS]**。

   >[!NOTE]
   >
   >如果資產&#x200B;*和*&#x200B;影像預設集尚未發佈，**[!UICONTROL URL]**&#x200B;按鈕（或URL和RESS按鈕，如果適用）將不可用。
   >
   >也請注意，影像預設集會自動發佈在Dynamic Media S7伺服器上。
