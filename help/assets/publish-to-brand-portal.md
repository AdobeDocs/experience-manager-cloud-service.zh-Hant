---
title: 將資產、檔案夾和系列發佈至品牌入口網站
seo-title: 將資產、檔案夾和系列發佈至品牌入口網站
description: 瞭解如何將資產、檔案夾和系列發佈及解除發佈至品牌入口網站。
seo-description: 瞭解如何將資產、檔案夾和系列發佈及解除發佈至品牌入口網站。
uuid: null
contentOwner: Vishabh Gupta
products: SG_EXPERIENCEMANAGER/ASSETS
topic-tags: brand-portal
content-type: reference
discoiquuid: null
translation-type: tm+mt
source-git-commit: abc98974f5507c71e75cdd864a98281f7cdba7f3

---


# 將資產、檔案夾和系列發佈至品牌入口網站 {#publish-aem-assets-to-brand-portal}

身為Adobe Experience Manager(AEM)Assets管理員，您可以將資產、檔案夾和系列發佈至AEM Assets品牌入口網站例項。 此外，您也可以將資產或資料夾的發佈工作流程排程到稍後的日期或時間。 發佈後，品牌入口網站的使用者可以存取資產、檔案夾和系列，並進一步將它們分發給其他使用者。

不過，您必須先將AEM資產與品牌入口網站一起設定。 如需詳細資訊，請 [參閱「設定AEM資產與品牌入口網站](configure-aem-assets-with-brand-portal.md)」。

如果您在AEM Assets中對原始資產、檔案夾或系列進行後續修改，在您從AEM Assets重新發佈之前，這些變更不會反映在品牌入口網站中。 此功能可確保品牌入口網站中不提供進行中的變更。 品牌入口網站中僅提供管理員發佈的已核准變更。

* [將資產發佈至品牌入口網站](#publish-assets-to-bp)
* [將資料夾發佈至品牌入口網站](#publish-folders-to-brand-portal)
* [將系列發佈至品牌入口網站](#publish-collections-to-brand-portal)

>[!NOTE]
>
>Adobe建議交錯排版，最好是在非尖峰時段進行，如此AEM作者就不會佔用過多的資源。


## Publish assets to Brand Portal {#publish-assets-to-bp}

以下是將資產從AEM Assets發佈至品牌入口網站的步驟：

1. 從「資產」主控台開啟父資料夾，並選取您要發佈的所有資產，然後從工具列按一下「 **[!UICONTROL 快速發佈]** 」選項。


   ![publish2bp-2](assets/publish2bp.png)

1. 以下是發佈資產的兩種方式：
   * [立即發佈](#publish-to-bp-now) （立即發佈資產）
   * [稍後發佈](#publish-to-bp-now) （排程發佈資產）

### 立即發佈資產 {#publish-to-bp-now}

若要將選取的資產發佈至品牌入口網站，請執行下列其中一項作業：

* 從工具列中選取「快 **[!UICONTROL 速發佈」]**。 在功能表中，按一下「 **[!UICONTROL 發佈至品牌入口網站」]**。

* 從工具列中，選擇「管 **[!UICONTROL 理出版物」]**。

   1. 從「 **[!UICONTROL 動作]**」中，選 **[!UICONTROL 擇「發佈至品牌入口網站]**」，然後從「計畫 **[!UICONTROL 」中選]**&#x200B;擇「 ****&#x200B;立即啟用」。 按一 **[!UICONTROL 下「下一步]**」。

   2. 在「範圍」中確認您 **[!UICONTROL 的選擇]**，然後按一 **[!UICONTROL 下「發佈至品牌入口網站」]**。

出現訊息，指出資產已排入發佈至品牌入口網站的佇列。 登入品牌入口網站介面，以檢視已發佈的資產。

### 稍後發佈資產 {#publish-to-bp-later}

若要排程將資產發佈至品牌入口網站的日期或時間：

1. 選取您要排程發佈的資產，從頂端的工具列選 **[!UICONTROL 取「管理出版物]** 」。

1. 在「管 **[!UICONTROL 理出版物]** 」頁面上，選 **[!UICONTROL 擇「從]** Portal發佈到品牌門戶 **[!UICONTROL 」操作，然後從SchedulingSchedulingPortal中選]**********&#x200B;擇Publish to Brand Portal。

   ![publishlaterbp-1](assets/publishlaterbp-1.png)

1. 選擇啟 **動日期** ，並指定時間。 按一 **下「下一步**」。

1. 在「工作流 **[!UICONTROL 程」中指定]** 「工 **[!UICONTROL 作流」標題]**。 按一下「 **[!UICONTROL 稍後發佈]**」。

   ![publishworkflow](assets/publishworkflow.png)

登入品牌入口網站介面，以檢視已發佈的資產可用。

![bp_landing_page](assets/bp_landing_page.png)

<!--

End - Publish assets to Brand Portal
Start- Publish folders to Brand Portal
-->


## Publish folders to Brand Portal{#publish-folders-to-brand-portal}

您可以立即發佈或取消發佈資產資料夾，或排程至稍後的日期或時間。

### Publish folders to Brand Portal {#publish-folders-to-brand-portal-1}

1. 從「資產」主控台中，選取您要發佈的檔案夾，然後從工具列按一 **[!UICONTROL 下「快速發佈]** 」選項。

   ![publish2bp](assets/publish2bp.png)

1. **立即發佈資料夾**

   若要將選取的檔案夾發佈至品牌入口網站，請執行下列其中一項作業：

   * 從工具列中選取「快 **[!UICONTROL 速發佈」]**。 從功能表中，選取「 **[!UICONTROL 發佈至品牌入口網站」]**。

   * 從工具列中，選擇「管 **[!UICONTROL 理出版物」]**。

      1. 從「 **[!UICONTROL 動作]**」中，選 **[!UICONTROL 取「發佈至品牌入口網站」]**。 在「 **[!UICONTROL 排程]**」中，選 **[!UICONTROL 擇「現在」]**。 按一 **[!UICONTROL 下「下一步]**」。
      1. 在「範圍」中確認您 **[!UICONTROL 的選擇]** ，然後按 **[!UICONTROL 一下「發佈至品牌入口網站」]**。
   出現訊息，指出資料夾已排入發佈至品牌入口網站的佇列。 登入您的品牌入口網站介面，以查看已發佈的資料夾。

1. **稍後發佈資料夾**

   若要排程將資產檔案夾發佈至稍後的日期或時間。

   1. 選取您要排程發佈的檔案夾，從頂端的工具列選 **[!UICONTROL 取「管理出版物]** 」。
   1. 從「 **[!UICONTROL 動作]**」中，選 **[!UICONTROL 擇「發佈至品牌入口網站]**」，然後從「計畫」 **[!UICONTROL 中選]** 擇「稍後 ****&#x200B;發佈」。

      ![publishlaterbp](assets/publishlaterbp.png)

   1. 選擇啟 **[!UICONTROL 動日期]** ，並指定時間。 按一 **[!UICONTROL 下「下一步]**」。
   1. 在「範圍」中確認您 **[!UICONTROL 的選擇]**。 按一 **[!UICONTROL 下「下一步]**」。
   1. 在「工作流程」( **[!UICONTROL Workflows)下指定「工作流」(Workflows]**)標題。 按一下「 **[!UICONTROL 稍後發佈]**」。

      ![managerchedulepub](assets/manageschedulepub.png)

### Unpublish folders from Brand Portal {#unpublish-folders-from-brand-portal}

您可以從AEM Assets例項中取消發佈任何已發佈至品牌入口網站的資產資料夾，以移除它。 解除發佈原始資料夾後，品牌入口網站使用者將無法再使用其副本。

您可以立即從品牌入口網站解除發佈資產資料夾，或排程以後的日期和時間。

若要從品牌入口網站取消發佈資產資料夾：

1. 從AEM Assets主控台中，選取您要解除發佈的檔案夾。

   ![publish2bp-1](assets/publish2bp.png)

1. 在工具列中，按一下「管 **[!UICONTROL 理出版物」]**。

1. **立即從品牌入口網站取消發佈**

   若要立即從品牌入口網站取消發佈選取的檔案夾：

   1. 從工具列中，選擇「管 **理出版物」**。
   1. 從「 **From**」( **From**)中，選擇「從品牌入口網站取消發佈」(Unpublish from Brand Portal **)，然後從「Scheduling**」（計畫）中選 **擇「Now** Zame」（立即發佈）。 按一 **下「下一步」。**
   1. 在「範圍」中確認您 **的選擇** ，然後按一 **下「從品牌入口網站取消發佈」**。
   ![確認——取消發佈](assets/confirm-unpublish.png)

1. **稍後從品牌入口網站取消發佈**

   若要排程從品牌入口網站取消發佈資料夾至稍後的日期和時間：

   1. 從工具列中，選擇「管 **理出版物」**。
   1. 從「 **動作**」中，選 **擇「從品牌入口網站取消發佈**」，然後從「計畫」 **中選** 擇「稍後 ****&#x200B;撤消」。
   1. 選擇啟 **動日期** ，並指定時間。 按一 **下「下一步**」。
   1. 在「範圍」中確認您 **的選擇** ，然後按一 **下「下一步」**。
   1. 在「工作流 **程」中指定** 「工 **作流」標題**。 按一下「 **稍後取消發佈」。**

      ![unpublish工作流程](assets/unpublishworkflows.png)


<!--
End - Publish folders to Brand Portal
Start- Publish Collections to Brand Portal

-->

## Publish collections to Brand Portal {#publish-collections-to-brand-portal}

您可以從AEM Assets例項發佈或取消發佈系列。

>[!NOTE]
>
>內容片段無法發佈至品牌入口網站。 因此，如果您在AEM Asset中選取內容片段，則「發佈至品 **[!UICONTROL 牌入口網站]** 」動作將無法使用。
>
>如果包含內容片段的系列從AEM Assets發佈至品牌入口網站，則資料夾的所有內容（內容片段除外）都會複製至品牌入口網站介面。

### 發佈系列 {#publish-a-collection-to-brand-portal}

以下是將系列從AEM Assets發佈至品牌入口網站的步驟：

1. 在「AEM Assets UI」中，按一下「AEM logo」。
1. From **Navigation** page, go to **[!UICONTROL Assets]** > **[!UICONTROL Collections]**.
1. 從「系 **列** 」主控台中，選取您要發佈至品牌入口網站的系列。

   ![select_collection](assets/select_collection.png)

1. 在工具列中，按一下「 **[!UICONTROL 發佈至品牌入口網站」]**。
1. 在確認對話方塊中，按一下「 **[!UICONTROL 發佈」]**。
1. 關閉確認消息。

   以管理員身分登入品牌入口網站。 「系列」主控台中提供已發佈 **[!UICONTROL 的系列]** 。

   ![發佈系列](assets/published_collection.png)

## 取消發佈系列 {#unpublish-collections}

您可以從AEM Assets例項中取消發佈任何發佈至品牌入口網站的系列，以移除它。 在您解除發佈原始系列後，品牌入口網站使用者將無法再使用其副本。

以下是解除發佈系列的步驟：

1. 從AEM Assets例項的「系列」主控台中，選取您要解除發佈的系列。

   ![select_collection-1](assets/select_collection-1.png)

1. 在工具列中，按一下「從 **[!UICONTROL 品牌入口網站移除]** 」圖示。
1. 在對話方塊中，按一下「 **[!UICONTROL 解除發佈]**」。
1. 關閉確認消息。 系列會從品牌入口網站介面中移除。

如需資產 [、檔案夾和系列散發給使用者的詳細資訊](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/home.html) ，請參閱品牌入口網站檔案。

<!--

End - Publish Collections to Brand Portal

-->

