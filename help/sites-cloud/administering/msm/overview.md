---
title: 重複使用內容 — 多網站管理員和即時副本
description: 了解如何使用AEM強大的Live Copy和Multi Site Manager功能的內容。
feature: Multi Site Manager
role: Admin
exl-id: 22b4041f-1df9-4189-8a09-cbc0c89fbf2e
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '2682'
ht-degree: 0%

---

# 重複使用內容：多網站管理員和即時副本 {#multi-site-manager-and-live-copy}

Multi Site Manager(MSM)可讓您在多個位置中使用相同的網站內容。 MSM會使用其Live Copy功能來達成此目標。

* 透過MSM，您可以：
   * 先建立內容一次
   * 在其他區域重複使用此內容(透過 [Live Copies](#live-copies))或其他網站。
* 然後MSM會維護來源內容與其Live Copy之間的即時關係，以便：
   * 當您對源內容進行更改時，將同步源和Live Copy。
   * 您只能透過中斷個別子頁面和/或元件的即時關係，對即時副本的內容進行調整。

本頁概略說明如何重複使用MSM內容。 下面將詳細介紹相關問題。

* [建立和同步Live Copy](creating-live-copies.md)
* [Live Copy概述主控台](live-copy-overview.md)
* [配置Live Copy同步](live-copy-sync-config.md)
* [MSM轉出衝突](rollout-conflicts.md)
* [MSM最佳實務](best-practices.md)

## 可能的情況 {#possible-scenarios}

MSM和Live Copy有許多使用案例。 有些情況包括：

* **跨國公司 — 全球到本地公司**

   MSM支援的一個典型使用案例是在多個跨國相同語言網站中重複使用內容。 這允許核心內容被重複使用，同時允許國家變化。

   例如， [WKND教學課程範例](/help/implementing/developing/introduction/develop-wknd-tutorial.md) 是為美國客戶建立的。 此網站中的大部分內容也可用於其他WKND網站，以迎合不同國家和文化的英語客戶。 所有網站的核心內容都保持不變，而且可進行地區調整。

   下列結構可用於美國和加拿大的網站。 注意方式 `language-masters` 節點不僅維護英語，還維護其他語言內容的主副本。 此內容可作為英文以外其他地區語言內容的基礎。

   ```xml
   /content
       |- wknd
           |- language-masters
               |- en
               |- es
               |- fr
           |- us
               |- en
               |- es
           |- ca
               |- en
               |- fr
   ```

   >[!NOTE]
   >
   >MSM不會翻譯內容。 它可用來建立所需的結構並部署內容。
   >
   >
   >請參閱 [轉譯多語言網站的內容](/help/sites-cloud/administering/translation/overview.md) 例如。

* **國家 — 總部至區域分部**

   或者，擁有經銷商網路的公司可能希望為其個別經銷商建立不同的網站，每個網站都是總部提供的主要網站的變體。 這可能適用於擁有多個地區辦事處的單一公司，或由中央特許經營者和多個地方特許經營者組成的全國特許經營系統。

   總辦事處可提供核心資訊，而區域實體可添加當地資訊，如聯繫詳情、開業時間和活動。

   ```xml
   /content
       |- head-office-berlin
       |- branch-hamburg
       |- branch-stuttgart
       |- branch-munich
       |- branch-frankfurt
   ```

* **多個版本**

   MSM可建立特定子分支的版本。 例如，支援子站點可以保留特定產品的不同版本的詳細資訊，在這些版本中，基本資訊保持不變，只需更改更新的功能：

   ```xml
   /content
       |- game-support
           |- polybius
               |- v5.0
               |- v4.0
               |- v3.0
               |- v2.0
               |- v1.0
   ```

   >[!TIP]
   >
   >在這種情況下，問題是要製作簡單的副本，還是使用即時副本，這是平衡的：
   >
   >* 有多少核心內容需要更新至多個版本。
   >
   >反對：
   >
   >* 需要調整多少個單個副本。


## 從UI進行MSM {#msm-from-the-ui}

您可透過適當控制台的各種選項，直接在UI中存取MSM。

* **建立網站** (**網站**)

   * MSM可協助您管理多個共用相同內容的網站。 例如，網站通常為國際受眾提供，因此大部分內容在所有國家/地區都是共有的，而其中的一部分內容是個別國家/地區特有的。 MSM可讓您 [建立Live Copy，以根據您的來源網站自動更新一個或多個網站](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). 這也可協助您強制建立通用的基礎結構、跨多個網站使用通用內容、維持通用的外觀和風格，並著重於管理實際上不同網站的內容。 以此方式建立網站：
      * 需要預先定義的Blueprint配置來指定源。
      * 建立（預先定義）來源的即時副本。
      * 為使用者提供 **轉出** 按鈕。

* **建立即時副本** (**網站**)

   * MSM可讓您 [建立網站個別頁面或子分支的臨機（一次性）即時副本。](creating-live-copies.md#creating-a-live-copy-of-a-page) 例如，複製子分支以提供關於產品的新版本/更新版本的資訊。 以下列方式建立即時副本：
      * 建立隨選即時副本（不需要Blueprint設定）。
      * 可用來（立即）建立任何頁面/分支的即時副本。
      * 需要 **同步** (不提供 **轉出** 按鈕)。

* **檢視屬性** (**網站**)

   * 如果適合，此選項可協助您 [監視您的Live Copy](creating-live-copies.md#monitoring-your-live-copy) 提供有關 **Live Copy** 或 **Blueprint**.

* **參考** (**網站**)

   * 此 [參考](/help/sites-cloud/authoring/getting-started/basic-handling.md#references) 邊欄提供關於 **Live Copies** 以及適當動作的存取權。

* **即時副本概述** (**網站**)

   * 此主控台可讓您 [檢視及管理您的Blueprint及其Live Copy。](live-copy-overview.md)

* **藍圖** (**工具** - **網站**)

   * 此主控台可讓您 [建立和管理您的blueprint設定。](creating-live-copies.md#creating-a-blueprint-configuration)

>[!NOTE]
>
>MSM功能的某些方面會用於數個其他AEM功能，例如Launchs。 在這些情況下，即時副本是由該功能管理。

### 使用的詞語 {#terms-used}

概述MSM所使用之主要術語。 後續章節及頁面會詳細說明這些內容。

| 詞彙 | 定義 | 更多詳情 |
|---|---|---|
| 來源 | 作為Live Copy基礎的原始頁面 | 與「藍圖」和/或「藍圖」頁同義 |
| 即時副本 | 由同步動作維護的復本（來源的），如轉出設定所定義 |  |
| Live Copy設定 | Live Copy的設定詳細資訊定義 |  |
| 即時關係 | 指定資源繼承的有效定義，即源和Live Copy之間的連接 | 確保對源的更改可以與Live Copy同步 |
| Blueprint | 與源同義 | 可由Blueprint設定定義 |
| Blueprint設定 | 指定源路徑的預定義配置 | 當Blueprint設定中參考Blueprint頁面時，「轉出」命令即可使用 |
| 章節 | 要包含在即時副本中的Blueprint區段 | 這些通常是根的子頁面 |
| 同步 | 在來源和即時副本之間同步內容的通用術語（由兩者同時使用） **轉出** 和 **同步** 選項) |  |
| 轉出 | 從來源同步至即時副本 | 可由作者（在Blueprint頁面上）或系統事件（由轉出設定定義）觸發 |
| 轉出設定 | 決定要同步哪些屬性、同步方式和同步時間的規則 |  |
| 同步 | 從Live Copy頁面手動請求同步 |  |
| 繼承 | Live Copy頁面/元件會在同步發生時從其來源頁面/元件繼承內容 |  |
| 擱置 | 暫時移除即時副本與其Blueprint頁面之間的即時關係 |  |
| 分離 | 永久移除即時副本與其Blueprint頁面之間的即時關係 |  |
| 重設 | 重設「即時副本」頁面以移除所有繼承取消，並將頁面傳回與來源頁面相同的狀態 | 重置會影響您對頁面屬性、段落系統和元件所做的任何更改。 |
| 淺 | 單一頁面的即時副本 |  |
| 深入 | 頁面的即時副本及其子頁面 |  |

<!--
>[!TIP]
>
>See [Overview of the Java API](/help/sites-developing/extending-msm.md#overview-of-the-java-api) for the object names.
-->

## 即時副本 {#live-copies}

MSM Live Copy是特定網站內容的復本，與原始來源維持即時關係：

* Live Copy會繼承來源的內容。
* 當對源進行更改時，同步執行實際內容傳輸。
* 即時副本可視為：
   * 淺：單頁
   * 深：頁面及其子頁面
* 同步規則（稱為轉出設定）可決定要同步的屬性以及同步發生的時間。

在上一個範例中， `/content/wknd/language-masters/en` 是全域的英文主網站。 若要重複使用此網站的內容，會建立MSM Live Copy:

* 以下內容 `/content/wknd/language-masters/en` 是來源。
* 以下內容 `/content/wknd/language-masters/en` 複製到 `/content/wknd/us/en/` 和 `/content/wknd/ca/en` 節點。 這些是即時副本。
* 作者對下列頁面進行變更 `/content/wknd/language-masters/en`.
* 觸發時，MSM會將這些變更同步至即時副本。

### 即時副本 — 組成 {#live-copies-composition}

>[!NOTE]
>
>本節中的圖表和說明表示潛在Live Copy的快照。 這些功能並非完整，但會提供概覽以強調特定特性。

當您初次建立即時副本時，選取的來源頁面會以1:1的方式反映在即時副本中。 之後，新資源（頁面和/或段落）也可直接在Live Copy中建立，因此請務必注意這些變數及其對同步的影響，這是很實用的。 可能的組合物包括：

* [包含非Live-Copy頁面的Live Copy](#live-copy-with-non-live-copy-pages)
* [巢狀即時副本](#nested-live-copies)

Live Copy的基本形式有：

* 以1:1為基礎反映所選來源頁面的即時副本頁面。
* 一個配置定義。
* 為每個資源定義的即時關係：
   * 將即時副本資源與其Blueprint/來源連結。
   * 用於實現繼承和轉出。

變更可以是 [已同步](creating-live-copies.md#synchronizing-your-live-copy) 根據要求。

![即時副本組成概觀](../assets/live-copy-composition.png)

#### 包含非即時副本頁面的即時副本 {#live-copy-with-non-live-copy-pages}

當您在AEM中建立Live Copy時，可以查看並導覽Live Copy分支，並在Live Copy分支上使用一般的AEM功能。 這表示您（或程式）可以在Live Copy中建立新資源（頁面和/或段落）。 例如特定地區或國家的產品。

* 這些資源與來源/Blueprint頁面沒有即時關係，且不會同步。
* MSM可能會以特殊情況處理的情況。 例如，當您（或程式）在來源/Blueprint和Live Copy分支中建立位置和名稱相同的頁面時。 若是這種情況，請參閱 [MSM轉出衝突](rollout-conflicts.md) 以取得更多資訊。

![包含非Live Copy頁面的Live Copy](../assets/live-copy-with-non-live-copy-pages.png)

#### 巢狀即時副本 {#nested-live-copies}

當您（或程式）建立 [現有即時副本中的新頁面](#live-copy-with-non-live-copy-pages) 此新頁面也可設為不同Blueprint的即時副本。 這稱為巢狀即時副本。 在巢狀即時副本中，第二個或內部即時副本的行為會以下列方式受到第一個或外部即時副本的影響：

* 頂層即時副本觸發的深層轉出可繼續進入巢狀即時副本。
* 來源之間的任何連結將在Live Copy中重寫。

例如，從第二個到第一個Blueprint的連結將重寫為從巢狀/第二個Live Copy指向第一個Live Copy的連結。

![巢狀即時副本](../assets/live-copy-nested.png)

>[!NOTE]
>
>如果您在Live Copy分支內移動或重新命名頁面，這會視為巢狀Live Copy，以讓AEM追蹤關係。

#### 堆疊即時副本 {#stacked-live-copies}

當即時副本建立為淺層即時副本的子項時，即稱為堆疊即時副本。 其行為方式與 [巢狀即時副本](#nested-live-copies).

### 源、藍圖和藍圖配置 {#source-blueprints-and-blueprint-configurations}

任何頁面或頁面的分支皆可作為即時副本的來源。 不過，MSM也可讓您定義Blueprint設定，以指定來源路徑。 使用Blueprint配置的好處是：

* 允許作者使用 **轉出** 藍圖上的「 」選項。 也就是說，將修改明確推送至繼承自此Blueprint的Live Copy。
* 允許作者使用 **建立網站**. 這可讓使用者輕鬆選取語言並設定Live Copy的結構。
* 為與Blueprint有關係的Live Copy定義預設轉出設定。

Live Copy的來源可以是一般頁面或Blueprint設定涵蓋的頁面。 兩者皆為有效的使用案例。

來源會形成即時副本的藍圖。 當您執行下列任一動作時，就會定義Blueprint:

* [建立Blueprint設定](creating-live-copies.md#creating-a-blueprint-configuration)  — 設定會預先定義要用來建立Live Copy的頁面。
* [建立頁面的即時副本](creating-live-copies.md#creating-a-live-copy-of-a-page)  — 用來建立Live Copy的頁面（來源頁面）為Blueprint頁面。 Blueprint設定可能參照或未參照來源頁面。

### 轉出與同步 {#rollout-and-synchronize}

轉出是與即時副本與其來源同步的中央MSM動作。 您可以手動執行轉出，也可以自動執行。

* A [轉出設定](#rollout-configurations) 可定義為 [事件](live-copy-sync-config.md#rollout-triggers) 會導致自動轉出。
* 編寫Blueprint頁面時，您可以使用 **[轉出](creating-live-copies.md#rolling-out-a-blueprint)** 命令將變更推送至Live Copy。
   * 此 **轉出** 命令可在blueprint配置引用的blueprint頁面上使用。

   ![轉出](../assets/live-copy-rollout.png)

* 編寫Live Copy頁面時，您可以使用 **[同步](creating-live-copies.md#synchronizing-a-live-copy)** 命令將更改從源提取到Live Copy。
   * 此 **同步** 無論源/blueprint頁面是否包含在blueprint配置中，命令都始終可用於Live Copy頁面。

   ![同步](../assets/live-copy-synchronize.png)

### 轉出設定 {#rollout-configurations}

轉出設定會定義Live Copy與來源內容同步的時間和方式。 轉出設定包含觸發器和一或多個同步動作：

* **觸發**  — 觸發器是導致即時動作同步發生的事件，例如啟動來源頁面。 MSM會定義您可使用的觸發器。
* **同步操作**  — 在Live Copy上執行同步操作，以便與源同步。 範例動作包括複製內容、排序子節點及啟動「即時副本」頁面。 MSM提供一些同步操作。

>[!NOTE]
>
>您可以使用Java API建立執行個體的自訂動作。

轉出設定可重複使用，因此多個Live Copy可使用相同的轉出設定。 數個 [轉出設定](live-copy-sync-config.md#installed-rollout-configurations) 包含在標準安裝中。

### 轉出衝突 {#rollout-conflicts}

轉出可能會變得複雜，尤其是當作者同時編輯來源和即時副本中的內容時。 因此，請注意AEM如何處理任何 [轉出期間可能發生的衝突。](rollout-conflicts.md)

### 掛起和取消繼承和同步 {#suspending-and-cancelling-inheritance-and-synchronization}

即時副本中的每個頁面和元件都會透過即時關係與其來源頁面和元件相關聯。 即時關係會設定來源中即時副本內容的同步。

您可以 **暫停** 即時副本繼承的頁面，以便您可以變更頁面屬性和元件。 暫停繼承時，頁面屬性和元件不再與源同步。

編輯個別頁面時，作者可 **取消繼承** （元件）。 取消繼承時，即時關係會暫停，且該元件不會同步。 當需要自訂內容的子區段時，取消繼承和同步很實用。

### 分離即時副本 {#detaching-a-live-copy}

您也可以 [分離即時副本](creating-live-copies.md#detaching-a-live-copy) 從其藍圖中刪除所有連接。

>[!CAUTION]
>
>「分離」(Detach)操作是永久的且不可逆的。

分離動作會永久移除即時副本與其Blueprint頁面之間的即時關係。 所有與MSM相關的屬性會從Live Copy中移除，而Live Copy頁面會變成獨立副本。

>[!TIP]
>
>請參閱 [分離即時副本](creating-live-copies.md#detaching-a-live-copy) 詳細資訊，包括子頁面和上層頁面的相關影響。

## 使用MSM的標準步驟 {#standard-steps-for-using-msm}

下列步驟說明使用MSM來重複使用內容及同步Live Copy變更的標準程式。

1. 開發來源網站的內容。
1. 決定要使用的轉出設定。

   1. MSM [安裝數項轉出設定](live-copy-sync-config.md#installed-rollout-configurations) 可滿足許多使用案例。
   1. （可選）您可以 [建立轉出設定](live-copy-sync-config.md#creating-a-rollout-configuration) （如果需要）。

1. 決定您需要的位置 [指定要使用的轉出設定](live-copy-sync-config.md#specifying-the-rollout-configurations-to-use) 並視需要進行設定。
1. 如果需要， [建立blueprint設定](creating-live-copies.md#creating-a-blueprint-configuration) 識別即時副本的來源內容。
1. [建立即時副本。](creating-live-copies.md#creating-a-live-copy)
1. 視需要變更來源內容。 您應採用貴組織已建立的一般內容審核和核准程式。
1. [轉出](creating-live-copies.md#rolling-out-a-blueprint) 藍圖，或 [同步即時副本](creating-live-copies.md#synchronizing-a-live-copy) 和變更。

## 自訂MSM {#customizing-msm}

MSM提供工具，讓您的實作能因應共用內容時可能存在的異常複雜情況。

* **自訂轉出設定** - [建立轉出設定](live-copy-sync-config.md#creating-a-rollout-configuration) 安裝的轉出設定不符合您的需求時。 您可以使用任何可用的轉出觸發器和同步動作。

<!--
* **Custom Synchronization Actions** - [Create a custom synchronization action](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action) when the installed actions do not meet your specific application requirements. MSM provides a Java API for creating custom synchronization actions.
-->

## 最佳作法 {#best-practices}

此 [MSM最佳實務](best-practices.md) 頁面包含與您的實作相關的重要資訊。
