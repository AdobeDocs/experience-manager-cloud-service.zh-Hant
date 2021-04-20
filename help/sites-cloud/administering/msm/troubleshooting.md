---
title: 疑難排解MSM問題及常見問題
description: 瞭解如何疑難排解最常見的MSM相關問題，並取得最常見的MSM相關問題的解答。
feature: Multi Site Manager
role: Administrator
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---


# 疑難排解MSM問題及常見問答{#troubleshooting-msm}

## 疑難排解第一步{#first-steps}

如果您遇到MSM中的錯誤行為或錯誤，請務必在開始和詳細的故障排除之前：

* 請查看[MSM常見問答集](#faq)，因為您的問題或問題可能已在此處解決。
* 查看[MSM最佳實務文章](best-practices.md)，提供一些提示，並澄清一些誤解。

## 尋找有關您藍圖和即時副本狀態{#advanced-info}的進階資訊

MSM在資源URL上註冊多個可向選擇器請求的servlet。 UI會使用這些功能，但您也可以直接要求這些功能，以直接查看您頁面的其他進階計算MSM狀態：

1. `http://<host>:<port>/content/path/to/bluprint/page.blueprint.json?&maxSize=500&advancedStatus=true&returnRelationships=true&msm%3Atrigger=ROLLOUT`
   * 在Blueprint頁面上使用此選項，可擷取連結到該頁面的所有即時副本清單，以及其他即時副本狀態資訊。
1. `http://<host>:<port>/content/path/to/livecopy/page.msm.json`
   * 在即時副本頁面上使用此功能，可擷取其與Blueprint頁面連線的進階資訊。 如果頁面不是即時副本，則不會傳回任何內容。

這些servlet通過`com.day.cq.wcm.msm`記錄程式生成DEBUG日誌消息，這也會有所幫助。

## 在儲存庫{#checking-repo}中檢查MSM特定資訊

先前的servlet返回基於MSM特定節點和混合的計算資訊。 資訊以下列方式儲存在儲存庫中。

* `cq:LiveSync` 混音類型
   * 這是在`jcr:content`節點上設定，並定義根即時副本頁面。
   * 這些頁面將具有`cq:LiveSyncConfig`類型`cq:LiveCopy`的子節點，該子節點將通過以下屬性包含有關即時副本的基本和強制資訊：
      * `cq:master` 指向即時副本的藍圖頁面。
      * `cq:rolloutConfigs` 指出套用至即時副本的作用中轉出設定。
      * `cq:isDeep` 如果此根即時副本頁面的子頁面包含在即時副本中，則為true。
* `cq:LiveRelationship` 混音類型
   * 任何即時副本頁面的`jcr:content`節點上都有此類混合類型。
   * 如果沒有，頁面在某個時刻已經分離或透過「即時副本」動作（建立或轉出）以外的製作介面手動建立。
* `cq:LiveSyncCancelled` 混音類型
   * 已新增至暫停之即時副本頁面的`jcr:content`節點。
   * 如果暫停對子頁面也有效，則在同一節點上將`cq:isCancelledForChildren`屬性設為true。

這些屬性中的資訊應反映在UI中，但是，在排除故障時，在發生MSM操作時，直接在儲存庫中觀察MSM行為可能很有幫助。

瞭解這些屬性對於查詢儲存庫和查找特定狀態的頁集也非常有用。 例如：

* `select * from cq:LiveSync` 傳回所有即時副本根頁面。

## 常見問答{#faq}

以下是與MSM和即時內容相關的常見問題。

### 為什麼在MSM推出期間，有些屬性（例如標題、註解）未更新？{#missing-properties}

MSM同步動作具有高度可配置性。 在展開期間修改的屬性或元件直接取決於這些組態的屬性。

如需此主題的詳細資訊，請參閱[本文](best-practices.md)。

### 如何移除一組作者的轉出權限？{#remove-rollout-permissions}

對於承擔者（用戶或組），沒有可設定或移除的&#x200B;**轉出&lt;a1/AEM>權限。**

您也可以：

* 自訂產品UI，以隱藏指定承擔者的「轉出」動作。
* 從「即時副本」樹狀結構中，移除不允許捲動的作者的寫入權限。

### 我為何會看到尾碼為&quot;_msm_moved&quot;的即時副本頁面？{#moved-pages}

如果藍圖頁面已推出，它將會更新其「即時副本」頁面，或建立新的「即時副本」頁面（如首次推出或手動刪除「即時副本」頁面）。

但在後一種情況下，如果存在同名的`cq:LiveRelationship`屬性的頁面，則在建立「即時副本」頁面之前，將相應地更名此頁面。

依預設，推出時會預期連結的即時副本頁面，藍圖更新將會發佈到該頁面，或建立即時副本頁面時不會顯示頁面。

如果找到「獨立」頁面，MSM會選擇重新命名此頁面，並建立個別的連結即時副本頁面。

「即時副本」子樹中的這種獨立頁面通常是&#x200B;**Detach**&#x200B;操作的結果，或者作者手動刪除了以前的「即時副本」頁面，然後以相同的名稱重新建立。

為避免此問題，請使用「即時副本&#x200B;**暫停**」功能，而不使用「分離」功能。 ****&#x200B;本文[中&#x200B;**Detach**&#x200B;動作的詳細資訊。](creating-live-copies.md)
