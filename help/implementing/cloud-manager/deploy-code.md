---
title: 部署代碼
description: 瞭解如何在as a Cloud Service中使用Cloud Manager管道部署AEM代碼。
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
source-git-commit: c6e930f62cc5039e11f2067ea31882c72be18774
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---


# 部署代碼 {#deploy-your-code}

瞭解如何在as a Cloud Service中使用Cloud Manager管道將代碼部署到生產AEM中。

![生產管線圖](./assets/configure-pipeline/production-pipeline-diagram.png)

將代碼無縫地部署到Stage ，然後直到Production ，通過生產管道完成。 生產管道執行分為兩個邏輯階段。

1. 部署到階段環境
   * 該代碼已構建並部署到Stage環境，用於自動功能測試、UI測試、體驗審核和用戶接受測試(UAT)。
1. 部署到生產環境
   * 在階段上驗證生成並批准升級到生產後，同一生成對象將部署到生產環境。

_只有「完整堆棧代碼」管道類型支援代碼掃描、功能測試、UI測試和體驗審核。_

## 在as a Cloud Service中使用雲管理器部署代AEM碼 {#deploying-code-with-cloud-manager}

一旦你 [已配置生產管道](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) 包括儲存庫、環境和測試環境，您已準備好部署代碼。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織。

1. 按一下要為其部署代碼的程式。

1. 按一下 **部署** 從行動要求開始 **概述** 螢幕以啟動部署過程。

   ![CTA](assets/deploy-code1.png)

1. 的 **管道執行** 螢幕。 按一下 **生成** 以啟動進程。

   ![「管道執行」螢幕](assets/deploy-code2.png)

生成過程將通過三個階段部署代碼。

1. [階段部署](#stage-deployment)
1. [階段測試](#stage-testing)
1. [生產部署](#production-deployment)

>[!TIP]
>
>您可以查看日誌或查看結果以查看測試標準中各個部署流程的步驟。

## 階段部署階段 {#stage-deployment}

的 **階段部署** 。 涉及到這些步驟。

* **驗證**   — 此步驟確保管道配置為使用當前可用資源。 例如，測試配置的分支是否存在以及環境是否可用。
* **構建和單元測試**  — 此步驟運行集裝箱化生成過程。
   * 請參閱文檔 [生成環境詳細資訊](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md) 的子菜單。
* **代碼掃描**  — 此步驟將評估應用程式碼的質量。
   * 請參閱文檔 [代碼質量測試](/help/implementing/cloud-manager/code-quality-testing.md) 的子菜單。
* **生成映像**  — 此過程負責將生成步驟生成的內容和分發程式包轉換為Docker映像和Kubernetes配置。
* **部署到階段**  — 映像部署到暫存環境，以準備 [階段測試階段。](#stage-testing)

![階段部署](assets/stage-deployment.png)

## 階段測試階段 {#stage-testing}

的 **階段測試** 階段涉及這些步驟。

* **產品功能測試** - Cloud Manager管道執行針對階段環境運行的test。
   * 請參閱文檔 [產品功能測試](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) 的子菜單。

* **自定義功能測試**  — 管道中的此步驟始終執行，無法跳過。 如果生成未生成testJAR，則預設情況下test會通過。
   * 請參閱文檔 [自定義功能測試](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) 的子菜單。

* **自定義UI測試**  — 此步驟是可選功能，可自動運行為自定義應用程式建立的UItest。
   * UItest是基於Selenium的test，打包在Docker映像中，允許在語言和框架（如Java和Maven、Node和WebDriver.io，或基於Selenium構建的任何其它框架和技術）中進行廣泛選擇。
   * 請參閱文檔 [自定義UI測試](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing) 的子菜單。

* **經驗審計**  — 管道中的此步驟始終執行，無法跳過。 在執行生產管道時，在將運行檢查的定製功能測試之後包括體驗審核步驟。
   * 配置的頁面將提交到服務並進行評估。
   * 這些結果是資訊性的，並顯示當前和以前的分數之間的分數和變化。
   * 這一洞見對於確定當前部署中是否將引入回歸非常重要。
   * 請參閱文檔 [瞭解經驗審計結果](/help/implementing/cloud-manager/experience-audit-testing.md) 的子菜單。

![階段測試](assets/stage-testing.png)

## 生產部署階段 {#deployment-production}

部署到生產拓撲的過程略有不同，以最大限度地減少對站點的AEM影響。

生產部署通常遵循與前面描述相同的步驟，但是採用滾動方式。

1. 部署AEM要創作的包。
1. 從負載平衡器中分離Dispatcher1。
1. 將包部AEM署到publish1，將調度程式包部署到dispatcher1，刷新調度程式快取。
1. 將dispatcher1放回負載平衡器。
1. 一旦dispatcher1恢復服務，將dispatcher2與負載平衡器分離。
1. 將包部AEM署到publish2，將調度程式包部署到dispatcher2，刷新調度程式快取。
1. 將dispatcher2放回負載平衡器中。

此過程一直持續到部署到達拓撲中的所有發佈者和調度程式為止。

![生產部署階段](assets/production-deployment.png)

## 超時 {#timeouts}

如果留在等待用戶反饋，以下步驟將超時：

| 步驟 | 逾時 |
|--- |--- |
| 代碼質量測試 | 14天 |
| 安全測試 | 14天 |
| 效能測試 | 14天 |
| 申請審批 | 14天 |
| 計畫生產部署 | 14天 |
| CSE支援 | 14天 |

## 部署過程 {#deployment-process}

所有Cloud Service部署都遵循滾動過程以確保零停機。 請參閱文檔 [滾動部署的工作方式](/help/implementing/deploying/overview.md#how-rolling-deployments-work) 來瞭解更多資訊。

## 重新執行生產部署 {#Reexecute-Deployment}

對於生產部署步驟已完成的執行，支援重新執行生產部署步驟。 完成的類型不重要 — 部署可能被取消或失敗。 話雖如此，預計主要使用案例將是生產部署步驟因暫時原因而失敗的案例。 重新執行使用同一管道建立新執行。 此新執行包括三個步驟：

1. 驗證步驟 — 這實質上與正常管道執行期間發生的驗證相同。
1. 生成步驟 — 在重新執行的上下文中，生成步驟是複製對象，而不是實際執行新的生成進程。
1. 生產部署步驟 — 與正常管道執行中的生產部署步驟使用相同的配置和選項。

生成步驟在UI中的標籤可能稍有不同，以反映它正在複製對象，而不是重新生成。

![重新部署](assets/Re-deploy.png)

限制:

* 重新執行生產部署步驟將僅在上次執行時可用。
* 無法重新執行推式更新執行。 如果上次執行是推式更新執行，則不可能重新執行。
* 如果上次執行是推式更新執行，則不可能重新執行。
* 如果上次執行在生產部署步驟之前的任何時間點失敗，則無法重新執行。

### 重新執行API {#Reexecute-API}

### 標識重新執行

為了確定執行是否是重新執行，可檢查觸發欄位。 它的價值是 *執行(_E)*。

### 觸發新執行

要觸發重新執行，需要向HAL連結&lt;(PUT請求)<http://ns.adobe.com/adobecloud/rel/pipeline/reExecute>)>。 如果存在此連結，則可以從該步驟重新啟動執行。 如果缺少，則無法從該步驟重新啟動執行。 在初始版本中，此連結將只出現在生產部署步驟中，但將來的版本可能支援從其他步驟啟動管道。 範例:

```Javascript
 {
  "_links": {
    "http://ns.adobe.com/adobecloud/rel/pipeline/logs": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/logs",
      "templated": false
    },
    "http://ns.adobe.com/adobecloud/rel/pipeline/reExecute": {
      "href": "/api/program/4/pipeline/1/execution?stepId=2983530",
      "templated": false
    },
    "http://ns.adobe.com/adobecloud/rel/pipeline/metrics": {
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


HAL連結的語法 _href_  以上值不打算用作參考點。 實際值應始終從HAL連結中讀取而不是生成。

提交 *PUT* 對此終結點的請求將導致 *201* 如果成功，則響應主體將表示新執行。 這類似於通過API啟動常規執行。
