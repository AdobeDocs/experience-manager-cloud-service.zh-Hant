---
title: 如何在預覽或發佈執行個體上發佈或取消發佈表單？
description: 瞭解如何從AEM製作環境發佈或取消發佈表單，以預覽或發佈執行個體。 無論您是在預備環境中測試表單，還是為一般使用者即時部署，AEM都能提供簡化的工具，讓您有效率地管理此程式。
Keywords: Manage publication, Forms Manage publication, AF Manage publication, Adaptive Forms Manage publication, Cloud Manage publication
feature: Adaptive Forms
feature-set: Experience Manager Assets,Experience Manager Sites,Experience Manager, Experience Manager Forms, Experience Manager Cloud Manager
role: User, Developer
level: Intermediate
source-git-commit: d3c089dcca80255f53c0888d46ee1b4b6246741e
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 0%

---


# 在Experience Manager Forms中管&#x200B;理發佈

作為Adobe Experience Manager Forms管理員，您可以從作者執行個體發佈表單至Experience Manager Forms。 您可以排程在稍後的日期或時間發佈表單或資料夾。 發佈後，使用者即可存取及填寫表單。

在Experience Manager Forms介面中，您可以使用以下功能發佈表單：
* [Publish選項](#publish-forms-using-the-publish-option)
* [管理發布選項](#publish-forms-using-the-manage-publication-option)

如果您對Experience Manager Forms中的原始表單或資料夾進行後續修改，則在您從Experience Manager Forms重新發佈之前，這些變更不會反映在&#x200B;**Publish**&#x200B;執行個體中。 這可確保在&#x200B;**Publish**&#x200B;執行個體中無法使用進行中的變更。 **Publish**&#x200B;執行個體中只能使用管理員發佈的變更。

## 使用Publish選項的Publish表單

**Publish**&#x200B;選項可讓您立即發佈表單。 若要使用工具列上的&#x200B;**Publish**&#x200B;按鈕發佈Experience Manager表單。 若要使用Publish選項發佈表單，請執行下列動作：

1. 從Experience Manager Forms主控台，導覽至上層資料夾，並選取您要發佈的表單。
1. 按一下工具列中的&#x200B;**Publish**&#x200B;選項，檢視所有將隨表單發佈的參考資產。
1. 點擊&#x200B;**[!UICONTROL 發佈]**。

   ![Publish與取消發佈表單](/help/edge/docs/forms/assets/publish-form-option.png)

   成功發佈表單及其相關資產後，**成功**&#x200B;對話方塊就會顯示。 按一下&#x200B;**關閉**&#x200B;以關閉對話方塊。

   ![成功對話框](/help/forms/assets/publish-success.png)

### 取消發佈表單

使用&#x200B;**Publish**&#x200B;選項及其相關資產成功發佈表單後，您甚至可以使用工具列上的&#x200B;**[!UICONTROL 取消發佈]**&#x200B;按鈕來取消發佈它們。 若要取消發佈表單：

1. 若要取消發佈表單及其相關資產，請選取表單，然後從工具列按一下&#x200B;**[!UICONTROL 取消發佈]**

   當您按一下&#x200B;**[!UICONTROL 取消發佈]**&#x200B;按鈕時，**取消發佈資產**&#x200B;對話方塊就會顯示。
1. 按一下&#x200B;**[!UICONTROL 取消發佈]**&#x200B;以開始取消發佈程式

   ![解除對話方塊](/help/forms/assets/unpublish-asset.png)

   一旦表單及其相關資產成功取消發佈，就會顯示&#x200B;**成功**&#x200B;對話方塊。 按一下&#x200B;**關閉**&#x200B;以關閉對話方塊。

   ![取消發佈成功](/help/forms/assets/unpublishing-start.png)

## 使用管理發布選項的Publish表單

管理出版物可讓您向選定目標發佈內容或從中取消發佈內容、在表單與檔案資料夾中將內容新增到發佈清單、選取要發佈的引用，以及排程發佈到更晚的日期或時間。  若要使用管理發布選項發佈表單，請執行下列動作：

1. 從Experience Manager Forms主控台，導覽至上層資料夾，並選取您要發佈的表單。
1. 按一下工具列中的&#x200B;**[!UICONTROL 管理出版物]**&#x200B;選項。

   ![管理出版物選項](/help/forms/assets/manage-publication-option.png)

   **管理出版物**&#x200B;介面出現：

   ![管理出版物](/help/forms/assets/manage-publication.png)

   **管理出版物**&#x200B;介面中有以下選項：

   * **動作**

      * **Publish**： Publish表單到選取的目的地
      * **取消發佈**：從目的地取消發佈表單

   * **目的地**

      * **Publish**： Publish表單至Experience Manager Forms (AEM) Publish執行個體。
      * **預覽**： Publish forms到Experience Manager Forms (AEM)預覽執行個體。

   * **排程**

      * **現在**：立即Publish表單
      * **稍後**：根據&#x200B;**啟用日期**&#x200B;或時間的Publish表單

1. 按一下[下一步]****&#x200B;繼續。
1. 在&#x200B;**範圍**&#x200B;索引標籤中，使用[新增內容](#add-content)選項來新增更多發佈內容。 例如，您可以新增更多Forms或記錄檔案檔案。
   ![範圍標籤](/help/forms/assets/scope-tab.png)
1. 按一下&#x200B;**[!UICONTROL Publish]**發佈表單和相關資產，成功訊息就會出現。
   ![成功發佈訊息](/help/forms/assets/publish-successful.png)

### 新增內容

發佈至Experience Manager Forms可讓您進一步新增更多內容（表單和資料夾）至發佈清單。 您可以從`formsanddocuments`資料夾新增更多表單或資料夾至清單。 但您無法一次從多個資料夾新增表單。 若要新增更多表單以進行發佈：

1. 按一下「**新增內容**」按鈕以新增更多內容。

   ![新增內容](/help/forms/assets/add-content.png)

1. 從&#x200B;**選取路徑**&#x200B;畫面中選取表單。 您可以從資料夾新增多個表單，或一次新增多個資料夾。 但您無法一次從多個資料夾新增表單。

   ![新增內容](/help/forms/assets/add-assets.png)

1. 若要設定要發佈或不發佈表單的參考，請選取表單並按一下&#x200B;**[!UICONTROL 已發佈參考]**。

   ![已發佈的參考](/help/forms/assets/published-references.png)

1. 在&#x200B;**已發佈的參考**&#x200B;對話方塊中，取消勾選您計畫不發佈的資產，然後按一下&#x200B;**[!UICONTROL 完成]**。
   ![已發佈的參考對話方塊](/help/forms/assets/published-references-dialog.png)

<!--
### Include Folder Settings
By default, publishing a folder to Experience Manager Forms publishes all the assets, subfolders, and their references. To filter the folder for publishing:

1. Click **[Include Folder Settings]** to filter the folder.

    ![Include folder](/help/forms/assets/include-folder.png)

    The **[UICONTROL Include Folder Settings]** dialog appears. 
    
    ![Include folder dialog](/help/forms/assets/include-folder-dialog.png)
    
    The **[UICONTROL Include Folder Settings]** includes following options:

    * **[!UICONTROL Include folder contents]** checkbox. 
        * If selected, all forms and assets in the chosen folder, its subfolders (including all forms and assets within them), and references are published.
        * If not selected, only the forms and assets in the selected folder are published, while subfolder forms and assets are not.

    * **[!UICONTROL Include only immediate folder contents]** checkbox
        Selecting the **[!UICONTROL Include folder contents]** checkbox enables the **[!UICONTROL Include only immediate folder contents]** checkbox for selection.

        * If you select both options, all the forms and assets of the selected folder, subfolders (empty), and references are published. The forms and assets of the subfolders are not published.
        * -->


### Publish或稍後取消發佈表單

除了可讓您在稍後日期和時間發佈或取消發佈表單外，稍後發佈或取消發佈選項也可讓您設定工作流程。 在工作流程完成後，會發佈或取消發佈表單。 若要排程表單以供發佈或取消發佈：

1. 從Experience Manager Forms主控台，導覽至上層資料夾，並選取您要排程發佈的表單。
1. 按一下工具列中的&#x200B;**[!UICONTROL 管理出版物]**&#x200B;選項。

   ![管理出版物](/help/forms/assets/manage-publication.png)

1. 按一下&#x200B;**Publish**&#x200B;或&#x200B;**從**[!UICONTROL &#x200B;動作&#x200B;]**取消發佈**，然後選取您要發佈或取消發佈內容的&#x200B;**[!UICONTROL 目的地]**。
   * **預覽**：使用&#x200B;**預覽**&#x200B;選項來發佈或取消發佈至Experience Manager Forms預覽環境。 Experience Manager Forms預覽環境用於測試開發表單。
   * **Publish**：使用Experience Manager Forms Publish選項，在表單準備好用於生產環境後，將表單傳送至Experience Manager Forms發佈環境。

1. 從排程中選取&#x200B;**[!UICONTROL 稍後]**。

   ![稍後再管理出版物](/help/forms/assets/manage-publication-later.png)

1. 選取&#x200B;**[!UICONTROL 啟用日期]**&#x200B;並指定日期和時間。
1. 按一下&#x200B;**[!UICONTROL 下一步]**。
1. 在&#x200B;**領域**&#x200B;索引標籤中，**[!UICONTROL 新增內容]** （如有必要）。
   ![稍後再管理出版物新增內容](/help/forms/assets/publish-later-add-content.png)
1. 按一下「**[!UICONTROL 下一步]**」。
1. （選擇性）在&#x200B;**工作流程**&#x200B;索引標籤中，指定&#x200B;**[!UICONTROL 工作流程標題]**。
1. 按一下&#x200B;**[!UICONTROL 稍後]**&#x200B;的Publish。

   ![管理發布工作流程](/help/forms/assets/manage-publication-workflows.png)

## 正在判斷發佈狀態

有多種方式可判斷發佈狀態：

* 登入目的地執行個體以驗證發佈的表單和其他資產（取決於排定的日期或時間）。

* 使用時間軸檢視來判斷出版物狀態。

* 使用最適化Forms編輯器中的頁面資訊選單。
