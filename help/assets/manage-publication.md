---
title: 管理發佈
description: 將資產發佈或取消發佈至Experience Manager Assets、Dynamic Media和Brand Portal
contentOwner: Vishabh Gupta
mini-toc-levels: 1
feature: Asset Management, Publishing, Collaboration, Asset Processing
role: User, Architect, Admin
exl-id: 691a0925-0061-4c62-85ac-8257b96dddf2
source-git-commit: ca01102673211f17e58af36ef2a59d0e964022d5
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 8%

---

# 在Experience Manager Assets中管理出版物 {#manage-publication-in-aem}

作為 [!DNL Adobe Experience Manager Assets] 管理員，您可以將包含資產的資產和資料夾，從製作例項發佈至 [!DNL Experience Manager Assets], [!DNL Dynamic Media]，和 [!DNL Brand Portal]. 此外，您也可以將資產或資料夾的發佈工作流程安排在之後的日期或時間。發佈後，使用者可以存取資產，並進一步將資產分發給其他使用者。 依預設，您可以將資產和資料夾發佈至 [!DNL Experience Manager Assets]. 不過，您可以設定 [!DNL Experience Manager Assets] 啟用發佈至 [[!DNL Dynamic Media]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/config-dm.html) 和 [[!DNL Brand Portal]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html).

您可以在資產或資料夾層級發佈或取消發佈資產，使用 **[!UICONTROL 快速發佈]** 或 **[!UICONTROL 管理出版物]** 選項 [!DNL Experience Manager Assets] 介面。 如果您後續修改中的原始資產或資料夾 [!DNL Experience Manager Assets]，在您從重新發佈前，變更不會反映在發佈例項中 [!DNL Experience Manager Assets]. 這可確保進行中的變更無法在發佈執行個體中使用。 發佈執行個體中只有管理員發佈的已核准變更可供使用。

* [使用快速發佈來發佈資產](#quick-publish)
* [使用管理出版物發佈資產](#manage-publication)
* [稍後發佈資產](#publish-assets-later)
* [將資產發佈至Dynamic Media](#publish-assets-to-dynamic-media)
* [將資產發佈至 Brand Portal](#publish-assets-to-brand-portal)
* [限制和提示](#limitations-and-tips)

## 使用快速發佈來發佈資產 {#quick-publish}

快速發佈可讓您立即將內容發佈至選取的目的地。 從 [!DNL Experience Manager Assets] 主控台，導覽至上層資料夾，並選取您要發佈的所有資產或資料夾。 按一下 **[!UICONTROL 快速發佈]** 選項，然後從下拉式清單中選取您要發佈資產的目的地。

![快速發佈](assets/quick-publish-to-aem.png)

## 使用管理出版物發佈資產 {#manage-publication}

管理出版物可讓您將內容發佈或取消發佈至所選目的地，或從所選目的地發佈內容 [新增內容](#add-content) 從DAM存放庫的發佈清單， [包含資料夾設定](#include-folder-settings) 發佈所選資料夾的內容並應用篩選器，以及 [排程發佈](#publish-assets-later) 到以後的日期或時間。

從 [!DNL Experience Manager Assets] 主控台，導覽至上層資料夾，並選取您要發佈的所有資產或資料夾。 按一下 **[!UICONTROL 管理出版物]** 選項。 如果您沒有 [!DNL Dynamic Media] 和 [!DNL Brand Portal] 在 [!DNL Experience Manager Assets] 例項，您只能將資產和資料夾發佈至 [!DNL Experience Manager Assets].

![管理發佈](assets/manage-publication-aem.png)

下列選項適用於 [!UICONTROL 管理出版物] 介面：

* [!UICONTROL 動作]
   * `Publish`:將資產和資料夾發佈至選取的目的地
   * `Unpublish`:從目的地取消發佈資產和資料夾

* [!UICONTROL 目的地]
   * `Publish`:將資產和資料夾發佈至 [!DNL Experience Manager Assets] (`AEM`)
   * `Dynamic Media`:將資產發佈至 [!DNL Dynamic Media]
   * `Brand Portal`:將資產和資料夾發佈至 [!DNL Brand Portal]

* [!UICONTROL 排程]
   * `Now`:立即發佈資產
   * `Later`:根據發佈資產 `Activation` 日期或時間

若要繼續，請按一下 **[!UICONTROL 下一個]**. 根據選取項目， **[!UICONTROL 範圍]** 標籤會反映不同的選項。 選項 **[!UICONTROL 新增內容]** 和 **[!UICONTROL 包含資料夾設定]** 僅供發佈資產和資料夾至 [!DNL Experience Manager Assets] (`Destination: Publish`)。

![管理發布範圍](assets/manage-publication-aem-scope.png)

### 新增內容 {#add-content}

發佈至 [!DNL Experience Manager Assets] 可讓您進一步將更多內容（資產和資料夾）新增至發佈清單。 您可以在dam-repositories中新增更多資產或資料夾至清單。 按一下 **[!UICONTROL 新增內容]** 按鈕以新增更多內容。

您可以從資料夾新增多個資產，或一次新增多個資料夾。 但您無法一次從多個資料夾新增資產。

![新增內容](assets/manage-publication-add-content.png)

### 包含資料夾設定 {#include-folder-settings}

依預設，將資料夾發佈至 [!DNL Experience Manager Assets] 會發佈所有資產、子資料夾及其參考。

若要篩選要發佈的資料夾內容，請按一下 **[!UICONTROL 包含資料夾設定]**:

* `Include folder contents`

   * 已啟用：會發佈所選資料夾、子資料夾（包括子資料夾的所有資產）和引用的所有資產。
   * 已禁用：僅發佈所選資料夾（空）和引用。 不會發佈所選資料夾的資產。

* `Include folder contents` 和 `Include only immediate folder contents`

   如果同時選取兩個選項，則會發佈所選資料夾、子資料夾（空）和引用的所有資產。 未發佈子資料夾的資產。

<!--
* [!UICONTROL Include only immediate folder contents]: Only the subfolders content and references are published. 

Only the selected folder content and references are published.
-->

![包含資料夾設定](assets/manage-publication-include-folder-settings.png)

套用篩選器後，按一下 **[!UICONTROL 確定]**，然後按一下 **[!UICONTROL 發佈]**. 按一下發佈按鈕時，會顯示確認訊息 `Resource(s) have been scheduled for publication` 框。 並且，會根據排程器(`Now` 或 `Later`)。 登入您的發佈執行個體，以確認資產和（或）資料夾已成功發佈。

![發佈至 AEM](assets/manage-publication-publish-aem.png)

在上圖中，您可以看到 **[!UICONTROL 發佈目標]** 屬性。 讓我們回想一下，您選擇發佈至 [!DNL Experience Manager Assets] (`Destination: Publish`)。 那麼，為什麼只顯示資料夾和資產已發佈至 `AEM`，而另外兩個資產會發佈至兩者 `AEM` 和 `Dynamic Media`?

在此，您必須了解資料夾屬性的角色。 資料夾的 **[!UICONTROL Dynamic Media發佈模式]** 屬性在發佈中扮演著重要角色。 要查看資料夾的屬性，請選擇資料夾並按一下 **[!UICONTROL 屬性]** 的上界。 如需資產，請參閱其上層資料夾的屬性。

下表說明發佈的發生方式，具體取決於已定義的 **[!UICONTROL 目的地]** 和 **[!UICONTROL Dynamic Media發佈模式]**:

| [!UICONTROL 目的地] | [!UICONTROL Dynamic Media 發佈模式] | [!UICONTROL 發佈目標] | 允許的內容 |
| --- | --- | --- | --- |
| 發佈 | 選擇性發佈 | `AEM` | 資產和（或）資料夾 |
| 發佈 | 立即 | `AEM` 和 `Dynamic Media` | 資產和（或）資料夾 |
| 發佈 | 啟動時 | `AEM` 和 `Dynamic Media` | 資產和（或）資料夾 |
| Dynamic Media | 選擇性發佈 | `Dynamic Media` | Assets |
| Dynamic Media | 立即 | `None` | 無法發佈資產 |
| Dynamic Media | 啟動時 | `None` | 無法發佈資產 |

>[!NOTE]
>
>只有資產會發佈至 [!DNL Dynamic Media].
>
>將資料夾發佈至 [!DNL Dynamic Media] 不支援。
>
>如果您選取資料夾(`Selective Publish`)，然後選取 [!DNL Dynamic Media] 目的地， [!UICONTROL 發佈目標] 屬性反映 `None`.


現在，讓我們變更 **[!UICONTROL 目的地]** 在上述使用案例中， **[!UICONTROL Dynamic Media]** 並驗證結果。 這樣做，只有 `Selective Publish` 資料夾已發佈至 [!DNL Dynamic Media]. 資產 `Immediate` 和 `Upon Activation` 資料夾未發佈，且會反映 `None`.

![發佈至 Dynamic Media](assets/manage-publication-dynamic-media.png)

>[!NOTE]
>
>若 [!DNL Dynamic Media] 未在 [!DNL Experience Manager Assets] 例項和 **[!UICONTROL 目的地]** is **[!UICONTROL 發佈]**，資產和資料夾一律會發佈至 `AEM`.
>
>發佈至 [!DNL Brand Portal] 獨立於資料夾屬性。 所有資產、資料夾和集合都可以發佈至Brand Portal。 請參閱 [將資產發佈至Brand Portal](#publish-assets-to-brand-portal).

>[!NOTE]
>
>如果您已自訂 [!DNL Manage Publication] 精靈，您的自訂功能會繼續與現有功能搭配使用。
>
>不過，您可以移除現有自訂，以使用新 [!DNL Manager Publication] 功能。


## 稍後發佈資產 {#publish-assets-later}

若要將資產的發佈工作流程排程至之後的日期或時間：

1. 從 [!UICONTROL Experience Manager Assets] 主控台，導覽至父資料夾，並選取您要排程發佈的所有資產或資料夾。
1. 按一下 **[!UICONTROL 管理出版物]** 選項。
1. 按一下 **[!UICONTROL 發佈]** 從 **[!UICONTROL 動作]**，然後選取 **[!UICONTROL 目的地]** 發佈內容的位置。
1. 在&#x200B;**[!UICONTROL 排程]**&#x200B;中選取&#x200B;**[!UICONTROL 稍後]**。
1. 選取 **[!UICONTROL 啟用日期]** 並指定日期和時間。 按一下&#x200B;**[!UICONTROL 下一步]**。

   ![管理發布工作流程](assets/manage-publication-workflow.png)

1. 在 **[!UICONTROL 範圍]** 標籤 **[!UICONTROL 新增內容]** （如有必要）。 按一下&#x200B;**[!UICONTROL 下一步]**。
1. 在 **[!UICONTROL 工作流程]** 頁簽，指定「工作流標題」。 按一下&#x200B;**[!UICONTROL 稍後發佈]**。

   ![工作流程標題](assets/manage-publication-workflow-title.png)

   登入目的地例項以驗證已發佈的資產（視排程的日期或時間而定）。

## 將資產發佈至Dynamic Media {#publish-assets-to-dynamic-media}

只有資產會發佈至 [!DNL Dynamic Media]. 不過，發佈行為會因資料夾屬性而異。 資料夾可以 **[!UICONTROL Dynamic Media發佈模式]** 已針對選擇性發佈進行設定，其可為下列任一項目：

* `Selective Publish`
* `Immediate`
* `Upon Activation`

的發佈程式 **[!UICONTROL 立即]** 和 **[!UICONTROL 啟動時]** 模式一致，但 **[!UICONTROL 選擇性發佈]**. 請參閱 [在Dynamic Media的資料夾層級設定選擇性發佈](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html). 在資料夾中設定選擇性發佈後，您可以執行下列任一操作：

* [使用管理出版物選擇性地將資產發佈至Dynamic Media或Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-manage-publication)
* [使用管理出版物從Dynamic Media或Experience Manager選擇性取消發佈資產](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-unpublish-manage-publication)
* [使用快速發佈將資產發佈至Dynamic Media或Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#quick-publish-aem-dm)
* [透過搜尋結果選擇性地發佈或取消發佈資產](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/selective-publishing.html?lang=en#selective-publish-unpublish-search-results)

## 將資產發佈至 Brand Portal {#publish-assets-to-brand-portal}

您可以將資產、資料夾和集合發佈至 [!DNL Experience Manager Assets Brand Portal] 例項。

* [將資產發佈至 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-assets-to-bp)
* [將資料夾發佈至 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-folders-to-brand-portal)
* [將集合發佈至 Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/publish-to-brand-portal.html?lang=en#publish-collections-to-brand-portal)

## 限制和提示 {#limitations-and-tips}

* 選項為 [!UICONTROL 管理出版物] 僅適用於具有復寫權限的使用者帳戶。
* 未發佈空資料夾。
* 如果您發佈的資產經過處理，則只會發佈原始內容。 遺失轉譯。 等待處理完成，然後在處理完成後發佈或重新發佈資產。
* 取消發佈複雜資產時，僅取消發佈資產。 請避免取消發佈參考，因為其他已發佈的資產可能會參照這些參考。
