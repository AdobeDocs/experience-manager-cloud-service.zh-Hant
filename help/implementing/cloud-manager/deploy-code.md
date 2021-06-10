---
title: 部署程式碼 — Cloud Services
description: 部署程式碼 — Cloud Services
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
source-git-commit: 64023bbdccd8d173b15e3984d0af5bb59a2c1447
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 2%

---

# 部署程式碼 {#deploy-your-code}

## 在AEM as aCloud Service{#deploying-code-with-cloud-manager}中使用Cloud Manager部署程式碼

一旦配置了生產管道（儲存庫、環境和測試環境），您就可以部署代碼。

1. 按一下Cloud Manager中的&#x200B;**Deploy**&#x200B;以啟動部署過程。

   ![](assets/deploy-code1.png)


1. 將顯示&#x200B;**Pipeline Execution**&#x200B;螢幕。

   按一下&#x200B;**Build**&#x200B;以啟動進程。

   ![](assets/deploy-code2.png)

1. 完成的建置程式會部署您的程式碼。

   建置程式涉及下列階段：

   1. 階段部署
   1. 階段測試
   1. 生產部署

   >[!NOTE]
   >
   >此外，您也可以檢視記錄或檢閱測試條件的結果，以檢閱各種部署程式的步驟。

   「 **舞台部署**」涉及以下步驟：

   * 驗證：此步驟可確保管道配置為使用當前可用資源，例如，配置的分支存在，環境可用。
   * 構建和單元測試：此步驟會執行容器化的建置程式。 如需有關建置環境的詳細資訊，請參閱[建置環境詳細資料](/help/onboarding/getting-access-to-aem-in-cloud/build-environment-details.md)。
   * 代碼掃描：此步驟會評估應用程式程式碼的品質。 如需測試程式的詳細資訊，請參閱[程式碼品質測試](/help/implementing/cloud-manager/code-quality-testing.md)。
   * 生成映像：此步驟包含用來建立影像之程式的記錄檔。 此程式負責將建置步驟產生的內容和Dispatcher套件轉換為Docker影像和Kubernetes設定。
   * 部署至預備

      ![](assets/stage-deployment.png)
   測試 **階段**，包括下列步驟：

   * **產品功能測試**:Cloud Manager管道執行將支援針對預備環境執行的測試。如需詳細資訊，請參閱[產品功能測試](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing) 。

   * **自訂功能測試**:管道中的此步驟一律存在，且無法略過。但是，如果組建未產生測試JAR，則測試預設會通過。\
      如需詳細資訊，請參閱[自訂功能測試](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing) 。

   * **自訂UI測試**:此步驟是選用功能，可讓客戶建立並自動執行其應用程式的UI測試。UI測試是封裝在Docker影像中的基於硒的測試，以允許在語言和框架（如Java和Maven、Node和WebDriver.io，或基於Selenium構建的任何其他框架和技術）中進行廣泛選擇。
如需詳細資訊，請參閱[自訂UI測試](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/test-results/functional-testing.html?lang=en#custom-ui-testing) 。


   * **體驗稽核**:管道中的此步驟一律存在，且無法略過。執行生產管道時，將在自訂功能測試（將執行檢查）後納入體驗稽核步驟。 系統會將已設定的頁面提交至服務並進行評估。 結果提供資訊，讓使用者可查看目前和先前分數之間的分數和變更。 此深入分析對於判斷是否有將於目前部署引入的回歸十分有用。
如需詳細資訊，請參閱[了解體驗稽核結果](/help/implementing/cloud-manager/experience-audit-testing.md) 。

      ![](assets/stage-testing.png)





## 部署過程{#deployment-process}

所有Cloud Service部署都會依循滾動程式，確保零停機時間。 請參閱[滾動部署如何運作](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html#how-rolling-deployments-work)以了解詳細資訊。

### 部署到生產階段{#deployment-production-phase}

部署至生產拓撲的程式稍有不同，以將對AEM網站訪客的影響降至最低。

生產部署通常會依照上述步驟進行，但以滾動方式進行：

1. 部署AEM套件以製作。
1. 從負載平衡器分離dispatcher1。
1. 將AEM套件部署至publish1，並將Dispatcher套件部署至dispatcher1，排清Dispatcher快取。
1. 將dispatcher1放回負載平衡器。
1. 當dispatcher1重新服務後，請從負載平衡器分離dispatcher2。
1. 將AEM套件部署至publish2，並將Dispatcher套件部署至dispatcher2，排清Dispatcher快取。
1. 將dispatcher2放回負載平衡器。
此過程將繼續，直到部署已到達拓撲中的所有發佈商和調度程式。
