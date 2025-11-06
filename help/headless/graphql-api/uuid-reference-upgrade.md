---
title: 升級您的內容片段以供UUID參考使用
description: 瞭解如何升級您的內容片段，以在Adobe Experience Manager as a Cloud Service中最佳化UUID參考，進而進行Headless內容傳送。
feature: Headless, Content Fragments,GraphQL API
role: Admin, Developer
exl-id: 004d1340-8e3a-4e9a-82dc-fa013cea45a7
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 2%

---

# 升級您的內容片段以供UUID參考使用 {#upgrade-content-fragments-for-UUID-references}

為了最佳化GraphQL篩選器的穩定性，您可以升級內容片段中的內容和片段參考，以便使用通用唯一識別碼(UUID)。

原本的內容片段模型提供&#x200B;**內容參考**&#x200B;和&#x200B;**片段參考**&#x200B;的資料型別。 這兩個參照都使用路徑指向參照的資源，如果移動資源，此路徑可能會過期。 雖然在大多數情況下這類參考已足夠，但內容片段模型已擴充為也根據UUID提供參考：

* **內容參考 (UUID)**
* **片段參考(UUID)**。

這些新參考型別可用於新內容片段模型和片段，以及擴充現有例項。

若要升級現有的內容片段和模型，您可以執行此處記錄的程式。

>[!CAUTION]
>
>在執行升級程式之前，您應該一律[執行試用](#execute-a-dry-run)，以強調內容的任何潛在問題。

## 升級內容 {#what-is-upgraded}

已進行下列更新：

* 資料型別的欄位：
   * **內容參考**&#x200B;已轉換為&#x200B;**內容參考(UUID)**
   * **片段參考**&#x200B;已轉換為&#x200B;**片段參考(UUID)**
* 保留在這些欄位中的路徑型參考值會由對應的UUID取代

>[!NOTE]
>
>升級後，兩種資料型別在內容片段模式編輯器中仍然可用。 您可以根據這兩種型別建立新欄位（雖然預計您將會使用以UUID為基礎的型別），並視需要重新執行升級。

## 未升級的專案 {#what-is-not-upgraded}

下列參照並未升級：

* 頁面參考 — 尚不支援UUID
* 任何無效的參考；例如，不存在內容片段路徑或資產路徑的目標

   * 無效的參考不會升級，就像內容片段路徑或資產路徑無效，沒有對應的UUID可指派。 原始參照保持不變。

   * 使用[試用](#execute-a-dry-run)來擷取任何無效的參考。

  >[!NOTE]
  >
  >由於無效，無論升級為何，都無法使用。

## 何時不應升級 {#when-you-should-not-upgrade}

不升級：

* 當您的任何內容片段使用頁面參考時；作為UUID尚未支援頁面參考

## UUID參考的限制 {#limitations-of-uuid-references}

目前，以下限制適用於根據UUID使用參照的情況：

* 模型

   * 無法透過OpenAPI建立具有內容片段UUID或內容參考UUID欄位的新內容片段模型。
   * 模型的`id`欄位尚未變更為以UUID為基礎。 它使用模型的base64解碼路徑。 無法移動模型，因此此值仍是穩定的。

* Assets

   * 透過OpenAPI建立內容片段時，必須使用`fragment-reference`或`content-reference`欄位型別來分別指定片段或資產的參考 — 即使設定以UUID為基礎的參考欄位的值也一樣。

## 升級計畫 {#upgrade-planning}

執行升級前，請先進行一些準備步驟。

### 執行練習 {#execute-a-dry-run}

建議&#x200B;*每次*&#x200B;當您升級內容時，請先執行試用。 這將建立記錄檔，其中含有反白顯示任何潛在問題的專案：

* 無效的參考
* 頁面引用

以`dryRun`模式執行內容升級，以：

* 識別任何無效參照；透過將其列在記錄檔案中
接著，您可以修正這些參考，再執行實際內容升級。
* 識別任何頁面參照；將其列在記錄檔案中
偵測到頁面參考時，您[不應該執行內容升級](#when-you-should-not-upgrade)。


### 強制凍結內容 {#enforce-a-content-freeze}

應該計畫在內容凍結期間執行內容升級。

內容凍結的持續時間取決於要升級的內容片段數量。 因此，升級可能從幾分鐘到幾小時不等，也取決於開始內容升級時使用的引數。

## 執行內容升級 {#running-the-content-upgrade}

可以使用端點來管理內容升級： `/libs/dam/cfm/maintenance.json`

>[!NOTE]
>
>您的帳戶需要`Administrator`角色才能存取端點。

### 開始內容升級 {#start-a-content-upgrade}

| 端點 | HTTP要求型別 | 評論 |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `POST` | |
| **要求引數** | **值** | |
| 動作 | `start` | |
| serviceTypeId | `uuidUpgradeService` | 服務型別ID （預先定義、固定值）。 |
|  segmentSize | `1000` | 一個區段（批次）中將升級的內容片段或模型數目。 |
| 基底路徑 | `/conf` | 指定下列其中一項：<ul><li>根`/conf`升級所有AEM設定</li><li>選取的AEM設定路徑。 已為其執行內容升級<br>例如： `/conf/wknd-shared`僅升級單一租使用者`wknd-shared`</li></ul> |
| 間隔 | `10` | 以秒為單位的間隔，過了這段時間後，下一個內容片段或模型區段就會升級。 |
| 模式 | `replicate`、`noReplicate` | <ul><li>`replicate`：在所有AEM Publish執行個體上復寫相同工作</li><li>`noReplicate`：僅在AEM Author執行個體上執行工作</li></ul> |
| 練習版 |  `true`，`false` | <ul><li>`false`：模擬內容升級，不儲存任何內容變更</li><li>`true`：執行內容升級，並儲存內容變更</li></ul> |
| **回應詳細資料** | **值** | |
| jobId | `UUID` |  執行內容升級的工作的ID。<ul><li>任何與此執行相關的後續呼叫都需要此ID。</li><li>如果`mode`值設為`replicate`，則在AEM Publish執行個體上執行也需要位於相同的`jobId`下。</li></ul> |
| 引數 | 內容升級引數 | 這些包括用於啟動內容升級的初始引數，以及一些內部預設值。 |


### 範例內容升級請求 {#example-content-upgrade-request}

+++請求

```http
POST http://localhost:4502/libs/dam/cfm/maintenance.json
Content-Type: application/json
Authorization: _REPLACE_WITH_VALID_AUTH_
Accept: application/json
 
{
    "action": "start",
    "serviceTypeId": "uuidUpgradeService",
    "segmentSize": 1000,
    "basePath": "/conf/wknd-shared",
    "interval": 10,
    "mode": "replicate",
    "dryRun": true
}
```

+++

+++回應

```http
HTTP/1.1 200 OK
Date: Wed, 16 Oct 2024 14:34:37 GMT
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
Content-Type: application/json
Content-Length: 386
 
{
  "jobId": "91af43a6-63ff-45e5-ac7b-06ccf565bdfa",
  "jcr:created": 1729089277309,
  "parameters": {
    "mode": "replicate",
    "dryRun": true,
    "segmentSize": 1000,
    "serviceTypeId": "uuidUpgradeService",
    "action": "start",
    "basePath": "/conf/wknd-shared",
    "topic": "cfm/maintenance",
    "interval": 10,
    "cronSchedule": "*/10 * * * * ?"
  }
}
```

+++

### 取得內容升級的狀態 {#get-the-status-of-a-content-upgrade}

| 端點 | HTTP要求型別 | 評論 |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `GET` | |
| **要求引數** | **值** | |
| 動作 | 狀態 | |
| jobId | `<UUID>` | 從呼叫傳回以開始內容升級的`jobId`。 |
| **回應詳細資料** | **值** | |
| 狀態 | JSON值 | 包含內容升級的詳細狀態：<ul><li>每隔間隔（秒）更新。</li><li>`uuidUpgradeService`執行有兩個階段：<ol><li>階段–0以升級內容片段模型</li><li>升級內容片段的第1階段</li></ol></li><li>在每個階段中，統計資料會在每個間隔後更新。</li><li>&quot;jobStatus&quot;： &quot;COMPLETED&quot;會將升級標籤為已成功完成。</li><li>其他狀態值的含義一目瞭然。</li></ul> |

### 內容升級狀態請求範例 {#example-content-upgrade-status-request}

+++請求

```http
GET http://localhost:4502/libs/dam/cfm/maintenance.json?action=status&jobId=91af43a6-63ff-45e5-ac7b-06ccf565bdfa
Authorization: _REPLACE_WITH_VALID_AUTH_
Accept: application/json
```

+++

+++回應

```http
HTTP/1.1 200 OK
Date: Wed, 16 Oct 2024 14:35:51 GMT
X-Content-Type-Options: nosniff
X-Frame-Options: SAMEORIGIN
Content-Type: application/json
Content-Length: 1116
 
{
  "jobId": "91af43a6-63ff-45e5-ac7b-06ccf565bdfa",
  "jcr:created": 1729089277309,
  "eventProcessed": 1,
  "parameters": {
    "mode": "replicate",
    "dryRun": true,
    "segmentSize": 1000,
    "serviceTypeId": "uuidUpgradeService",
    "action": "start",
    "confPath": "/conf/wknd-shared",
    "topic": "cfm/uuid-migration",
    "interval": 10,
    "cronSchedule": "*/10 * * * * ?"
  },
  "status": {
    "jobStatus": "COMPLETED",
    "lastModified": 1729089310301,
    "currentPhaseIndex": 1,
    "phases": {
      "phase-0": {
        "bookmark": 1727183332520,
        "stats": {
          "successCount": 2,
          "skippedCount": 1,
          "errorCount": 0
        },
        "name": "modelUpgrade",
        "lastModified": 1729089290040,
        "isCompleted": true
      },
      "phase-1": {
        "bookmark": 1727183347990,
        "stats": {
          "successCount": 29,
          "skippedCount": 0,
          "errorCount": 1
        },
        "name": "cfUpgrade",
        "lastModified": 1729089310298,
        "isCompleted": true
      }
    }
  }
}
```

+++

+++記錄檔範例

除了從HTTP端點取得的執行中內容升級狀態之外，AEM記錄檔還提供內容層級進度的詳細資訊。 例如：

```xml
#Successful model upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-0: resource: /conf/wknd-shared/settings/dam/cfm/models/article , status: SUCCESS, skips: [], errors: []
 
#Successful content fragment upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-1: resource: /content/dam/wknd-shared/en/magazine/san-diego-surf-spots/san-diego-surfspots , status: SUCCESS, skips: [], errors: []
 
#Unsuccessful/Skipped model upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-0: resource: /conf/wknd-shared/settings/dam/cfm/models/adventure , status: SKIPPED, skips: [Model: '/conf/wknd-shared/settings/dam/cfm/models/adventure', no upgradeable fields found], errors: []
 
#Unsuccessful content fragment upgrade
com.adobe.cq.dam.cfm.impl.servicing.uuid.* Phase phase-1: resource: /content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van , status: FAILED, skips: [], errors: [Path '/content/dam/wknd-shared/en/magazine/western-australia/western-australia-by-camper-van', Variation: 'master' Field 'featuredImage', Value '/content/dam/wknd-shared/en/magazine/western-australia/adobestock_156407519.jpeg' is invalid; will not upgrade this field.] 
```

此外，在處理內容片段和模型的每個區段（批次）後，會記錄累積狀態，以彙總目前為止的進度。 例如：

```xml
com.adobe.cq.dam.cfm.impl.servicing.PhaseChainProcessor Phase phase-x, processed a segment, stats: {successCount=29, skippedCount=0, errorCount=1}
```

+++

### 中止內容升級 {#abort-a-content-upgrade}

>[!CAUTION]
>
>中止內容升級（這不是演習）：
>
>* 不會回覆已進行的任何變更
>* 可能會讓您的內容處於混合狀態
>
>請謹慎使用此動作。

| 端點 | HTTP要求型別 | 評論 |
|--- |--- |--- |
| `/libs/dam/cfm/maintenance.json` | `POST` | |
| **要求引數** | **值** | |
| 動作 | abort | |
| jobId | `<UUID>` | 從呼叫傳回以開始內容升級的`jobId`。 |
| **回應詳細資料** | **值** | |
| 狀態 | JSON值 | 包含內容升級的詳細狀態：<ul><li>要注意的狀態是「jobStatus」：「ABORTED」。<br>中止動作之後，將不會處理任何擱置的資料區段。</li><li>如果jobStatus在中止前為「COMPLETED」，呼叫沒有任何效果。</li></ul> |

### 中止內容升級請求的範例 {#example-abort-content-upgrade-request}

+++請求

```http
POST http://localhost:4502/libs/dam/cfm/maintenance.json
Content-Type: application/json
Authorization: Basic YWRtaW46YWRtaW4=
Accept: application/json
 
{
    "action": "abort",
    "jobId": "b1dbf6f9-5f59-4007-b631-01b63cd17807"
    "mode": "replicate",
}
```

+++

+++回應

```http
HTTP/1.1 200 OK
Date: Wed, 16 Oct 2024 14:39:03 GMT
 
{
  "jobId": "b1dbf6f9-5f59-4007-b631-01b63cd17807",
   ...
  "eventProcessed": 2,
  "parameters": {
    ...
    "abort": true,
    ...
  },
  "status": {
     "jobStatus": "ABORTED",
    ...
  }
}
```

+++
