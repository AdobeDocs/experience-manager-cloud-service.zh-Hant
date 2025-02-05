---
title: 推出衝突
description: 瞭解如何管理和解決多網站管理員轉出衝突。
feature: Multi Site Manager
role: Admin
exl-id: 733e9411-50a7-42a5-a5a8-4629f6153f10
solution: Experience Manager Sites
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 2%

---

# 推出衝突 {#msm-rollout-conflicts}

如果在Blueprint分支和相依即時副本分支中同時建立具有相同頁面名稱的新頁面，則可能會發生衝突。 轉出時必須處理和解決此類衝突。

## 衝突處理 {#conflict-handling}

當Blueprint和即時副本分支中存在衝突的頁面時，MSM可讓您定義應如何（甚至是否）處理衝突。

為確保轉出不被封鎖，可能的定義可以包括：

* 轉出時哪個頁面（Blueprint或即時副本）優先
* 哪些頁面會重新命名，以及如何重新命名
* 這會如何影響任何已發佈的內容

Adobe Experience Manager (AEM)的預設現成行為是發佈內容不受影響。 因此，如果在即時副本分支中手動建立的頁面已發佈，在衝突處理和轉出後，該內容仍會發佈。

除了標準功能外，您也可以新增自訂的衝突處理常式，以實作不同的規則。 這些功能也可以允許將動作發佈為個別程式。

### 範例情境 {#example-scenario}

在以下區段中，使用在Blueprint和Live Copy分支（手動建立）中建立的新頁面`b`的範例，以說明解決衝突的各種方法：

* Blueprint： `/b`

  具有一個子頁面的主版頁面，`bp-level-1`

* 即時副本： `/b`

  在即時副本分支中手動建立的頁面，具有一個子頁面`lc-level-1`

   * 與子頁面一起在發佈時以`/b`啟動

#### 轉出前 {#before-rollout}

|  | 轉出前的Blueprint | 轉出前的即時副本 | 轉出前的Publish |
|---|---|---|---|
| 值 | `b` | `b` | `b` |
| 評論 | 在Blueprint分支中建立，可供轉出 | 在即時副本分支中手動建立 | 包含在Live Copy分支中手動建立的頁面`b`的內容 |
| 值 | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| 評論 |  | 在即時副本分支中手動建立 | 包含在Live Copy分支中手動建立的頁面`child-level-1`的內容 |

## 轉出管理程式與衝突處理 {#rollout-manager-and-conflict-handling}

轉出管理員可讓您啟用或停用衝突管理。

這是使用&#x200B;**Day CQ WCM轉出管理員**&#x200B;的[OSGi組態](/help/implementing/deploying/configuring-osgi.md)完成的。 如果轉出管理員應處理在Live Copy中建立的頁面與Blueprint中已存在的名稱發生的衝突，則將值&#x200B;**處理與手動建立的頁面**&#x200B;的衝突(`rolloutmgr.conflicthandling.enabled`)設定為true。

已停用衝突管理時，AEM有[預先定義的行為](#behavior-when-conflict-handling-deactivated)。

## 衝突處理常式 {#conflict-handlers}

AEM使用衝突處理常式，來解決將內容從Blueprint轉出至即時副本時存在的任何頁面衝突。 重新命名頁面是解決這類衝突的常用（而非唯一）方法。 可以執行多個衝突處理常式，以允許選取不同的行為。

AEM提供：

* [預設衝突處理常式](#default-conflict-handler)：
   * `ResourceNameRolloutConflictHandler`
* 實施[自訂處理常式](#customized-handlers)的可能性
* 可讓您設定每個個別處理常式優先順序的服務排名機制
   * 使用排名最高的服務。

### 預設衝突處理常式 {#default-conflict-handler}

預設衝突處理常式為`ResourceNameRolloutConflictHandler`

* 使用此處理常式，Blueprint頁面會獲得優先權。
* 此處理常式的服務排名設定為低。 也就是說，低於`service.ranking`屬性的預設值，因為假設自訂處理常式需要較高的排名。 不過，排名並非在需要時確保彈性的絕對最低值。

此衝突處理常式會賦予Blueprint優先權。 例如，即時副本頁面`/b`在即時副本分支中移至`/b_msm_moved`。

* 即時副本： `/b`

  在即時副本中移至`/b_msm_moved`。 這會作為備份，並確保不會遺失任何內容。

   * 未移動`lc-level-1`。

* 藍圖： `/b`

  轉出至即時副本頁面`/b`。

   * `bp-level-1`已轉出至即時副本。

#### 轉出後 {#after-rollout}

|  | 轉出後的Blueprint | 轉出後的即時副本 | 轉出後的即時副本 | 轉出後的Publish |
|---|---|---|---|---|
| 值 | `b` | `b` | `b_msm_moved` | `b` |
| 評論 |  | 具有已轉出的Blueprint頁面`b`的內容 | 具有在即時副本分支中手動建立的頁面`b`的內容 | 無變更；包含在Live Copy分支中手動建立的原始頁面`b`的內容，現在稱為`b_msm_moved` |
| 值 | `/bp-level-1` | `/bp-level-1` | `/lc-level-1` | `/lc-level-1` |
| 評論 |  |  | 無變更 | 無變更 |

### 自訂處理常式 {#customized-handlers}

自訂衝突處理常式可讓您實作自己的規則。 使用服務排名機制，您也可以定義它們如何與其他處理常式互動。

自訂的衝突處理常式可以：

* 根據您的需求命名。
* 根據您的需求進行開發/設定。
   * 例如，您可以開發處理常式，讓即時副本頁面獲得優先權。
* 可以使用[OSGi設定](/help/implementing/deploying/configuring-osgi.md)來設定。 尤其是：
   * **服務排名**&#x200B;定義與其他衝突處理常式( `service.ranking`)相關的順序。
      * 預設值為 `0`。

### 停用衝突處理時的行為 {#behavior-when-conflict-handling-deactivated}

如果您手動[停用衝突處理](#rollout-manager-and-conflict-handling)，AEM不會對任何衝突頁面執行任何動作。 非衝突頁面會如預期轉出。

>[!CAUTION]
>
>當衝突處理停用時，AEM不會指出將忽略衝突。 由於在這種情況下必須明確設定此行為，因此假設這是所需的行為。

在此情況下，即時副本會有效取得優先權。 不會複製Blueprint頁面`/b`，而即時副本頁面`/b`保持不變。

* 藍圖： `/b`

  它根本不會複製，而是被忽略。

* 即時副本： `/b`

  維持不變。

#### 轉出後 {#after-rollout-no-conflict}

|  | 轉出後的Blueprint | 轉出後的即時副本 | 轉出後的Publish |
|---|---|---|---|
| 值 | `b` | `b` | `b` |
| 評論 |  | 無變更；具有在即時副本分支中手動建立的頁面`b`的內容 | 無變更；包含在Live Copy分支中手動建立的頁面`b`的內容 |
| 值 | `/bp-level-1,` | `/lc-level-1` | `/lc-level-1` |
| 評論 |  | 無變更 | 無變更 |

### 服務排名 {#service-rankings}

[OSGi](https://www.osgi.org/)服務排名可用來定義個別衝突處理常式的優先順序。
