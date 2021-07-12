---
title: 轉出衝突
description: 了解如何管理和解決多網站管理員轉出衝突。
feature: 多站點管理員
role: Admin
exl-id: 733e9411-50a7-42a5-a5a8-4629f6153f10
source-git-commit: 24a4a43cef9a579f9f2992a41c582f4a6c775bf3
workflow-type: tm+mt
source-wordcount: '926'
ht-degree: 2%

---

# 轉出衝突 {#msm-rollout-conflicts}

如果在Blueprint分支和相依的Live Copy分支中建立了具有相同頁面名稱的新頁面，則可能會發生衝突。 這類衝突需要在推出時處理和解決。

## 衝突處理 {#conflict-handling}

當發生衝突的頁面確實存在時（在Blueprint和Live Copy分支中）,MSM可讓您定義應如何（甚至是如何）處理這些頁面。

為確保轉出未遭到封鎖，可能的定義可能包括：

* 轉出期間哪個頁面（Blueprint或Live Copy）會具有優先順序
* 將重新命名哪些頁面（以及如何）
* 這會如何影響任何已發佈的內容

AEM的預設現成行為是已發佈內容將不會受到影響。 因此，如果在Live Copy分支中手動建立的頁面已發佈，該內容在處理和轉出衝突後仍會發佈。

除了標準功能外，還可以添加自定義衝突處理程式以實施不同的規則。 這些也可允許以個別程式發佈動作。

### 範例案例 {#example-scenario}

在以下幾節中，我們使用在Blueprint和Live Copy分支（手動建立）中建立的新頁面`b`的示例來說明各種衝突解決方法：

* blueprint:`/b`

   包含1個子頁的母版頁`bp-level-1`

* 即時副本: `/b`

   在Live Copy分支中手動建立的頁面，其中包含1個子頁面`lc-level-1`

   * 發佈時啟動為`/b`，連同子頁面

#### 轉出前 {#before-rollout}

|  | 轉出前的Blueprint | 轉出前即時副本 | 轉出前發佈 |
|---|---|---|---|
| 值 | `b` | `b` | `b` |
| 評論 | 在Blueprint分支中建立，可轉出 | 在Live Copy分支中手動建立 | 包含在Live Copy分支中手動建立之頁面`b`的內容 |
| 值 | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| 評論 |  | 在Live Copy分支中手動建立 | 包含在Live Copy分支中手動建立之頁面`child-level-1`的內容 |

## 轉出管理員和衝突處理 {#rollout-manager-and-conflict-handling}

轉出管理器可讓您啟用或停用衝突管理。

這是使用&#x200B;**Day CQ WCM轉出管理器**&#x200B;的[OSGi設定](/help/implementing/deploying/configuring-osgi.md)來完成。 如果轉出管理器應處理來自Live Copy中建立且Blueprint中存在名稱的頁面的衝突，請將值&#x200B;**處理與手動建立的頁面**(`rolloutmgr.conflicthandling.enabled`)設為true。

AEM具有[在停用衝突管理時預先定義的行為。](#behavior-when-conflict-handling-deactivated)

## 衝突處理程式 {#conflict-handlers}

AEM使用衝突處理常式來解決從Blueprint將內容轉出至Live Copy時存在的任何頁面衝突。 更名頁面是解決此類衝突的常用（不僅是）方法。 可以操作多個衝突處理程式以允許選擇不同的行為。

AEM提供：

* [預設衝突處理程式](#default-conflict-handler):
   * `ResourceNameRolloutConflictHandler`
* 實施[自定義處理程式的可能性](#customized-handlers)
* 可讓您設定每個個別處理常式之優先順序的服務排名機制
   * 會使用排名最高的服務。

### 預設衝突處理程式 {#default-conflict-handler}

預設衝突處理程式為`ResourceNameRolloutConflictHandler`

* 使用此處理常式時，Blueprint頁面會優先。
* 此處理程式的服務排名設定得較低，即`service.ranking`屬性的預設值之下，因為假定自定義處理程式需要較高的排名。 然而，排名並非確保必要時靈活性的絕對最小值。

此衝突處理程式優先於Blueprint。 前述範例中，即時副本頁面`/b`會在即時副本分支內移至`/b_msm_moved`。

* 即時副本: `/b`

   在Live Copy中移至`/b_msm_moved`。 這可作為備份，並確保不會遺失任何內容。

   * `lc-level-1` 未移動。

* Blueprint:`/b`

   已轉出至「即時副本」頁面`/b`。

   * `bp-level-1` 會轉出至Live Copy。

#### 轉出後 {#after-rollout}

|  | 轉出後的Blueprint | 轉出後即時副本 | 轉出後即時副本 | 轉出後發佈 |
|---|---|---|---|---|
| 值 | `b` | `b` | `b_msm_moved` | `b` |
| 評論 |  | 已推出Blueprint頁面`b`的內容 | 具有在Live Copy分支中手動建立之頁面`b`的內容 | 無變更，包含在Live Copy分支中手動建立的原始頁面`b`的內容，現在稱為`b_msm_moved` |
| 值 | `/bp-level-1` | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| 評論 |  |  | 無更改 | 無更改 |

### 自訂處理常式 {#customized-handlers}

自定義的衝突處理程式允許您實施自己的規則。 使用服務排名機制，您也可以定義它們與其他處理常式的互動方式。

自定義衝突處理程式可以：

* 根據你的要求命名。
* 根據您的需求進行開發/配置。
   * 例如，您可以開發處理常式，以便指定「即時副本」頁面優先。
* 可設計為使用[OSGi配置](/help/implementing/deploying/configuring-osgi.md)進行配置。 尤其是：
   * **服務** 排名定義了與其他衝突處理程式( `service.ranking`)相關的順序。
      * 預設值為 `0`.

### 停用衝突處理時的行為 {#behavior-when-conflict-handling-deactivated}

如果您手動[停用衝突處理，](#rollout-manager-and-conflict-handling) AEM不會在任何衝突頁面上採取任何動作。 非衝突頁面會如預期般推出。

>[!CAUTION]
>
>停用衝突處理時，AEM不會指出衝突正在忽略。 因為在這種情況下，必須明確設定此行為，因此假定這是所需的行為。

在這種情況下，有效的即時副本優先。 Blueprint頁面`/b`不會複製，而「即時副本」頁面`/b`則不會受到影響。

* Blueprint:`/b`

   完全不會複製，但會忽略。

* 即時副本: `/b`

   保持不變。

#### 轉出後 {#after-rollout-no-conflict}

|  | 轉出後的Blueprint | 轉出後即時副本 | 轉出後發佈 |
|---|---|---|---|
| 值 | `b` | `b` | `b` |
| 評論 |  | 無變更，且頁面`b`的內容已在即時副本分支中手動建立 | 無變更，包含在Live Copy分支中手動建立之頁面`b`的內容 |
| 值 | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| 評論 |  | 無更改 | 無更改 |

### 服務排名 {#service-rankings}

[OSGi](https://www.osgi.org/)服務排名可用於定義單個衝突處理程式的優先順序。
