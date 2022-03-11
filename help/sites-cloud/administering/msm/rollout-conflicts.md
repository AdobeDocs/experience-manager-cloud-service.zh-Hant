---
title: 部署衝突
description: 瞭解如何管理和解決多站點管理器部署衝突。
feature: Multi Site Manager
role: Admin
exl-id: 733e9411-50a7-42a5-a5a8-4629f6153f10
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 2%

---

# 部署衝突 {#msm-rollout-conflicts}

如果在藍圖分支和從屬即時複製分支中都建立了具有相同頁面名稱的新頁面，則可能會發生衝突。 這些衝突需要在部署時得到處理和解決。

## 衝突處理 {#conflict-handling}

當衝突頁面確實存在（在藍圖和Live Copy分支中）時，MSM允許您定義應如何（甚至是如果）處理它們。

為確保部署不被阻止，可能的定義可以包括：

* 在部署期間，哪個頁面（藍圖或即時拷貝）具有優先順序
* 將更名哪些頁（以及如何）
* 這將如何影響任何已發佈內容

出廠設定AEM的預設行為是發佈的內容不會受到影響。 因此，如果在Live Copy分支中手動建立的頁面已發佈，則在衝突處理和部署後仍將發佈該內容。

除了標準功能外，還可以添加自定義衝突處理程式以實現不同的規則。 這也允許作為單個進程發佈操作。

### 示例方案 {#example-scenario}

在以下各節中，我們使用新頁面的示例 `b`，在藍圖和Live Copy分支中建立（手動建立），以說明各種衝突解決方法：

* 藍圖： `/b`

   一個母版頁， `bp-level-1`

* 即時副本: `/b`

   在Live Copy分支中手動建立的頁，其中包含1個子頁， `lc-level-1`

   * 在發佈時激活為 `/b`，連同子頁

#### 推廣前 {#before-rollout}

|  | 部署前藍圖 | 部署前即時拷貝 | 部署前發佈 |
|---|---|---|---|
| 值 | `b` | `b` | `b` |
| 評論 | 在藍圖分支中建立，準備部署 | 在Live Copy分支中手動建立 | 包含頁面內容 `b` 在Live Copy分支中手動建立的 |
| 值 | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| 評論 |  | 在Live Copy分支中手動建立 | 包含頁面的內容 `child-level-1` 在Live Copy分支中手動建立的 |

## 部署管理器和衝突處理 {#rollout-manager-and-conflict-handling}

部署管理器允許您激活或停用衝突管理。

這是使用 [OSGi配置](/help/implementing/deploying/configuring-osgi.md) 共 **第CQ WCM推出管理器**。 設定值 **處理與手動建立的頁面的衝突** ( `rolloutmgr.conflicthandling.enabled`)為true，如果部署管理器應處理在即時複製中建立的頁面中的衝突，並且該頁面的名稱在藍圖中存在。

AEM [已停用衝突管理時的預定義行為。](#behavior-when-conflict-handling-deactivated)

## 衝突處理程式 {#conflict-handlers}

使AEM用衝突處理程式解決將內容從藍圖移出到即時拷貝時存在的任何頁面衝突。 更名頁面是解決此類衝突的常用（不僅如此）方法。 可以操作多個衝突處理程式，以允許選擇不同的行為。

AEM提供：

* 的 [預設衝突處理程式](#default-conflict-handler):
   * `ResourceNameRolloutConflictHandler`
* 執行 [自定義處理程式](#customized-handlers)
* 允許您設定每個處理程式的優先順序的服務分級機制
   * 使用排名最高的服務。

### 預設衝突處理程式 {#default-conflict-handler}

預設衝突處理程式為 `ResourceNameRolloutConflictHandler`

* 使用此處理程式，將優先顯示藍圖頁。
* 此處理程式的服務等級設定為低，即低於 `service.ranking` 屬性，因為假定自定義處理程式需要更高的等級。 但是，排名並非確保必要時靈活性的絕對最小值。

此衝突處理程式優先於藍圖。 前例，「即時複製」頁 `/b` 在Live Copy分支中移動到 `/b_msm_moved`。

* 即時副本: `/b`

   在Live Copy中移動到 `/b_msm_moved`。 這將充當備份，並確保不會丟失任何內容。

   * `lc-level-1` 的子菜單。

* 藍圖： `/b`

   已展開到「即時複製」頁 `/b`。

   * `bp-level-1` 將滾動到即時副本。

#### 推出後 {#after-rollout}

|  | 推出後的藍圖 | 推廣後即時拷貝 | 推廣後即時拷貝 | 部署後發佈 |
|---|---|---|---|---|
| 值 | `b` | `b` | `b_msm_moved` | `b` |
| 評論 |  | 藍圖頁的內容 `b` 被推開 | 具有頁面內容 `b` 在Live Copy分支中手動建立的 | 無更改，包含原始頁面的內容 `b` 已在Live Copy分支中手動建立，現在稱為 `b_msm_moved` |
| 值 | `/bp-level-1` | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| 評論 |  |  | 無更改 | 無更改 |

### 自定義處理程式 {#customized-handlers}

自定義衝突處理程式允許您實施自己的規則。 使用服務排名機制，您還可以定義它們如何與其他處理程式交互。

自定義衝突處理程式可以：

* 根據你的要求命名。
* 根據您的要求開發/配置。
   * 例如，可以開發處理程式，以便優先顯示「即時複製」頁。
* 可設計為使用 [OSGi配置](/help/implementing/deploying/configuring-osgi.md)。 特別是：
   * **服務排名** 定義與其他衝突處理程式相關的順序( `service.ranking`)。
      * 預設值為 `0`.

### 取消激活衝突處理時的行為 {#behavior-when-conflict-handling-deactivated}

如果手動 [停用衝突處理，](#rollout-manager-and-conflict-handling) 對任AEM何衝突頁面不執行任何操作。 非衝突頁面將按預期展開。

>[!CAUTION]
>
>停用衝突處理時，AEM不會顯示衝突正在被忽略。 因為在這種情況下，必須顯式配置此行為，所以假定它是所需的行為。

在這種情況下， Live Copy會有效優先。 藍圖頁 `/b` 未複製且「即時複製」頁 `/b` 保持原狀。

* 藍圖： `/b`

   完全未複製，但被忽略。

* 即時副本: `/b`

   保持原樣。

#### 推出後 {#after-rollout-no-conflict}

|  | 推出後的藍圖 | 推廣後即時拷貝 | 部署後發佈 |
|---|---|---|---|
| 值 | `b` | `b` | `b` |
| 評論 |  | 無更改，具有頁面內容 `b` 在Live Copy分支中手動建立的 | 無更改，包含頁面內容 `b` 在Live Copy分支中手動建立的 |
| 值 | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| 評論 |  | 無更改 | 無更改 |

### 服務排名 {#service-rankings}

的 [OSGi](https://www.osgi.org/) 服務排名可用於定義單個衝突處理程式的優先順序。
