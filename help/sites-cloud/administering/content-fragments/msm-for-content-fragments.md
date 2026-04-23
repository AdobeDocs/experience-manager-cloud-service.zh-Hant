---
title: 使用MSM和即時副本重複使用內容片段
description: 瞭解如何使用MSM的即時副本功能，以便在多個位置使用相同或類似的內容片段內容，同時與來源內容同步。
badgeSaas: label="AEM Sites" type="Positive" tooltip="適用於AEM Sites)。"
feature: Content Fragments
role: User
solution: Experience Manager Sites
hide: true
hidefromtoc: true
index: false
source-git-commit: 85b72909597a95531aea51719c841bc5db9c1a21
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 3%

---

# 使用MSM重複使用內容片段 {#reuse-content-fragments-using-msm}

多站點管理員(MSM)和即時副本功能可讓您在多個位置使用相同的內容，同時與來源內容同步。

<!-- CQDOC-23473 - feature is currently beta so page is hidden, see metadata -->
<!-- CQDOC-23473 - screenshots -->
<!-- CQDOC-23473 - only mentioned once in ToC, add entries -->
<!-- CQDOC-23473 - will work on folders -->

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

>[!CAUTION]
>
>內容片段主控台的MSM目前是Beta功能，僅供特定客戶使用。
>
>透過&#x200B;**Assets**&#x200B;主控台使用內容片段時，也可以使用MSM取得內容片段。

* 使用MSM即時副本，您可以：
   * 建立內容一次
   * 在相同網站的其他區域、其他網站或應用程式中重複使用此內容。
* 然後，MSM 維護您的來源內容與其 Live Copy 之間的即時關係，以便：
   * 當您變更來源內容時，來源和即時副本會同步。
   * 您可以中斷個別子片段和/或元件的即時關係來只調整即時副本的內容。

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

如需MSM概念的詳細概觀，請參閱重複使用內容：多站點管理員和即時副本。

<!--
For a detailed overview of MSM concepts see [Reusing Content: Multi Site Manager and Live Copy](/help/sites-cloud/administering/msm/overview.md).
-->

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

>[!NOTE]
>
>Adobe Experience Manager中的多網站管理員(MSM)功能可讓使用者重複使用製作一次的內容，然後跨多個網站位置重複使用。

<!--
>[!NOTE]
>
>[Multi Site Manager (MSM)](/help/sites-cloud/administering/msm/overview.md) functionality in Adobe Experience Manager enables users to reuse content that is authored once and then reused across multiple web-locations. 
-->

使用MSM處理內容片段您可以：

* 建立內容片段一次，然後製作（連結）這些片段的復本，以便在網站或應用程式的其他區域重複使用。
* 更新來源復本一次，然後將變更推送至（即時）復本，保持多個復本同步。
* 暫時或永久地暫停父片段與子片段之間的連結（完全或針對其變數或欄位），以進行本機變更。

內容片段的MSM結合內容片段編輯器中的功能，可讓您中斷並恢復欄位層級的繼承。

<!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

>[!NOTE]
>
>本頁介紹使用&#x200B;**內容片段**&#x200B;主控台時的MSM功能。
>
>透過&#x200B;**Assets**&#x200B;主控台使用內容片段時，也可以使用MSM取得內容片段。

<!--
>[!NOTE]
>
>This page covers MSM functionality when using the **Content Fragments** console.
>
>MSM for Content Fragments is also available when using [Content Fragments via the **Assets** console](/help/assets/content-fragments/content-fragments-msm.md). 
-->

## 建立 Live Copy {#create-a-live-copy}

<!-- CQDOC-23473 - exclude children or referenced content fragments? -->

若要建立內容片段的即時副本：

1. 在內容片段控制檯導覽至片段的位置。
1. 選取您的片段。
1. 從頂端工具列選取&#x200B;**建立即時副本**。
1. 在開啟的對話方塊中，指定目的地並繼續執行&#x200B;**下一步**。
1. 指定屬性。 您可以指定標題、名稱以及即時副本是否應排除子項（巢狀片段）。
1. 繼續&#x200B;**下一步**。
1. 選取您要立即建立即時副本（**立即**），或在&#x200B;**稍後**&#x200B;的日期和時間建立。
1. 向&#x200B;**建立即時副本**&#x200B;確認。

   <!-- CQDOC-23473 - feature is currently beta remove Caution for GA -->

   >[!CAUTION]
   >
   >如果您想使用MSM建立內容片段的復本)，則應該從個別內容片段模式中使用的任何資料型別中移除任何&#x200B;**唯一**&#x200B;限制。

   <!--
   >[!CAUTION]
   >
   >If you want to use MSM to create copies of Content Fragments), then any **Unique** constraints should be removed from any Data Types used in the respective [Content Fragment Models](/help/assets/content-fragments/content-fragments-models.md).
   -->

## 檢視屬性和狀態 {#view-properties-and-status}

若要檢視屬性以及來源和即時副本的狀態：

1. 在內容片段控制檯導覽至片段的位置。
1. 選取您的片段。
1. 選取片段之&#x200B;**Title**&#x200B;欄中的資訊(i)圖示。
右邊的資訊面板將會開啟。
1. 選取&#x200B;**即時副本詳細資料**&#x200B;的索引標籤。

   ![即時副本的資訊](/help/sites-cloud/administering/content-fragments/assets/cf-msm-information.png)

## 傳播修改 {#propagate-modifications}

在來源和您的即時副本之間傳播修改。

### 同步 {#synchronize}

若要觸發將內容更新從即時副本提取至來源的同步：

1. 在內容片段控制檯導覽到片段來源的位置。
1. 選取您的片段。
1. 從工具列選取&#x200B;**同步處理**。
1. 在對話方塊中確認&#x200B;**同步**。

### 推出 {#rollout}

若要觸發將來源更新推送至您即時副本的轉出：

1. 在內容片段控制檯導覽至片段即時副本的位置。
1. 選取您的片段。
1. 從工具列選取&#x200B;**轉出**。 精靈將開啟以引導您完成此程式。
1. 選取要包含在轉出中的即時副本，然後&#x200B;**繼續**。
1. 排程立即轉出（**現在**）或&#x200B;**稍後**。
1. **繼續**&#x200B;視情況而定。

<!-- CQDOC-23473 - feature is beta, is in authoring so remove here when GA -->

## 取消及還原編輯器中的繼承 {#cancel-and-revert-to-inheritance-in-the-editor}

繼承是可自動將內容從一個片段推送到另一個片段的機制。 繼承的欄位和變數可以是多網站管理的產品。

您可以在內容片段編輯器中取消（然後還原為）繼承。 根據內容，這可用於變數，或單個欄位，如果片段是即時副本的一部分。

例如：

* 取消繼承

  ![取消繼承圖示](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-cancel-inheritance.png)

* 還原為繼承（如果繼承已取消）

  ![還原為繼承圖示](/help/sites-cloud/administering/content-fragments/assets/cf-authoring-revert-to-inheritance.png)

<!-- CQDOC-23473 - feature is currently beta reinstate Note for GA -->

<!--
## Cancel, and revert to, inheritance {#cancel-and-reinstate-inheritance}

Inheritance is the mechanism where content can be automatically pushed from one fragment to another. Inherited fields, and variations, can be the product of Multi-Site Management.

You can cancel (then revert) the inheritance. Depending on the context, this can be available for a variation, or an individual field, if the fragment is part of a live copy.
-->

<!--
>[!NOTE]
>
>For more details see [Cancel, and revert to, inheritance in the editor](/help/sites-cloud/administering/content-fragments/authoring.md#cancel-and-revert-to-inheritance).
-->

## 比較內容片段和網站頁面的MSM {#compare-msm-for-content-fragments-and-sites-pages}

<!-- CQDOC-23473 - needs a detailed review -->

在大多數情況下，內容片段的MSM會符合MSM for Sites Pages功能的行為。 需要注意的主要差異如下：

* MSM中Sites頁面的Blueprint稱為MSM中內容片段的即時副本來源。
* 對於網站頁面，您可以比較Blueprint及其即時副本，但內容片段無法比較來源與其即時副本。
* 您無法在內容片段主控台中編輯即時副本。
* 網站頁面通常有子項，但內容片段沒有，儘管它們可能有參照的片段。 包含或排除子項的選項會參照這些參照的片段。
* MSM不支援在內容片段中移除建立網站精靈中的章節步驟。
* 內容片段的MSM不支援在頁面屬性上設定MSM鎖定。
* 對於內容片段的MSM，請僅使用&#x200B;**標準轉出設定**。 其他轉出設定不適用於MSM的內容片段。

>[!NOTE]
>
>請記住，透過內容片段主控台存取的內容片段MSM是根據Assets功能；這是因為它們會儲存為Assets （雖然視為Sites功能）。

## 限制 {#limitations}

* 內容片段不存在修改時觸發程式及相關轉出設定。
