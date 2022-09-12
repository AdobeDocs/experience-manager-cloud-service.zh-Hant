---
title: 部署程式碼
description: 了解如何在AEMas a Cloud Service中使用Cloud Manager管道部署程式碼。
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
source-git-commit: 430179bf13c1fff077c515eed0676430e9e7f341
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---


# 部署程式碼 {#deploy-your-code}

了解如何在AEMas a Cloud Service中使用Cloud Manager管道將程式碼部署至生產環境。

![生產管道圖](./assets/configure-pipeline/production-pipeline-diagram.png)

可透過生產管道將程式碼順暢地部署至預備，然後再部署至生產。 生產管道執行會分為兩個邏輯階段。

1. 部署到預備環境
   * 程式碼已建置並部署至Stage環境，以進行自動化功能測試、UI測試、體驗稽核和使用者接受測試(UAT)。
1. 部署至生產環境
   * 在預備上驗證組建並核准升級至生產環境後，相同的組建工件就會部署至生產環境。

_只有完整堆疊程式碼管道類型支援程式碼掃描、函式測試、UI測試和體驗稽核。_

## 在AEM as a Cloud Service中使用Cloud Manager部署程式碼 {#deploying-code-with-cloud-manager}

一旦您 [已設定您的生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 包括存放庫、環境和測試環境，您都可以部署程式碼。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選取適當的組織。

1. 按一下要為其部署代碼的程式。

1. 按一下 **部署** 從 **概述** 螢幕啟動部署過程。

   ![CTA](assets/deploy-code1.png)

1. 此 **管道執行** 畫面隨即顯示。 按一下 **建置** 來啟動程式。

   ![管道執行畫面](assets/deploy-code2.png)

建置程式會透過三個階段部署您的程式碼。

1. [階段部署](#stage-deployment)
1. [階段測試](#stage-testing)
1. [生產部署](#production-deployment)

>[!TIP]
>
>您可以檢視記錄或檢閱結果，以檢閱各種部署程式中的步驟，以了解測試標準。

## 階段部署階段 {#stage-deployment}

此 **階段部署** 階段。 包含這些步驟。

* **驗證**   — 此步驟可確保將管道配置為使用當前可用資源。 例如，測試已配置的分支是否存在以及環境是否可用。
* **構建和單元測試**  — 此步驟會執行容器化的建置程式。
   * 請查看該文檔 [建置環境詳細資訊](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) 以取得建置環境的詳細資訊。
* **程式碼掃描**  — 此步驟會評估應用程式程式碼的品質。
   * 請查看該文檔 [程式碼品質測試](/help/implementing/cloud-manager/code-quality-testing.md) 以取得測試程式的詳細資訊。
* **建立影像**  — 此程式負責將建置步驟產生的內容和Dispatcher套件轉換為Docker影像和Kubernetes設定。
* **部署至預備**  — 映像部署到測試環境，以準備 [測試階段。](#stage-testing)

![階段部署](assets/stage-deployment.png)

## 階段測試階段 {#stage-testing}

此 **階段測試** 階段包含這些步驟。

* **產品功能測試** - Cloud Manager管道會執行針對預備環境執行的測試。
   * 請參閱該文檔 [產品功能測試](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) 以取得更多詳細資訊。

* **自訂功能測試**  — 管道中的此步驟一律執行，且無法略過。 如果組建未產生任何測試JAR，則預設會通過測試。
   * 請參閱該文檔 [自訂功能測試](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) 以取得更多詳細資訊。

* **自訂UI測試**  — 此步驟是可選功能，可自動執行為自訂應用程式建立的UI測試。
   * UI測試是封裝在Docker映像中的基於硒的測試，以允許在語言和框架（如Java和Maven、Node和WebDriver.io，或基於Selenium構建的任何其他框架和技術）中進行廣泛選擇。
   * 請參閱該文檔 [自訂UI測試](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) 以取得更多詳細資訊。

* **體驗稽核**  — 管道中的此步驟一律執行，且無法略過。 執行生產管道時，將在自訂功能測試（將執行檢查）後納入體驗稽核步驟。
   * 已設定的頁面會提交至服務並評估。
   * 結果提供資訊，並顯示目前和先前分數之間的分數和變更。
   * 此深入分析對於判斷是否有將於目前部署引入的回歸十分有用。
   * 請參閱該文檔 [了解體驗稽核結果](/help/implementing/cloud-manager/experience-audit-testing.md) 以取得更多詳細資訊。

![階段測試](assets/stage-testing.png)

## 生產部署階段 {#deployment-production}

部署至生產拓撲的程式稍有不同，以將對AEM網站訪客的影響降至最低。

生產部署通常會依照先前說明的相同步驟進行，但會以滾動方式進行。

1. 部署AEM套件以製作。
1. 從負載平衡器分離dispatcher1。
1. 將AEM套件部署至publish1，並將Dispatcher套件部署至dispatcher1，排清Dispatcher快取。
1. 將dispatcher1放回負載平衡器。
1. 當dispatcher1重新服務後，請從負載平衡器分離dispatcher2。
1. 將AEM套件部署至publish2，並將Dispatcher套件部署至dispatcher2，排清Dispatcher快取。
1. 將dispatcher2放回負載平衡器。

此過程將繼續，直到部署已到達拓撲中的所有發佈商和調度程式。

![生產部署階段](assets/production-deployment.png)

## 逾時 {#timeouts}

如果讓您等候使用者意見回饋，下列步驟會逾時：

| 步驟 | 逾時 |
|--- |--- |
| 程式碼品質測試 | 14天 |
| 安全性測試 | 14天 |
| 效能測試 | 14天 |
| 申請批准 | 14天 |
| 排程生產部署 | 14天 |
| CSE支援 | 14天 |

## 部署過程 {#deployment-process}

所有Cloud Service部署都會依循滾動程式，確保零停機時間。 請參閱該文檔 [滾動部署的運作方式](/help/implementing/deploying/overview.md#how-rolling-deployments-work) 了解更多。

## 重新執行生產部署 {#Reexecute-Deployment}

生產部署步驟已完成時，執行支援重新執行生產部署步驟。 完成類型不重要 — 可取消部署或失敗。 也就是說，主要使用案例應為生產部署步驟因暫時原因而失敗的案例。 重新執行會使用相同的管道建立新執行。 此新執行包含三個步驟：

1. 驗證步驟 — 基本上與正常管道執行期間發生的驗證相同。
1. 建置步驟 — 在重新執行的內容中，建置步驟是複製成品，而非實際執行新的建置程式。
1. 生產部署步驟 — 這會使用與正常管道執行中的生產部署步驟相同的設定和選項。

建置步驟在UI中的標籤可能會稍有不同，以反映它是複製成品，而非重新建置。

![重新部署](assets/Re-deploy.png)

限制:

* 重新執行生產部署步驟將僅在上次執行時可用。
* 推送更新執行無法重新執行。 如果上次執行是推送更新執行，則無法重新執行。
* 如果上次執行是推送更新執行，則無法重新執行。
* 如果上次執行在生產部署步驟之前的任何時間點失敗，則無法重新執行。

### 重新執行API {#Reexecute-API}

### 識別重新執行的執行

若要識別執行是否為重新執行，可檢查觸發欄位。 其價值將是 *執行(_E)*.

### 觸發新執行

若要觸發重新執行，必須對HAL連結&lt;(<https://ns.adobe.com/adobecloud/rel/pipeline/reExecute>)> ，而非生產部署步驟狀態。 如果此連結存在，則可從該步驟重新啟動執行。 如果不存在，則無法從該步驟重新啟動執行。 在初始版本中，此連結只會出現在生產部署步驟，但未來版本可能支援從其他步驟啟動管道。 範例:

```Javascript
 {
  "_links": {
    "https://ns.adobe.com/adobecloud/rel/pipeline/logs": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/logs",
      "templated": false
    },
    "https://ns.adobe.com/adobecloud/rel/pipeline/reExecute": {
      "href": "/api/program/4/pipeline/1/execution?stepId=2983530",
      "templated": false
    },
    "https://ns.adobe.com/adobecloud/rel/pipeline/metrics": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/metrics",
      "templated": false
    },
    "self": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530",
      "templated": false
    }
  },
  "id": "6187842",
  "stepId": "2983530",
  "phaseId": "1575676",
  "action": "deploy",
  "environment": "weretail-global-b75-prod",
  "environmentType": "prod",
  "environmentId": "59254",
  "startedAt": "2022-01-20T14:47:41.247+0000",
  "finishedAt": "2022-01-20T15:06:19.885+0000",
  "updatedAt": "2022-01-20T15:06:20.803+0000",
  "details": {
  },
  "status": "FINISHED"
```


HAL連結的語法 _href_  值以上並非用作參考點。 實際值應始終從HAL連結中讀取，而不是生成。

提交 *PUT* 向此端點提出的請求會導致 *201* 如果成功，則回應內文將代表新執行。 這類似於透過API開始定期執行。
