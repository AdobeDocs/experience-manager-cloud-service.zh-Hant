---
title: 重複使用內容——多網站管理員和即時副本
description: 簡介如何運用強大的即時副本AEM和多網站管理員功能來重複使用內容。
feature: Multi Site Manager
role: Administrator
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '2686'
ht-degree: 1%

---


# 重複使用內容：多站點管理器和即時拷貝{#multi-site-manager-and-live-copy}

Multi Site Manager(MSM)可讓您在多個位置使用相同的網站內容。 MSM使用其即時副本功能來達成此目的。

* 有了MSM，您可以：
   * 只要建立內容一次，
   * 將此內容重複用於相同或其他網站的其他區域（透過[即時副本](#live-copies)）。
* 然後，MSM會維持來源內容與其即時副本之間的即時關係，以便：
   * 當您變更來源內容時，來源和即時副本會同步。
   * 您只能透過中斷個別子頁面和／或元件的即時關係，對即時副本的內容進行調整。

本頁概述如何使用MSM的內容。 下面幾頁詳細介紹相關問題。

* [建立和同步即時副本](creating-live-copies.md)
* [即時副本概述主控台](live-copy-overview.md)
* [配置即時拷貝同步](live-copy-sync-config.md)
* [MSM推出衝突](rollout-conflicts.md)
* [MSM最佳實務](best-practices.md)

## 可能的藍本{#possible-scenarios}

MSM和即時副本有許多使用案例。 有些情況包括：

* **跨國公司——全球對本地公司**

   MSM支援的一個典型使用案例是，在多個跨國同文網站中重複使用內容。 這允許核心內容被重複使用，同時允許國家變化。

   例如，為美國客戶建立[WKND教學課程範例](/help/implementing/developing/introduction/develop-wknd-tutorial.md)的英文區段。 本網站的大部分內容也可用於其他WKND網站，以迎合不同國家和文化的英語客戶。 所有網站的核心內容都維持不變，而且可進行區域調整。

   以下結構可用於美國和加拿大的網站。 請注意`language-masters`節點如何維護主副本，不僅包含英文，還包含其他語言內容。 此內容可做為附加地區語言及英文內容的基礎。

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
   >如需範例，請參閱[多語言網站翻譯內容](/help/sites-cloud/administering/translation/overview.md)。

* **國家——總部至區域分支機構**

   或者，擁有經銷商網路的公司可能希望為其個別經銷商單獨建立網站，每個網站都是總部提供的主要網站。 可能是單一公司有多個地區辦事處，或是由中央加盟商和多個地方加盟商組成的全國加盟系統。

   總部可以提供核心資訊，而區域實體可以添加當地資訊，如聯絡詳情、開業時間和活動。

   ```xml
   /content
       |- head-office-berlin
       |- branch-hamburg
       |- branch-stuttgart
       |- branch-munich
       |- branch-frankfurt
   ```

* **多個版本**

   MSM可以建立特定子分支的版本。 例如，支援子網站可以保留特定產品不同版本的詳細資訊，其中基本資訊保持不變，且只需變更更新的功能：

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
   >在這種情況下，這是要製作直接副本還是使用即時副本的問題，這是平衡：
   >
   >* 多少核心內容需要更新至多個版本。
   >
   >反對：
   >
   >* 需要調整的個別副本數量。


## UI {#msm-from-the-ui}中的MSM

MSM可直接在UI中使用適當主控台的各種選項存取。

* **建立網站** (**網站**)

   * MSM可協助您管理多個共用共同內容的網站。 例如，網站通常是為國際觀眾提供的，因此大部分內容在所有國家／地區都很常見，而個別國家／地區的特定內容則有一部分。 MSM允許您[建立即時副本，以便根據源站點](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)自動更新一個或多個站點。 這也可協助您強制建立共同的基本結構、跨多個網站使用共同內容、維持共同的外觀和感覺，並集中精力管理實際不同網站的內容。 以此方式建立網站：
      * 需要預先定義的Blueprint設定來指定來源。
      * 建立（預先定義）來源的即時副本。
      * 為用戶提供&#x200B;**Rolovate**&#x200B;按鈕。

* **建立即時副本** (**網站**)

   * MSM可讓您建立網站個別頁面或子分支的臨機（一次性）即時副本。[](creating-live-copies.md#creating-a-live-copy-of-a-page) 例如，複製子分支以提供有關產品新版／更新版的資訊。以此方式建立即時副本：
      * 建立臨機即時副本（不需要藍圖設定）。
      * 可用來（立即）建立任何頁面／分支的即時副本。
      * 需要&#x200B;**Synchronize**（不提供&#x200B;**Rolovate**&#x200B;按鈕）。

* **檢視屬性** (**網站**)

   * 如果適用，此選項可協助您提供有關&#x200B;**即時副本**&#x200B;或&#x200B;**藍圖**&#x200B;的相關資訊，以協助您監控即時副本。[](creating-live-copies.md#monitoring-your-live-copy)

* **參考** (**網站**)

   * [參考](/help/sites-cloud/authoring/getting-started/basic-handling.md#references)邊欄提供有關&#x200B;**即時副本**&#x200B;的資訊，並可存取適當的動作。

* **即時副本概觀** (**網站**)

   * 此控制台允許您[查看和管理您的藍圖及其即時副本。](live-copy-overview.md)

* **Blueprint** (**工具** -站 **點**)

   * 此控制台允許您[建立和管理Blueprint配置。](creating-live-copies.md#creating-a-blueprint-configuration)

>[!NOTE]
>
>MSM功能的一些方面則用於數種其AEM他功能，例如Launchs。 在這些情況下，即時副本由該功能管理。

### 使用的詞語{#terms-used}

作為簡介，下表概述MSM使用的主要詞語。 後續章節和頁面將會提供更多詳細資訊。

| 詞彙 | 定義 | 詳細資訊 |
|---|---|---|
| 來源 | 作為即時副本基礎的原始頁面 | 與「藍圖」和／或「藍圖」頁面同義 |
| 即時副本 | 由同步操作維護的源副本（源副本），如轉出配置所定義 |  |
| 即時副本設定 | 即時副本的設定詳細資訊定義 |  |
| 即時關係 | 對給定資源繼承的有效定義，即源和即時副本之間的連接 | 確保對源的更改可以與即時副本同步 |
| Blueprint | 與來源同義 | 可由Blueprint組態定義 |
| Blueprint設定 | 指定源路徑的預定義配置 | 當藍圖設定中參考藍圖頁面時，「轉出」命令便可使用 |
| 章 | 要包含在即時副本中的Blueprint區段 | 這些通常是根目錄的子頁面 |
| 同步 | 用於同步源和即時拷貝之間內容的通用術語（由&#x200B;**Rolovate**&#x200B;和&#x200B;**Synchronize**&#x200B;選項共同使用） |  |
| 轉出 | 從來源同步到即時副本 | 可由作者（在藍圖頁面上）或系統事件（由轉出設定定義）觸發 |
| 轉出設定 | 決定要同步哪些屬性、方式和時間的規則 |  |
| 同步 | 從「即時副本」頁面手動請求同步 |  |
| 繼承 | 當同步發生時，即時副本頁面／元件會繼承其源頁面／元件中的內容 |  |
| 擱置 | 臨時移除即時副本與其藍圖頁面之間的即時關係 |  |
| 分離 | 永久移除即時副本與其藍圖頁面之間的即時關係 |  |
| 重設 | 重設「即時副本」頁面以移除所有繼承取消，並將頁面傳回至與來源頁面相同的狀態 | 重設會影響您對頁面屬性、段落系統和元件所做的任何變更。 |
| 淺層 | 單一頁面的即時副本 |  |
| 深入 | 頁面的即時副本及其子頁面 |  |

<!--
>[!TIP]
>
>See [Overview of the Java API](/help/sites-developing/extending-msm.md#overview-of-the-java-api) for the object names.
-->

## 即時副本 {#live-copies}

MSM即時副本是特定網站內容的副本，其與原始來源的即時關係會維持：

* 即時副本會繼承其來源的內容。
* 同步在對源進行更改時執行內容的實際傳輸。
* 即時副本可視為：
   * 淺層：單頁
   * 深度：頁面及其子頁面
* 同步規則（稱為轉出配置）可確定要同步的屬性以及同步發生的時間。

在上例中，`/content/wknd/language-masters/en`是全域英文主體網站。 若要重複使用此網站的內容，請建立MSM即時副本：

* `/content/wknd/language-masters/en`下方的內容是來源。
* `/content/wknd/language-masters/en`下方的內容會複製到`/content/wknd/us/en/`和`/content/wknd/ca/en`節點下方。 這些是即時副本。
* 作者對`/content/wknd/language-masters/en`下的頁面進行變更。
* 觸發時，MSM會將這些變更同步至即時副本。

### 即時副本——構圖{#live-copies-composition}

>[!NOTE]
>
>本節中的圖表和說明表示潛在即時拷貝的快照。 它們不全面，但提供概述以強調特定特性。

當您最初建立即時副本時，選取的來源頁面會以1:1的基準反映在即時副本中。 此後，您也可以直接在即時副本中建立新資源（頁面和／或段落），因此，請務必注意這些變化及其對同步的影響。 可能的構圖包括：

* [包含非即時副本頁面的即時副本](#live-copy-with-non-live-copy-pages)
* [巢狀即時副本](#nested-live-copies)

即時副本的基本形式有：

* 即時複製頁面，以1:1為基礎反映所選來源頁面。
* 一個配置定義。
* 為每個資源定義的即時關係：
   * 將即時副本資源與其藍圖／來源連結。
   * 在實現繼承和轉出時使用。

根據需求，更改可以是[synchronized](creating-live-copies.md#synchronizing-your-live-copy)。

![即時複製構圖概觀](../assets/live-copy-composition.png)

#### 包含非即時副本頁面的即時副本{#live-copy-with-non-live-copy-pages}

當您在中建立即時副本時，AEM可以查看並導覽即時副本分支，並在即時副本分支AEM上使用一般功能。 這表示您（或流程）可以在即時副本中建立新資源（頁面和／或段落）。 例如，特定地區或國家的產品。

* 這些資源與源／藍圖頁面沒有即時關係，並且不同步。
* MSM可以處理特殊情況。 例如，當您（或流程）在來源／藍圖和即時副本分支中建立位置和名稱相同的頁面時。 如需詳細資訊，請參閱[MSM轉出衝突](rollout-conflicts.md)。

![包含非即時副本頁面的即時副本](../assets/live-copy-with-non-live-copy-pages.png)

#### 巢狀即時副本{#nested-live-copies}

當您（或流程）在現有即時副本中建立[新頁面時，此新頁面也可設為不同藍圖的即時副本。 ](#live-copy-with-non-live-copy-pages)這稱為巢狀即時副本。 在巢狀即時副本中，第二個或內部即時副本的行為會受到第一個或外部即時副本的影響，方式如下：

* 對頂層即時副本觸發的深度轉出，可以繼續進入巢狀即時副本。
* 源之間的任何連結都將在「即時副本」中重寫。

例如，從第二個到第一個藍圖的連結將重寫為從巢狀／第二個即時副本到第一個即時副本的連結。

![巢狀即時副本](../assets/live-copy-nested.png)

>[!NOTE]
>
>如果您在即時副本分支中移動或重新命名頁面，這將被視為巢狀即時副本，以便AEM追蹤關係。

#### 堆疊的即時拷貝{#stacked-live-copies}

即時副本作為淺層即時副本的子項建立時，即稱為堆疊即時副本。 它的運作方式與[巢狀即時副本](#nested-live-copies)相同。

### 源、藍圖和藍圖配置{#source-blueprints-and-blueprint-configurations}

任何頁面或頁面分支皆可用作即時副本的來源。 不過，MSM也允許您定義指定源路徑的藍圖配置。 使用Blueprint設定的優點是：

* 允許作者在藍圖上使用&#x200B;**Rovolt**&#x200B;選項。 亦即，明確將修改推送至繼承自此藍圖的即時副本。
* 允許作者使用&#x200B;**Create Site**。 這可讓使用者輕鬆選擇語言並設定即時副本的結構。
* 定義與藍圖有關的即時副本的預設轉出設定。

即時副本的來源可以是常規頁面或藍圖配置涵蓋的頁面。 這兩種都是有效的使用案例。

來源會形成即時副本的藍圖。 Blueprint是在下列情況下定義的：

* [建立Blueprint設定](creating-live-copies.md#creating-a-blueprint-configuration) -此設定會預先定義要用來建立即時副本的頁面。
* [建立頁面的即時副本](creating-live-copies.md#creating-a-live-copy-of-a-page) -用於建立即時副本（來源頁面）的頁面是Blueprint頁面。Blueprint設定可能會參考或不參考來源頁面。

### 轉出並同步{#rollout-and-synchronize}

推出是集中的MSM動作，可同步即時副本與其來源。 您可以手動執行展開，也可以自動執行。

* 可以定義[轉出配置](#rollout-configurations)，使得特定[事件](live-copy-sync-config.md#rollout-triggers)可自動轉出。
* 在製作藍圖頁面時，您可以使用&#x200B;**[Rovolt](creating-live-copies.md#rolling-out-a-blueprint)**&#x200B;命令將變更推送至即時副本。
   * **Rovolt**&#x200B;命令可用於藍圖配置所引用的藍圖頁面。

   ![轉出](../assets/live-copy-rollout.png)

* 在編寫「即時副本」頁面時，您可以使用&#x200B;**[Synchronize](creating-live-copies.md#synchronizing-a-live-copy)**&#x200B;命令將更改從源位置提取到「即時副本」。
   * 無論Blueprint配置是否包含源/Blueprint頁，「即時副本」頁面上始終可以使用&#x200B;**Synchronize**&#x200B;命令。

   ![同步](../assets/live-copy-synchronize.png)

### 轉出設定 {#rollout-configurations}

轉出配置定義即時副本與來源內容同步的時間和方式。 轉出配置由觸發器和一個或多個同步操作組成：

* **觸發器** -觸發器是導致即時動作同步發生的事件，例如啟動來源頁面。MSM定義您可使用的觸發器。
* **同步操作** -對即時副本執行同步操作，以便與源同步。例如，複製內容、排序子節點，以及啟動「即時副本」頁面等動作。 MSM提供了一些同步操作。

>[!NOTE]
>
>您可以使用Java API為例項建立自訂動作。

可重複使用轉出設定，因此多個即時副本可以使用相同的轉出設定。 標準安裝中包含幾個[轉出配置](live-copy-sync-config.md#installed-rollout-configurations)。

### 轉出衝突{#rollout-conflicts}

推播可能會變得複雜，尤其是當作者同時在來源和即時副本中編輯內容時。 因此，請務必注意如何處AEM理在轉出期間可能發生的任何[衝突。](rollout-conflicts.md)

### 掛起和取消繼承和同步{#suspending-and-cancelling-inheritance-and-synchronization}

即時副本中的每個頁面和元件都會透過即時關係與其來源頁面和元件相關聯。 即時關係會設定來源的即時副本內容同步。

您可以&#x200B;**暫停**&#x200B;即時副本頁面的即時副本繼承，以便您能夠變更頁面屬性和元件。 暫停繼承時，頁面屬性和元件不再與源同步。

編輯單個頁面時，作者可以&#x200B;**取消元件的繼承**。 取消繼承後，即時關係將暫停，該元件不會進行同步。 當需要自訂內容的子區段時，取消繼承和同步很有用。

### 分離即時副本{#detaching-a-live-copy}

您也可以[將即時副本](creating-live-copies.md#detaching-a-live-copy)從其藍圖中分離，以刪除所有連接。

>[!CAUTION]
>
>「分離」(Detach)操作是永久的和不可逆的。

分離動作會永久移除即時副本與其藍圖頁面之間的即時關係。 所有與MSM相關的屬性都會從即時副本中移除，而即時副本頁面會變成獨立副本。

>[!TIP]
>
>如需完整詳細資訊，包括子頁面和父頁面的相關影響，請參閱[分離即時副本](creating-live-copies.md#detaching-a-live-copy)。

## 使用MSM {#standard-steps-for-using-msm}的標準步驟

以下步驟說明使用MSM重複使用內容並同步即時副本變更的標準程式。

1. 開發來源網站的內容。
1. 確定要使用的轉出配置。

   1. MSM [安裝了幾個可滿足多種使用情況的轉出配置](live-copy-sync-config.md#installed-rollout-configurations)。
   1. 您也可以視需要建立轉出設定[。](live-copy-sync-config.md#creating-a-rollout-configuration)

1. 確定您需要在哪裡指定[的轉出配置以使用](live-copy-sync-config.md#specifying-the-rollout-configurations-to-use)並視需要進行配置。
1. 如果需要，[會建立藍圖設定](creating-live-copies.md#creating-a-blueprint-configuration)，以識別即時副本的來源內容。
1. [建立即時副本。](creating-live-copies.md#creating-a-live-copy)
1. 視需要變更來源內容。 您應採用貴組織已建立的一般內容審閱與核准程式。
1. [將滑](creating-live-copies.md#rolling-out-a-blueprint) 鼠指向藍圖，或 [將即時組](creating-live-copies.md#synchronizing-a-live-copy) 排文字與變更同步。

## 自定義MSM {#customizing-msm}

MSM提供多種工具，讓您的實作能夠因應分享內容時可能存在的特殊複雜性。

* **自訂轉出設定** -當 [安裝的轉出](live-copy-sync-config.md#creating-a-rollout-configuration) 設定不符合您的需求時，建立轉出設定。您可以使用任何可用的轉出觸發器和同步操作。

<!--
* **Custom Synchronization Actions** - [Create a custom synchronization action](/help/sites-developing/extending-msm.md#creating-a-new-synchronization-action) when the installed actions do not meet your specific application requirements. MSM provides a Java API for creating custom synchronization actions.
-->

## 最佳作法 {#best-practices}

[MSM最佳實務](best-practices.md)頁面包含您實作的重要資訊。
