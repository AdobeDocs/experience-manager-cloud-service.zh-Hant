---
title: 部署程式碼 — Cloud Services
description: 部署程式碼 — Cloud Services
exl-id: 2c698d38-6ddc-4203-b499-22027fe8e7c4
source-git-commit: 782035708467693ec7648b1fd701c329a0b5f7c8
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 1%

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

以下章節說明如何在階段階段和生產階段部署AEM和Dispatcher套件。

Cloud Manager會將建置程式產生的所有target/*.zip檔案上傳至儲存位置。  在管道的部署階段，會從此位置檢索這些對象。

當Cloud Manager部署至非生產拓撲時，目標是盡快完成部署，因此成品會同時部署至所有節點，如下所示：

1. Cloud Manager會判斷每個工件是AEM或Dispatcher套件。
1. Cloud Manager會從負載平衡器中移除所有調度程式，以在部署期間隔離環境。

   除非另有配置，否則您可以跳過開發和階段部署中的負載平衡器更改，即分離和附加非生產管道中的步驟，用於開發環境，以及生產管道，用於預備環境。

   >[!NOTE]
   >
   >此功能預計主要供1-1-1名客戶使用。

1. 每個AEM工件都會透過套件管理器API部署至每個AEM執行個體，且套件相依性會決定部署順序。

   要進一步了解如何使用包來安裝新功能、在實例之間轉移內容以及備份儲存庫內容，請參閱如何使用包。

   >[!NOTE]
   >
   >所有AEM成品都部署至作者和發佈者。 需要節點特定設定時，應運用執行模式。 若要進一步了解執行模式可如何讓您針對特定用途調整AEM執行個體，請參閱執行模式。

1. Dispatcher工件會依下列方式部署至每個Dispatcher:

   1. 當前配置被備份並複製到臨時位置
   1. 除不可變的檔案外，所有配置都將被刪除。 如需詳細資訊，請參閱管理Dispatcher設定。 這會清除目錄，以確保不會留下任何孤立的檔案。
   1. 將對象提取到`httpd`目錄。  不可覆寫的檔案。 在部署時，您對Git存放庫中不可變的檔案所做的任何變更都會被忽略。  這些檔案是AMS Dispatcher架構的核心，無法變更。
   1. Apache會執行設定測試。 若未找到錯誤，則會重新載入服務。 如果發生錯誤，則會從備份還原設定、重新載入服務，並將錯誤回報至Cloud Manager。
   1. 管道設定中指定的每個路徑都會失效或從Dispatcher快取中清除。

   >[!NOTE]
   >
   >Cloud Manager預期Dispatcher工件會包含完整的檔案集。  所有Dispatcher設定檔都必須存在於Git存放庫中。 缺少檔案或資料夾將導致部署失敗。

1. 成功將所有AEM和Dispatcher套件部署至所有節點後，Dispatcher會新增回負載平衡器，且部署完成。

   >[!NOTE]
   >
   >您可以跳過開發和預備部署中的負載平衡器更改，即在非生產管道、開發人員環境和生產管道中（用於預備環境）分離和附加步驟。

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
