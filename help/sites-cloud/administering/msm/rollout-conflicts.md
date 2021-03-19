---
title: 推出衝突
description: 瞭解如何管理和解決Multi Site Manager的推出衝突。
feature: 多站點管理員
role: 管理員
translation-type: tm+mt
source-git-commit: 0f2b7176b44bb79bdcd1cecf6debf05bd652a1a1
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 3%

---


# 轉出衝突{#msm-rollout-conflicts}

如果在Blueprint分支和相依即時副本分支中建立具有相同頁面名稱的新頁面，則可能會發生衝突。 這些衝突需要在推出時處理並解決。

## 衝突處理{#conflict-handling}

當衝突頁面確實存在（在Blueprint和即時副本分支中）時，MSM可讓您定義應如何（甚至是如何）處理這些頁面。

為確保轉出未遭封鎖，可能的定義可包括：

* 在推出期間，哪個頁面（Blueprint或即時副本）將具有優先順序
* 將重新命名哪些頁面（以及如何重新命名）
* 這會如何影響任何發佈的內容

預設的現AEM成可用行為是發佈的內容不會受到影響。 因此，如果在即時副本分支中手動建立的頁面已發佈，該內容仍會在衝突處理和轉出後發佈。

除了標準功能外，還可新增自訂的衝突處理常式，以實作不同的規則。 這些動作也可以允許以個別程式進行發佈動作。

### 藍本{#example-scenario}示例

在以下幾節中，我們使用在Blueprint和Live Copy分支（手動建立）中建立的新頁面`b`的示例來說明各種衝突解決方法：

* 藍圖：`/b`

   包含1個子頁面的主版頁面`bp-level-1`

* 即時副本: `/b`

   在「即時副本」分支中手動建立的頁面，其中包含1個子頁面`lc-level-1`

   * 在發佈時以`/b`和子頁面一起啟動

#### 推出前{#before-rollout}

|  | 推出前的藍圖 | 在推出前即時複製 | 轉出前發佈 |
|---|---|---|---|
| 值 | `b` | `b` | `b` |
| 評論 | 在Blueprint分支中建立，準備推出 | 在即時副本分支中手動建立 | 包含在即時副本分支中手動建立之頁面`b`的內容 |
| 值 | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| 評論 |  | 在即時副本分支中手動建立 | 包含在即時副本分支中手動建立之頁面`child-level-1`的內容 |

## 轉出管理器和衝突處理{#rollout-manager-and-conflict-handling}

轉出管理員可讓您啟用或停用衝突管理。

這是使用&#x200B;**Day CQ WCM Pollout Manager**&#x200B;的[OSGi配置](/help/implementing/deploying/configuring-osgi.md)來完成的。 如果轉出管理員應處理在「即時副本」中建立且名稱位於Blueprint中的頁面衝突，請將「處理與手動建立的頁面衝突」(**)設為true。**`rolloutmgr.conflicthandling.enabled`

已AEM在衝突管理停用時具有[預先定義的行為。](#behavior-when-conflict-handling-deactivated)

## 衝突處理程式{#conflict-handlers}

使AEM用衝突處理常式來解決從Blueprint將內容發佈至即時副本時存在的任何頁面衝突。 重新命名頁面是解決此類衝突的常用方法（不僅如此）。 可以操作多個衝突處理程式以允許選擇不同的行為。

AEM提供：

* [預設衝突處理程式](#default-conflict-handler):
   * `ResourceNameRolloutConflictHandler`
* 實作[自訂處理常式](#customized-handlers)的可能性
* 允許您設定每個單獨處理程式的優先順序的服務排名機制
   * 使用排名最高的服務。

### 預設衝突處理程式{#default-conflict-handler}

預設衝突處理程式為`ResourceNameRolloutConflictHandler`

* 使用此處理常式時，Blueprint頁面會優先。
* 此處理常式的服務排名設為低，即低於`service.ranking`屬性的預設值，因為自訂處理常式需要較高的排名。 不過，排名並非確保必要時靈活性的絕對最小值。

此衝突處理常式優先於Blueprint。 在前例中，「即時副本」頁面`/b`會在「即時副本」分支中移至`/b_msm_moved`。

* 即時副本: `/b`

   在「即時副本」中移至`/b_msm_moved`。 這可當成備份，並確保不會遺失任何內容。

   * `lc-level-1` 未移動。

* 藍圖：`/b`

   已推出至「即時副本」頁面`/b`。

   * `bp-level-1` 即時副本。

#### 轉出後{#after-rollout}

|  | 推出後的藍圖 | 推出後即時復本 | 推出後即時復本 | 轉出後發佈 |
|---|---|---|---|---|
| 值 | `b` | `b` | `b_msm_moved` | `b` |
| 評論 |  | 已推出的Blueprint頁面`b`內容 | 具有在即時副本分支中手動建立的頁面`b`的內容 | 無變更，包含在即時副本分支中手動建立的原始頁面`b`的內容，現在稱為`b_msm_moved` |
| 值 | `/bp-level-1` | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| 評論 |  |  | 無變更 | 無變更 |

### 自定義處理程式{#customized-handlers}

自訂的衝突處理常式可讓您實作自己的規則。 使用服務排名機制，您也可以定義它們與其他處理常式的互動方式。

自訂的衝突處理常式可以：

* 請根據您的需求命名。
* 根據您的需求進行開發／設定。
   * 例如，您可以開發處理常式，讓即時副本頁面優先。
* 可設計為使用[OSGi配置](/help/implementing/deploying/configuring-osgi.md)進行配置。 尤其是：
   * **服務** 規則定義與其他衝突處理程式( `service.ranking`)相關的順序。
      * 預設值為 `0`.

### 衝突處理停用{#behavior-when-conflict-handling-deactivated}時的行為

如果您手動[停用衝突處理，](#rollout-manager-and-conflict-handling)對任何衝突頁AEM面不會採取任何動作。 非衝突頁面會如預期般推出。

>[!CAUTION]
>
>當衝突處理停用時，AEM不會顯示衝突正在被忽略。 由於在這種情況下，必須明確設定此行為，因此假定這是所要的行為。

在這種情況下，即時副本有效優先。 Blueprint頁面`/b`不會複製，而「即時副本」頁面`/b`則不受影響。

* 藍圖：`/b`

   完全不複製，但會被忽略。

* 即時副本: `/b`

   保持不變。

#### 轉出後{#after-rollout-no-conflict}

|  | 推出後的藍圖 | 推出後即時復本 | 轉出後發佈 |
|---|---|---|---|
| 值 | `b` | `b` | `b` |
| 評論 |  | 無變更，具有在即時副本分支中手動建立的頁面`b`的內容 | 無變更，包含在即時副本分支中手動建立之頁面`b`的內容 |
| 值 | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| 評論 |  | 無變更 | 無變更 |

### 服務排名{#service-rankings}

[OSGi](https://www.osgi.org/)服務排名可用於定義單個衝突處理程式的優先順序。
