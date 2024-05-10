---
title: 使用 MSM 重複使用資產
description: 跨衍生自父資產並連結至該資產的多個頁面/資料夾使用資產。 資產會與主要副本保持同步，只要按幾下，即可從父資產接收更新。
contentOwner: AG
mini-toc-levels: 1
role: User, Admin, Architect
feature: Asset Management,Multi Site Manager
exl-id: a71aebdf-8e46-4c2d-8960-d188b14aaae9
source-git-commit: f7f60036088a2332644ce87f4a1be9bae3af1c5e
workflow-type: tm+mt
source-wordcount: '3407'
ht-degree: 10%

---

# 使用MSM對重複使用資產 [!DNL Assets] {#reuse-assets-using-msm-for-assets}

| 版本 | 文章連結 |
| -------- | ---------------------------- |
| AEM 6.5 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/reuse-assets-using-msm.html) |
| AEM as a Cloud Service  | 本文章 |

中的多站點管理員(MSM)功能 [!DNL Adobe Experience Manager] 可讓使用者重複使用已撰寫一次且可在多個網站位置重複使用的內容。 名稱為MSM的數位資產可使用相同的功能 [!DNL Assets]. 將MSM用於 [!DNL Assets]，您可以：

* 建立資產一次，然後製作這些資產的復本以在網站的其他區域重複使用。
* 將多個副本保持同步，並更新一次原始主副本，以將變更推送到子副本。
* 暫時或永久中止父項與子項資產之間的連結，以進行本機變更。

>[!NOTE]
>
>的MSM [!DNL Assets] 功能包括內容片段，其儲存為 [!DNL Assets] （雖然已視為Sites功能）。

>[!CAUTION]
>
>內容片段的MSM僅適用於透過使用內容片段時 **[!UICONTROL 資產]** 主控台。
>
>MSM功能為 *非* 使用時可用 **[!UICONTROL 內容片段]** 主控台。

## 瞭解MSM的好處和概念 {#concepts}

### 運作方式與優點 {#how-it-works-and-the-benefits}

若要瞭解在多個網站位置重複使用相同內容（文字和資產）的使用案例，請參閱 [可能的MSM案例](/help/sites-cloud/administering/msm/overview.md). [!DNL Experience Manager] 維護原始資產與其連結副本之間的連結，稱為即時副本(LC)。 維持的連結可將集中變更推送至多個即時副本。 這樣可以在消除管理重複副本的限制的同時實現更快的更新。 變更的傳播不會發生錯誤，而且是集中化的。 功能提供空間，讓更新僅限於選取的即時副本。 使用者可以分離連結（亦即中斷繼承），並進行本機編輯，這些編輯在下次更新主要副本並轉出變更時不會遭到覆寫。 分離功能適用於幾個選取的中繼資料欄位或整個資產。 它可讓您在本機靈活地更新原來從主要副本繼承的資產。

MSM會維護來源資產與其即時副本之間的即時關係，以便：

* 來源資產的變更也會套用（轉出）至即時副本，即即時副本會與來源同步。
* 您可以暫停即時關係或移除一些有限欄位的繼承，以更新即時副本。 對來源的修改不再套用至即時副本。

### MSM辭彙表 [!DNL Assets] 辭彙 {#glossary}

**來源：** 原始資產或資料夾。 從中衍生即時副本的主要副本。

**即時副本：** 與其來源同步的源資產/資料夾的副本。 即時副本可以是進一步即時副本的來源。 瞭解如何建立LC。

**繼承：** 即時副本資產/資料夾與其來源之間的連結/參考，系統使用它來記住要將更新傳送至何處。 中繼資料欄位的繼承存在於精細層級，也有內容片段變數和欄位。 可以移除所選專案的繼承，同時保留來源與其即時副本之間的即時關係。

**轉出：** 此動作會將針對來源所做的修改推送至其即時副本的下游。 您可以使用轉出動作一次更新一或多個即時副本。 請參閱轉出。

**轉出設定：** 決定同步哪些屬性、同步方式和時間的規則。 這些設定會在建立即時副本時套用；可以稍後編輯；而且子資產可以從其父資產繼承轉出設定。 對於MSM [!DNL Assets]，僅使用標準轉出設定。 其他轉出設定不適用於MSM的 [!DNL Assets].

**同步：** 除了轉出之外的另一個動作，是將更新從來源傳送至即時副本，以實現來源與其即時副本之間的對等性。 系統會為特定即時副本起始同步處理，而動作會從來源提取變更。 使用此動作時，只能更新其中一個即時副本。 請參閱同步動作。

**暫停：** 暫時移除即時副本與其來源資產/資料夾之間的即時關係。 您可以恢復關係。 請參閱暫停動作。

**繼續：** 恢復即時關係，以便即時副本再次開始從來源接收更新。 請參閱恢復動作。

**重設：** 重設動作會覆寫所有本機變更，使即時副本再次成為來源的復本。 它也會移除繼承取消，並重設所有中繼資料欄位的繼承。 若要日後進行本機修改，您必須再次取消特定欄位的繼承。 請參閱LC的本機修改。

**分離：** 不可撤銷地移除即時副本資產/資料夾的即時關係。 分離動作後，即時副本永遠無法接收來自來源的更新，且不再為即時副本。 請參閱移除關係。

## 建立資產的即時副本 {#create-livecopy}

若要從一或多個來源資產或資料夾建立即時副本，請遵循下列其中一項操作：

* 方法1：選取來源資產並按一下 **[!UICONTROL 建立]** > **[!UICONTROL 即時副本]** 從頂部的工具列開啟。
* 方法2：在 [!DNL Experience Manager] 使用者介面，按一下 **[!UICONTROL 建立]** > **[!UICONTROL 即時副本]** 從介面的右上角。

您可以一次建立一個資產或資料夾的即時副本。 您可以建立衍生自資產或即時副本本身的資料夾的即時副本。

若要使用第一種方法建立即時副本，請遵循下列步驟：

1. 選取來源資產或資料夾。 在工具列中按一下 **[!UICONTROL 建立]** > **[!UICONTROL 即時副本]**.

   ![建立即時副本來源 [!DNL Experience Manager] 介面](assets/create_lc1.png)

   *圖：從建立即時副本 [!DNL Experience Manager] 介面。*

1. 選取目的地資料夾。 按一下「**[!UICONTROL 下一步]**」。
1. 提供標題和名稱。 資產沒有子項。 建立資料夾的即時副本時，您可以選擇包含或排除子項。
1. 選取轉出設定。 按一下&#x200B;**[!UICONTROL 建立]**。

若要使用第二個方法建立即時副本，請遵循下列步驟：

1. 在 [!DNL Experience Manager] 介面，從右上角，按一下 **[!UICONTROL 建立]** > **[!UICONTROL 即時副本]**.

   ![建立即時副本來源 [!DNL Experience Manager] 介面](assets/create_lc2.png)

   *圖：從建立即時副本 [!DNL Experience Manager] 介面。*

1. 選取來源資產或檔案夾。 按一下「**[!UICONTROL 下一步]**」。
1. 選取目的地資料夾。 按一下「**[!UICONTROL 下一步]**」。
1. 提供標題和名稱。 資產沒有子項。 建立資料夾的即時副本時，您可以選擇包含或排除子項。
1. 選取轉出設定。 按一下&#x200B;**[!UICONTROL 建立]**。

>[!NOTE]
>
>移動來源或即時副本時，會保留關係。 刪除即時副本時，會移除關係。

## 檢視來源和即時副本的各種屬性和狀態 {#properties}

您可以從以下各個區域檢視即時副本的資訊和MSM相關狀態，例如關係、同步、轉出等 [!DNL Experience Manager] 使用者介面。

資產和資料夾的運作方式如下：

* 選取即時副本資產，並在其「屬性」頁面中尋找資訊。
* 選取來源資料夾，並尋找每個即時副本的詳細資訊，從 [!UICONTROL 即時副本主控台].

>[!TIP]
>
>若要檢查幾個個別即時副本的狀態，請使用第一個方法來檢查 **[!UICONTROL 屬性]** 頁面。 若要檢查多個即時副本的狀態，請使用第二個方法來檢查 **[!UICONTROL 關係狀態]** 頁面。

### 即時副本的資訊和狀態 {#status-lc-asset}

若要檢查即時副本資產或資料夾的資訊和狀態，請按照以下步驟操作。

1. 選取即時複製資產或資料夾。 按一下 **[!UICONTROL 屬性]** 工具列中的。 或者，使用鍵盤快速鍵 `p`.
1. 按一下 **[!UICONTROL 即時副本]**. 您可以檢查來源的路徑、暫停狀態、同步化狀態、上次轉出日期以及上次轉出的使用者。

   ![即時副本資訊和狀態會顯示在「屬性」的控制檯中](assets/lcfolder_info_properties.png)

   *圖：即時副本資訊和狀態。*

1. 如果子資產借用即時副本設定，您可以啟用或停用。

1. 您可以選擇即時副本的選項，以從父項繼承轉出設定或變更設定。

### 資料夾所有即時副本的資訊和狀態 {#status-lc-folder}

[!DNL Experience Manager] 提供一個主控台來檢查來源資料夾的所有即時副本的狀態。 此主控台顯示所有子資產的狀態。

1. 選取來源資料夾。 按一下 **[!UICONTROL 屬性]** 工具列中的。 或者，使用鍵盤快速鍵 `p`.
1. 按一下「 **[!UICONTROL 即時複製來源」]**。若要開啟主控台，請按一下「即 **[!UICONTROL 時複製概述」]**。此控制面板提供所有子資產的頂層狀態。

   ![在來源的即時副本控制檯中檢視即時副本的狀態](assets/livecopy-statuses.png)

   *圖：在中檢視即時副本的狀態 [!UICONTROL 即時副本主控台] 來源。*

1. 若要檢視即時副本檔案夾中每個資產的詳細資訊，請選取資產，然後從工具列按一 **[!UICONTROL 下「關係狀態]** 」。

   ![資料夾中即時副本子資產的詳細資訊和狀態](assets/livecopy_relationship_status.png)

   資料夾中即時副本子資產的詳細資訊和狀態

>[!TIP]
>
>您可以快速檢視其他資料夾即時副本的狀態，不必瀏覽太多內容。 從檔案夾的中上部變更檔案夾 **[!UICONTROL 即時副本概觀]** 介面。

### 來源的「參考」邊欄中的快速動作 {#ref-rail-source}

對於來源資產或資料夾，您可以檢視以下資訊，並直接從「參考」邊欄執行下列動作：

* 檢視即時副本的路徑。
* 在中開啟或顯示特定即時副本 [!DNL Experience Manager] 使用者介面。
* 同步特定即時副本的更新。
* 暫停特定即時副本的關係或變更轉出設定。
* 存取即時副本概述主控台。

選取來源資產或資料夾，開啟左側邊欄，然後按一下 **[!UICONTROL 引用]**. 或者，選取資產或資料夾，然後使用鍵盤快速鍵 `Alt + 4`.

![所選來源的「參考」邊欄中可用的動作和資訊](assets/referencerail_source.png)

*圖：在參照邊欄中，所選來源的可用動作和資訊。*

如需特定即時副本，請按一下 **[!UICONTROL 編輯即時副本]** 以暫停關係或變更轉出設定。

![對於特定即時副本，在選取來源資產時，可以從「參考」邊欄存取暫停關係或變更轉出設定的選項](assets/referencerail_editlc_options.png)

*圖：暫停關係或變更特定即時副本的轉出設定。*

### 即時副本的「參考」邊欄中的快速動作 {#ref-rail-lc}

對於即時複製資產或資料夾，您可以檢視以下資訊，並直接從「參考」邊欄執行下列動作：

* 檢視其來源的路徑。
* 在中開啟或顯示特定即時副本 [!DNL Experience Manager] 使用者介面。
* 推出更新。

選取即時複製資產或資料夾，開啟左側導軌，然後按一下「參 **[!UICONTROL 考」]**。或者，選取資產或資料夾，然後使用鍵盤快速鍵 `Alt + 4`.

![在「參考」(References)邊欄中，所選即時副本的可用動作](assets/referencerail_livecopy.png)

*圖：在參照邊欄中，所選即時副本的可用動作。*

## 將修改從來源傳播到即時副本 {#rollout-sync}

修改來源後，可以使用同步動作或轉出動作將變更傳播到即時副本。 若要瞭解這兩個動作之間的差異，請參閱 [字彙表](#glossary).

### 轉出動作 {#rollout}

您可以從來源資產起始轉出動作，並更新所有或數個選取的即時副本。

1. 選取即時複製資產或資料夾。 按一下 **[!UICONTROL 屬性]** 工具列中的。 或者，使用鍵盤快速鍵 `p`.
1. 按一下「 **[!UICONTROL 即時複製來源」]**。按一下 **[!UICONTROL 轉出]** 工具列中的。
1. 選取您要更新的即時副本。 按一下 **[!UICONTROL 轉出]**.
1. 若要轉出對子資產所做的更新，請選取 **[!UICONTROL 轉出來源與所有子項]**.

   ![將來源的修改轉出到幾個或所有即時副本](assets/livecopy_rollout_page.png)

   *圖：將來源的修改轉出到一些或全部即時副本。*

>[!NOTE]
>
>在來源資產中所做的修改只會轉出到直接相關的即時副本。 如果即時副本是從另一個即時副本衍生而來，則修改不會轉出到衍生的即時副本。

或者，您也可以在選取特定即時副本後，從「參照」邊欄啟動轉出動作。 如需詳細資訊，請參閱 [即時副本的「參考」邊欄中的快速動作](#ref-rail-lc). 在此轉出方法中，只會更新選取的即時副本及其選擇性子項。

![將來源的修改轉出到所選的即時副本](assets/livecopy_rollout_dialog.png)

*圖：將來源的修改轉出到所選的即時副本。*

### 關於同步動作 {#about-sync}

同步動作僅將修改從來源提取到所選的即時副本。 同步動作會遵循並維持在取消繼承後完成的本機修改。 不會覆寫本機修改，也不會重新建立取消的繼承。 您可以透過三種方式啟動同步動作。

| 位置 [!DNL Experience Manager] 介面 | 使用的時機與原因 | 使用方式 |
|---|---|---|
| [!UICONTROL 引用] 邊欄 | 當您已選取來源時，請快速同步處理。 | 另請參閱 [來源的「參考」邊欄中的快速動作](#ref-rail-source) |
| 中的工具列 [!UICONTROL 屬性] 頁面 | 當您已經開啟即時副本屬性時，啟動同步。 | 另請參閱 [同步即時副本](#sync-lc) |
| [!UICONTROL 即時副本概觀] 主控台 | 在選取來源資料夾或 [!UICONTROL 即時副本概觀] 主控台已開啟。 系統會一次起始一個資產的同步動作，但可一次同步多個資產的更快速方式。 | 另請參閱 [對即時副本資料夾中許多資產的動作](#bulk-actions) |

### 同步即時副本 {#sync-lc}

若要啟動同步動作，請開啟即 **[!UICONTROL 時副本的「屬性]** 」頁面，按一下「即時 **** 副本」，然後從工具列按一下所要的動作。

要查看與同步操作相關的狀態和資訊，請參 [閱即時副本的資訊和狀態](#status-lc-asset)[以及資料夾所有即時副本的狀態](#status-lc-folder)。

![同步動作提取對來源所做的變更](assets/livecopy_sync.png)

*圖：同步處理動作會提取對來源所做的變更。*

>[!NOTE]
>
>如果關係已暫停，則同步化動作在工具列中無法使用。 雖然「參考」邊欄中提供了同步動作，但即使轉出成功，修改也不會傳播。

## 取消並重新啟用個別專案的繼承 {#canceling-reenabling-inheritance-individual-items}

您可以取消的即時副本繼承：

* 中繼資料欄位
* [內容片段變數](/help/assets/content-fragments/content-fragments-variations.md#inheritance)
* [內容片段資料欄位](/help/assets/content-fragments/content-fragments-variations.md#inheritance)

這表示該專案不再與來源元件同步。 如有需要，您可在稍後啟用繼承。

### 取消先前設定 {#cancel-inheritance}

若要取消繼承，請執行下列動作：

1. 選取 **取消繼承** 圖示，在必要專案旁：

   ![同步動作提取對來源所做的變更](assets/cancel-inheritance-icon.png)

1. 在「取消繼承」對話方塊中，使用「是」確認動作。

### 重啟先前設定 {#reenable-inheritance}

若要重新啟用繼承：

1. 若要啟用專案的繼承，請選取 **重新啟用繼承** 必要專案旁的圖示：

   ![同步動作提取對來源所做的變更](assets/re-enable-inheritance-icon.png)

   >[!NOTE]
   >
   >當您重新啟用繼承時，專案不會自動與來源同步。 如有需要，您可以手動要求同步。

## 暫停並繼續關係 {#suspend-resume}

您可以暫時暫停關係，以防止即時副本接收對來源資產或資料夾所做的修改。 也可以恢復關係，讓即時副本開始從來源接收修改。

若要暫停或繼續，請開啟即 **[!UICONTROL 時副本的「屬性]** 」頁面，按一下「即時副本 **** 」，然後從工具列按一下所要的動作。

或者，您也可以從即時副本概述主控台，快速暫停或繼續即時副本資料夾中多 **[!UICONTROL 個資產的關係]** 。請參 [閱對即時副本資料夾中的許多資產採取動作](#bulk-actions)。

## 對即時副本進行本機修改 {#local-mods}

即時副本是建立時原始來源的復本。 即時副本的中繼資料值繼承自來源。 中繼資料欄位個別維護與來源資產個別欄位的繼承。

不過，您有彈性對即時副本進行本機修改，以變更一些選取的屬性。若要進行本機修改，請取消所要屬性的繼承。當取消一個或多個元資料欄位的繼承時，保留資產的即時關係和其它元資料欄位的繼承。任何同步或轉出都不會覆寫本機修改。若要這麼做，請開啟 **[!UICONTROL 屬性]** 即時副本資產的頁面，按一下 **[!UICONTROL 取消繼承]** 中繼資料欄位旁的選項。

您可以復原所有本機修改，並將資產恢復為其來源的狀態。 重設動作不可撤銷且會立即覆寫所有本機修改，並重新建立所有中繼資料欄位的繼承。 若要還原，請從 **[!UICONTROL 屬性]** 即時副本資產的頁面，按一下 **[!UICONTROL 重設]** 工具列中的。

![重設動作會覆寫本機編輯，並部分將即時副本與其來源匯入。](assets/livecopy_reset.png)

*圖：重設動作會覆寫本機編輯，並使即時副本部分包括其來源。*

## 移除即時關係 {#detach}

您可以使用「分離」動作完全移除來源與即時副本之間的關係。 即時副本在分離後會成為獨立的資產或資料夾。 它會顯示為中的新資產，位於 [!DNL Experience Manager] 介面，在分離後立即執行。 若要從即時副本的來源分離即時副本，請按照以下步驟操作。

1. 選取即時複製資產或資料夾。 按一下 **[!UICONTROL 屬性]** 工具列中的。 或者，使用鍵盤快速鍵 `p`.

1. 按一下 **[!UICONTROL 即時副本]**. 按一下 **[!UICONTROL 分離]** （在工具列中）。 按一下 **[!UICONTROL 分離]** 從出現的對話方塊。

   ![分離動作會完全移除來源與即時副本之間的關係](assets/livecopy_detach.png)

   *圖：分離動作會完全移除來源和即時副本之間的關係。*

   >[!CAUTION]
   >
   >當您按一下時，關係會立即移除 **[!UICONTROL 分離]** 從對話方塊。 您無法按一下「 」加以還原 **[!UICONTROL 取消]** 在屬性頁面上。

或者，您也可以從以下快速分離即時副本資料夾中的多個資產： **[!UICONTROL 即時副本概觀]** 主控台。 請參 [閱對即時副本資料夾中的許多資產採取動作](#bulk-actions)。

## 即時副本資料夾中的大量動作 {#bulk-actions}

如果您在即時副本資料夾中有多個資產，對每個資產起始動作可能會很繁瑣。 您可以對許多資產快速啟動基本動作，從 [!UICONTROL 即時副本主控台]. 上述方法可繼續用於個別資產。

1. 選取來源資料夾。 按一下 **[!UICONTROL 屬性]** 工具列中的。 或者，使用鍵盤快速鍵 `p`.
1. 按一下「 **[!UICONTROL 即時複製來源」]**。若要開啟主控台，請按一下「即 **[!UICONTROL 時複製概述」]**。
1. 在此控制面板中，從即時複製資料夾選取即時複製資產。從工具列按一下所需的動作。可用的動作包括 **[!UICONTROL 同步]**， **[!UICONTROL 重設]**， **[!UICONTROL 暫停]**、和 **[!UICONTROL 分離]**. 您可以在任何數量的即時副本資料夾中，對與所選來源資料夾處於即時關係的任何資產快速啟動這些動作。

   ![從即時副本概述控制檯輕鬆更新即時副本資料夾中的許多資產](assets/livecopyconsole_update_many_assets.png)

   *圖：從輕鬆更新即時副本資料夾中的許多資產 [!UICONTROL 即時副本概觀] 主控台。*

<!-- TBD: Can MSM be extended using Java APIs in CS?

## Extend MSM for [!DNL Assets] {#extend-api}

[!DNL Experience Manager] lets you extend the functionality using the MSM Java APIs. For [!DNL Assets], the extending works just the same as it works with MSM for [!DNL Sites]. For details, see [Extending the MSM](/help/sites-developing/extending-msm.md) and the following for information about specific tasks:

* [Overview of APIs](/help/sites-developing/extending-msm.md#overview-of-the-java-api)
* [Create a synchronization action](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action)
* [Create a rollout configuration](/help/sites-developing/extending-msm.md#creating-a-new-rollout-configuration)
* [Create and use a simple LiveActionFactory class](/help/sites-developing/extending-msm.md#creating-and-using-a-simple-liveactionfactory-class)

-->

## 資產管理任務對即時副本的影響 {#manage-assets}

即時副本和來源是可當作數位資產在一定程度上管理的資產或資料夾。 中的部分資產管理任務 [!DNL Experience Manager] 對即時副本有特定影響。

* 複製即時副本時，會建立與第一個即時副本具有相同來源的即時副本資產。
* 當您移動來源或其即時副本時，即時關係會保留。
* 編輯動作不適用於即時副本資產。 如果即時副本的來源本身是即時副本，則編輯動作對其無效。
* 簽出動作不適用於即時副本資產。
* 對於來源資料夾，可以使用建立稽核任務的選項。
* 在清單檢視和欄檢視中檢視資產清單時，即時副本資產或資料夾會針對其顯示「即時副本」。 它可協助您輕鬆識別資料夾中的即時副本。

## 比較MSM [!DNL Assets] 和 [!DNL Sites] {#comparison}

在更多案例中，MSM用於 [!DNL Assets] 符合MSM for Sites功能的行為。 需要注意的主要差異如下：

* MSM中的Blueprint用於 [!DNL Sites] 在MSM中為稱為即時副本來源 [!DNL Assets].
* 在Sites中，您可以比較Blueprint及其即時副本，但無法在中比較 [!DNL Assets] 比較來源與其即時副本。
* 您無法在中編輯即時副本 [!DNL Assets].
* 網站通常有子項，但 [!DNL Assets] 不要。 建立個別資產的即時副本時，包含或排除子項的選項不存在。
* 的MSM不支援在建立網站精靈中移除章節步驟 [!DNL Assets].
* MSM不支援在頁面屬性上設定MSM鎖定 [!DNL Assets].
* 對於MSM [!DNL Assets]，僅使用 **[!UICONTROL 標準轉出設定]**. 其他轉出設定不適用於MSM的 [!DNL Assets].

>[!NOTE]
>
>請記住，內容片段的MSM (透過 **[!UICONTROL 資產]** console)使用Assets功能，這是因為它們會儲存為Assets （雖然視為Sites功能）。

## MSM的限制和已知問題 [!DNL Assets] {#limitations}

以下是MSM對的限制 [!DNL Assets].

* MSM不適用於已啟用中繼資料回寫。 回寫時，繼承中斷。

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
* [使用內容片段](/help/assets/content-fragments/content-fragments.md)
* [發佈資產至 AEM 和 Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)