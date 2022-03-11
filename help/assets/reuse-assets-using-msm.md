---
title: 使用MSM重新使用資產
description: 跨從父資產派生並連結到父資產的多個頁/資料夾使用資產。 資產與主副本保持同步，只需按一下幾下，即可從父資產接收更新。
contentOwner: AG
mini-toc-levels: 1
role: User, Admin, Architect
feature: Asset Management,Multi Site Manager
exl-id: a71aebdf-8e46-4c2d-8960-d188b14aaae9
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '3221'
ht-degree: 10%

---

# 使用MSM重新使用資產 [!DNL Assets] {#reuse-assets-using-msm-for-assets}

中的多站點管理器(MSM)功能 [!DNL Adobe Experience Manager] 使用戶能夠重用一次創作的內容，並可跨多個Web位置重用。 MSM的名稱對於數字資產可使用相同功能 [!DNL Assets]。 使用MSM [!DNL Assets]，您可以：

* 建立一次資產，然後製作這些資產的拷貝，以在站點的其他區域中重新使用。
* 在同步中保留多個副本，並更新一次原始主副本以將更改推送到子副本。
* 通過臨時或永久暫停父資產和子資產之間的連結來進行本地更改。

## 瞭解MSM的優點和概念 {#concepts}

### 它的工作原理和優點 {#how-it-works-and-the-benefits}

要瞭解在多個Web位置重複使用相同內容（文本和資產）的使用情形，請參見 [可能的MSM方案](/help/sites-cloud/administering/msm/overview.md)。 [!DNL Experience Manager] 維護原始資產及其連結副本（稱為即時副本）之間的連結。 維護的連結允許將集中的更改推送到許多即時拷貝。 這允許更快的更新，同時消除管理重複副本的限制。 變化的傳播是無錯誤的和集中的。 該功能允許為僅限於選定即時副本的更新留出空間。 用戶可以分離連結（即中斷繼承），並在下次更新主副本並刪除更改時不覆蓋的本地編輯。 可以對幾個選定的元資料欄位或整個資產進行分離。 它允許靈活地本地更新最初從主副本繼承的資產。

MSM在源資產及其即時拷貝之間保持即時關係，以便：

* 對源資產的更改也會應用（滾出）到即時拷貝，即即時拷貝與源同步。
* 您可以通過掛起即時關係或刪除幾個有限欄位的繼承來更新即時副本。 對源的修改不再應用於即時副本。

### MSM辭彙表 [!DNL Assets] 條款 {#glossary}

**來源：** 原始資產或資料夾。 從中派生即時副本的主副本。

**即時拷貝：** 與其源同步的源資產/資料夾的副本。 即時拷貝可以是更多即時拷貝的來源。 請參見如何建立LC。

**繼承：** 即時複製資產/資料夾及其源之間的連結/引用，系統用於記住將更新發送到何處。 元資料欄位的繼承在粒度級別。 可以刪除選擇性元資料欄位的繼承，同時保留源與其活動副本之間的活動關係。

**推廣：** 將對源進行的修改向下推至其即時副本的操作。 可以使用推廣操作一次更新一個或多個即時拷貝。 請參閱推廣。

**部署配置：** 確定同步哪些屬性、同步方式和同步時間的規則。 建立即時拷貝時應用這些配置；以後可以編輯；子項可以從其父資產繼承轉出配置。 MSM用於 [!DNL Assets]，僅使用標準部署配置。 其他部署配置不適用於MSM [!DNL Assets]。

**同步：** 除了部署外，還有一項操作，它通過將更新從源發送到即時拷貝，在源和其即時拷貝之間實現了奇偶校驗。 為特定即時副本啟動同步，該操作將從源中提取更改。 使用此操作，只能更新一個即時副本。 請參閱同步操作。

**掛起：** 臨時刪除即時副本與其源資產/資料夾之間的即時關係。 你可以恢復關係。 請參閱暫停操作。

**繼續：** 恢復即時關係，以便即時副本再次開始從源接收更新。 請參閱恢復操作。

**重置：** 重置操作通過覆蓋任何本地更改使即時拷貝再次成為源的複製副本。 它還會刪除繼承取消並重置所有元資料欄位的繼承。 要在將來進行本地修改，必須再次取消對特定欄位的繼承。 請參見對LC的本地修改。

**分離：** 不可撤消地刪除即時複製資產/資料夾的即時關係。 分離操作後，即時拷貝將永遠無法從源接收更新，並且它將不再是即時拷貝。 請參閱刪除關係。

## 建立資產的即時副本 {#create-livecopy}

要從一個或多個源資產或資料夾建立即時拷貝，請執行以下任一操作：

* 方法1:選擇源資產並按一下 **[!UICONTROL 建立]** > **[!UICONTROL 即時拷貝]** 的上界。
* 方法2:在 [!DNL Experience Manager] 用戶介面，按一下 **[!UICONTROL 建立]** > **[!UICONTROL 即時拷貝]** 從介面的右上角。

您可以一次建立資產或資料夾的即時副本。 您可以建立從資產或作為即時副本本身的資料夾派生的即時副本。 此使用情形不支援內容片段(CF)。 當嘗試建立其即時副本時，CF將按原樣複製，而不與任何關係。 複製的CF是及時的快照，在更新原始CF時不會更新。

要使用第一種方法建立即時拷貝，請執行以下步驟：

1. 選擇源資產或資料夾。 在工具欄中，按一下 **[!UICONTROL 建立]** > **[!UICONTROL 即時拷貝]**。

   ![建立即時副本 [!DNL Experience Manager] 介面](assets/create_lc1.png)

   *圖：建立即時副本 [!DNL Experience Manager] 。*

1. 選擇目標資料夾。 按一下&#x200B;**[!UICONTROL 下一步]**。
1. 提供標題和名稱。 資產沒有子項。 建立資料夾的即時副本時，您可以選擇包括或排除子項。
1. 選擇一個推廣配置。 按一下&#x200B;**[!UICONTROL 建立]**。

要使用第二種方法建立即時副本，請執行以下步驟：

1. 在 [!DNL Experience Manager] 介面，從右上角按一下 **[!UICONTROL 建立]** > **[!UICONTROL 即時拷貝]**。

   ![建立即時副本 [!DNL Experience Manager] 介面](assets/create_lc2.png)

   *圖：建立即時副本 [!DNL Experience Manager] 。*

1. 選擇源資產或資料夾。 按一下&#x200B;**[!UICONTROL 下一步]**。
1. 選擇目標資料夾。 按一下&#x200B;**[!UICONTROL 下一步]**。
1. 提供標題和名稱。 資產沒有子項。 建立資料夾的即時副本時，您可以選擇包括或排除子項。
1. 選擇一個推廣配置。 按一下&#x200B;**[!UICONTROL 建立]**。

>[!NOTE]
>
>移動源或即時副本時，將保留這些關係。 刪除即時副本後，將刪除關係。

## 查看源副本和即時副本的各種屬性和狀態 {#properties}

您可以從以下各個區域查看即時拷貝的資訊和MSM相關狀態：關係、同步、展開等 [!DNL Experience Manager] 用戶介面。

以下兩種方法適用於資產和資料夾：

* 選擇即時複製資產並在其「屬性」頁中查找資訊。
* 選擇源資料夾並從中查找每個即時副本的詳細資訊 [!UICONTROL 即時複製控制台]。

>[!TIP]
>
>要檢查幾個單獨的即時副本的狀態，請使用第一種方法檢查 **[!UICONTROL 屬性]** 的子菜單。 要檢查多個即時副本的狀態，請使用第二種方法檢查 **[!UICONTROL 關係狀態]** 的子菜單。

### 即時副本的資訊和狀態 {#status-lc-asset}

要檢查即時複製資產或資料夾的資訊和狀態，請執行以下步驟。

1. 選擇即時複製資產或資料夾。 按一下 **[!UICONTROL 屬性]** 的子菜單。 或者，使用鍵盤快捷鍵 `p`。
1. 按一下 **[!UICONTROL 即時拷貝]**。 您可以檢查源的路徑、暫停狀態、同步狀態、上次推廣日期以及上次推廣的用戶。

   ![即時複製資訊和狀態顯示在控制台的「屬性」中](assets/lcfolder_info_properties.png)

   *圖：即時複製資訊和狀態。*

1. 如果子資產借用即時複製配置，則可以啟用或禁用。

1. 您可以選擇即時副本的選項，以從父代繼承部署配置或更改配置。

### 資料夾所有即時副本的資訊和狀態 {#status-lc-folder}

[!DNL Experience Manager] 提供了一個控制台，用於檢查源資料夾所有即時副本的狀態。 此控制台顯示所有子資產的狀態。

1. 選擇源資料夾。 按一下 **[!UICONTROL 屬性]** 的子菜單。 或者，使用鍵盤快捷鍵 `p`。
1. 按一下「 **[!UICONTROL 即時複製來源」]**。若要開啟主控台，請按一下「即 **[!UICONTROL 時複製概述」]**。此控制面板提供所有子資產的頂層狀態。

   ![在源的Live Copy控制台中查看即時副本的狀態](assets/livecopy-statuses.png)

   *圖：查看中即時副本的狀態 [!UICONTROL 即時複製控制台] 來源。*

1. 若要檢視即時副本檔案夾中每個資產的詳細資訊，請選取資產，然後從工具列按一 **[!UICONTROL 下「關係狀態]** 」。

   ![資料夾中即時複製子資產的詳細資訊和狀態](assets/livecopy_relationship_status.png)

   資料夾中即時複製子資產的詳細資訊和狀態

>[!TIP]
>
>您可以快速查看其他資料夾的即時副本的狀態，而無需瀏覽太多。 從資料夾的中上部更改資料夾 **[!UICONTROL 即時複製概述]** 。

### 從「參考」(References)導軌為源執行快速操作 {#ref-rail-source}

對於源資產或資料夾，您可以查看以下資訊，並直接從「參考」(References)導軌執行以下操作：

* 請參閱即時副本的路徑。
* 在中開啟或顯示特定即時副本 [!DNL Experience Manager] 用戶介面。
* 將更新同步到特定即時副本。
* 掛起特定即時拷貝的關係或更改轉出配置。
* 訪問即時拷貝概述控制台。

選擇源資產或資料夾，開啟左滑軌，然後按一下 **[!UICONTROL 引用]**。 或者，選取資產或檔案夾，然後使用鍵盤快速鍵 `Alt + 4`。

![在「參照」(References)導軌中為選定源提供的操作和資訊](assets/referencerail_source.png)

*圖：在「參照」(References)滑軌中可用於選定源的操作和資訊。*

對於特定即時副本，按一下 **[!UICONTROL 編輯即時副本]** 掛起關係或更改展出配置。

![對於特定即時副本，當選擇源資產時，可以從「參考」導軌訪問掛起關係或更改展出配置的選項](assets/referencerail_editlc_options.png)

*圖：掛起特定即時副本的關係或更改轉出配置。*

### 從「參考」(References)導軌快速執行即時複製操作 {#ref-rail-lc}

對於即時複製資產或資料夾，您可以直接從「參考」(References)導軌查看以下資訊並執行以下操作：

* 查看其源的路徑。
* 在中開啟或顯示特定即時副本 [!DNL Experience Manager] 用戶介面。
* 啟動更新。

選取即時複製資產或資料夾，開啟左側導軌，然後按一下「參 **[!UICONTROL 考」]**。或者，選取資產或檔案夾，然後使用鍵盤快速鍵 `Alt + 4`。

![在「參考」(References)邊欄中，所選即時副本的可用動作](assets/referencerail_livecopy.png)

*圖：在「參照」(References)滑軌中可用於選定即時副本的操作。*

## 將修改從源傳播到即時拷貝 {#rollout-sync}

修改源後，可以使用同步操作或推廣操作將更改傳播到即時副本。 要瞭解兩個操作之間的差異，請參閱 [術語](#glossary)。

### 推廣操作 {#rollout}

您可以從源資產啟動推廣操作，並更新所有或幾個選定的即時副本。

1. 選擇即時複製資產或資料夾。 按一下 **[!UICONTROL 屬性]** 的子菜單。 或者，使用鍵盤快捷鍵 `p`。
1. 按一下「 **[!UICONTROL 即時複製來源」]**。按一下 **[!UICONTROL 推廣]** 的子菜單。
1. 選擇要更新的即時副本。 按一下 **[!UICONTROL 推廣]**。
1. 要推廣對子資產進行的更新，請選擇 **[!UICONTROL 推廣源和所有子級]**。

   ![將源的修改擴展為幾個或所有即時副本](assets/livecopy_rollout_page.png)

   *圖：將源的修改推廣到幾個或所有即時副本。*

>[!NOTE]
>
>在源資產中所做的修改只被推出到直接相關的即時副本。 如果即時副本是從另一個即時副本派生的，則不會將修改推出到派生的即時副本。

或者，在選擇特定即時副本後，可以從「參考」(References)滑軌啟動展示操作。 有關詳細資訊，請參見 [從「參考」(References)導軌快速執行即時複製操作](#ref-rail-lc)。 在此部署方法中，只更新選定的即時副本及其子代（可選）。

![將源的修改推出到所選即時副本](assets/livecopy_rollout_dialog.png)

*圖：將源的修改推出到所選即時副本。*

### 關於同步操作 {#about-sync}

同步操作將修改從源僅拉動到所選即時副本。 同步操作會尊重並維護取消繼承後進行的本地修改。 本地修改不會被覆蓋，取消的繼承也不會重新建立。 可以通過三種方式啟動同步操作。

| 在何處 [!DNL Experience Manager] 介面 | 何時和為什麼使用 | 如何使用 |
|---|---|---|
| [!UICONTROL 引用] 軌 | 已選擇源時，快速同步。 | 請參閱 [從「參考」(References)導軌為源執行快速操作](#ref-rail-source) |
| 工具欄 [!UICONTROL 屬性] 頁 | 在已開啟即時複製屬性時啟動同步。 | 請參閱 [同步即時拷貝](#sync-lc) |
| [!UICONTROL 即時複製概述] 控制台 | 在選擇或選擇源資料夾時快速同步多個資產（不一定全部） [!UICONTROL 即時複製概述] 控制台已開啟。 一次為一個資產啟動同步操作，但是這是一次為多個資產同步的更快方法。 | 請參閱 [對即時拷貝資料夾中的許多資產執行操作](#bulk-actions) |

### 同步即時拷貝 {#sync-lc}

若要啟動同步動作，請開啟即 **[!UICONTROL 時副本的「屬性]** 」頁面，按一下「即時 **** 副本」，然後從工具列按一下所要的動作。

要查看與同步操作相關的狀態和資訊，請參 [閱即時副本的資訊和狀態](#status-lc-asset)[以及資料夾所有即時副本的狀態](#status-lc-folder)。

![同步操作將調出對源所做的更改](assets/livecopy_sync.png)

*圖：同步操作將拉動對源所做的更改。*

>[!NOTE]
>
>如果關係已掛起，則同步操作在工具欄中不可用。 雖然同步操作在「參考」(References)導軌中可用，但即使成功部署，也不會傳播修改。

## 掛起和恢復關係 {#suspend-resume}

您可以暫時掛起關係，以防止即時副本接收對源資產或資料夾所做的修改。 還可以恢復關係，以便即時複製開始從源接收修改。

若要暫停或繼續，請開啟即 **[!UICONTROL 時副本的「屬性]** 」頁面，按一下「即時副本 **** 」，然後從工具列按一下所要的動作。

或者，您也可以從即時副本概述主控台，快速暫停或繼續即時副本資料夾中多 **[!UICONTROL 個資產的關係]** 。請參 [閱對即時副本資料夾中的許多資產採取動作](#bulk-actions)。

## 對即時副本進行本地修改 {#local-mods}

活動拷貝是建立原始源時的副本。 活動副本的元資料值從源繼承。 元資料欄位單獨地維護與源資產的各個欄位的繼承。

不過，您有彈性對即時副本進行本機修改，以變更一些選取的屬性。若要進行本機修改，請取消所要屬性的繼承。當取消一個或多個元資料欄位的繼承時，保留資產的即時關係和其它元資料欄位的繼承。任何同步或轉出都不會覆寫本機修改。為此，請開啟 **[!UICONTROL 屬性]** 頁面，按一下 **[!UICONTROL 取消繼承]** 選項。

您可以撤消所有本地修改並將資產還原為其源的狀態。 不可撤消且立即重置操作將覆蓋所有本地修改並重新建立所有元資料欄位的繼承。 要還原，請從 **[!UICONTROL 屬性]** 頁，按一下 **[!UICONTROL 重置]** 的子菜單。

![重置操作會覆蓋本地編輯內容，並部分將即時副本與其源一起提供。](assets/livecopy_reset.png)

*圖：重置操作會覆蓋本地編輯內容，並部分將即時副本與其源一起提供。*

## 刪除即時關係 {#detach}

使用「分離」(Detach)操作可以完全刪除源和即時副本之間的關係。 拆分後，即時副本將成為獨立資產或資料夾。 它將顯示為 [!DNL Experience Manager] 介面，在分離後立即。 要從源中分離即時副本，請執行以下步驟。

1. 選擇即時複製資產或資料夾。 按一下 **[!UICONTROL 屬性]** 的子菜單。 或者，使用鍵盤快捷鍵 `p`。

1. 按一下 **[!UICONTROL 即時拷貝]**。 按一下 **[!UICONTROL 分離]** 的子菜單。 按一下 **[!UICONTROL 分離]** 對話框。

   ![分離操作將完全刪除源副本和即時副本之間的關係](assets/livecopy_detach.png)

   *圖：分離操作將完全刪除源副本和即時副本之間的關係。*

   >[!CAUTION]
   >
   >按一下後，將立即刪除關係 **[!UICONTROL 分離]** 的雙曲餘切值。 無法通過按一下 **[!UICONTROL 取消]** 的子菜單。

或者，您可以快速將即時副本資料夾中的多個資產從 **[!UICONTROL 即時複製概述]** 控制台。 請參 [閱對即時副本資料夾中的許多資產採取動作](#bulk-actions)。

## 即時複製資料夾中的批量操作 {#bulk-actions}

如果您在一個即時副本資料夾中有多個資產，則啟動每個資產的操作會非常繁瑣。 您可以快速啟動來自 [!UICONTROL 即時複製控制台]。 上述方法繼續適用於單個資產。

1. 選擇源資料夾。 按一下 **[!UICONTROL 屬性]** 的子菜單。 或者，使用鍵盤快捷鍵 `p`。
1. 按一下「 **[!UICONTROL 即時複製來源」]**。若要開啟主控台，請按一下「即 **[!UICONTROL 時複製概述」]**。
1. 在此控制面板中，從即時複製資料夾選取即時複製資產。從工具列按一下所需的動作。可用的操作有 **[!UICONTROL 同步]**、重置 **[!UICONTROL 、]**&#x200B;掛起 ****&#x200B;和 ****&#x200B;分離。您可以快速啟動對任意數量的即時複製資料夾中與選定源資料夾處於即時關係的任何資產的這些操作。

   ![從Live Copy概述控制台輕鬆更新即時複製資料夾中的許多資產](assets/livecopyconsole_update_many_assets.png)

   *圖：從中輕鬆更新即時拷貝資料夾中的許多資產 [!UICONTROL 即時複製概述] 控制台。*

<!-- TBD: Can MSM be extended using Java APIs in CS?

## Extend MSM for [!DNL Assets] {#extend-api}

[!DNL Experience Manager] lets you extend the functionality using the MSM Java APIs. For [!DNL Assets], the extending works just the same as it works with MSM for [!DNL Sites]. For details, see [Extending the MSM](/help/sites-developing/extending-msm.md) and the following for information about specific tasks:

* [Overview of APIs](/help/sites-developing/extending-msm.md#overview-of-the-java-api)
* [Create a synchronization action](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action)
* [Create a rollout configuration](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration)
* [Create and use a simple LiveActionFactory class](/help/sites-developing/extending-msm.md#creating-and-using-a-simple-liveactionfactory-class)

-->

## 資產管理任務對即時拷貝的影響 {#manage-assets}

即時拷貝和源是可以在某種程度上作為數字資產進行管理的資產或資料夾。 中的某些資產管理任務 [!DNL Experience Manager] 對即時拷貝有特定影響。

* 複製即時拷貝時，建立與第一個即時拷貝具有相同源的即時拷貝資產。
* 移動源或其即時副本時，將保留即時關係。
* 編輯操作不適用於即時複製資產。 如果即時副本的源本身是即時副本，則編輯操作對它不起作用。
* 簽出操作不可用於即時複製資產。
* 對於源資料夾，可以使用建立審閱任務的選項。
* 在清單視圖和列視圖中查看資產清單時，即時複製資產或資料夾將顯示「即時複製」。 它幫助您輕鬆識別資料夾中的即時副本。

## 比較MSM [!DNL Assets] 和 [!DNL Sites] {#comparison}

在更多情況下，MSM [!DNL Assets] 與MSM的「站點」功能的行為匹配。 需要注意的一些關鍵區別是：

* MSM的藍圖 [!DNL Sites] 在MSM中為 [!DNL Assets]。
* 在「站點」中，您可以比較藍圖及其即時副本，但是在 [!DNL Assets] 將源與其即時副本進行比較。
* 無法在中編輯即時副本 [!DNL Assets]。
* 網站通常有孩子，但 [!DNL Assets] 別這樣。 建立單個資產的即時副本時，不存在包含或排除子項的選項。
* MSM不支援刪除建立站點嚮導中的章節步驟 [!DNL Assets]。
* 在MSM中不支援在頁面屬性上配置MSM鎖 [!DNL Assets]。
* MSM用於 [!DNL Assets]，僅使用 **[!UICONTROL 標準部署配置]**。 其他部署配置不適用於MSM [!DNL Assets]。

## MSM的局限性和已知問題 [!DNL Assets] {#limitations}

以下是MSM的限制 [!DNL Assets]。

* 不支援內容片段。 嘗試建立即時副本時，內容片段將按原樣複製，而不與任何關係。 複製的內容片段是一個及時的快照，在更新原始內容片段時不進行更新。

* 啟用元資料寫回時，MSM不工作。 寫回後，遺產就會斷。
