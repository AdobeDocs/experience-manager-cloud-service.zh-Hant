---
title: 部署您的程式碼——雲端服務
description: 部署您的程式碼——雲端服務
translation-type: tm+mt
source-git-commit: aef8afd3efca4d6d5db9f457e952958ee9ca38de
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 1%

---


# 部署程式碼 {#deploy-your-code}

## 使用Cloud Manager部署代碼{#deploying-code-with-cloud-manager}

一旦配置了生產管線（儲存庫、環境和測試環境），您就可以部署代碼。

1. 從Cloud Manager按一下「**部署**」以開始部署程式。

   ![](assets/deploy-code1.png)


1. 將顯示&#x200B;**管線執行**&#x200B;螢幕。

   按一下&#x200B;**Build**&#x200B;啟動進程。

   ![](assets/deploy-code2.png)

1. 完整的建立程式會部署您的程式碼。

   構建過程涉及以下階段：

   1. 階段部署
   1. 階段測試
   1. 生產部署

   >[!NOTE]
   >
   >此外，您也可以檢視記錄檔或檢視結果，以檢視各種部署程式中的步驟，以取得測試標準。

   「 **舞台部署**」涉及以下步驟：

   * 驗證：此步驟確保將管線配置為使用當前可用資源，例如，已配置的分支存在，環境可用。
   * 構建和單元測試：此步驟會執行容器化的建立程式。 有關構建環境的詳細資訊，請參閱[構建環境詳細資訊](/help/onboarding/getting-access-to-aem-in-cloud/build-environment-details.md)。
   * 代碼掃描：此步驟會評估您的應用程式碼的品質。 如需測試程式的詳細資訊，請參閱[程式碼品質測試](/help/implementing/cloud-manager/code-quality-testing.md)。
   * 建立影像：此步驟包含用於構建映像的進程的日誌檔案。 此程式負責將構建步驟生成的內容和調度程式包轉換為Docker映像和Kubernetes配置。
   * 部署至舞台

      ![](assets/stage-deployment.png)
   測試 **階段**，包括下列步驟：

   * 產品功能測試：Cloud Manager管道執行將支援對舞台環境運行的測試的執行。
如需詳細資訊，請參閱[產品功能測試](/help/implementing/cloud-manager/functional-testing.md#product-functional-testing)。

   * 自訂功能測試：管線中的此步驟始終存在，不能跳過。 但是，如果構建版本未生成測試JAR，則預設情況下測試通過。\
      如需詳細資訊，請參閱[自訂功能測試](/help/implementing/cloud-manager/functional-testing.md#custom-functional-testing)。

   * 自訂UI測試：管線中的此步驟始終存在，不能跳過。 您可編寫自訂UI測試，讓客戶快速建立測試自動化套件，以驗證以AEM為基礎的網頁和行動應用程式。
如需詳細資訊，請參閱[自訂UI測試](/help/implementing/cloud-manager/functional-testing.md#custom-ui-testing)。

   * 體驗審核：管線中的此步驟始終存在，不能跳過。 執行生產管線時，會在執行檢查的自訂功能測試後加入體驗稽核步驟。 所設定的頁面將會提交至服務並進行評估。 這些結果是提供資訊的，讓使用者可以查看目前和先前的分數之間的分數和變更。 此見解對於判斷目前部署中是否會引入回歸，十分有用。
如需詳細資訊，請參閱[瞭解體驗稽核結果](/help/implementing/cloud-manager/experience-audit-testing.md)。

      ![](/help/implementing/cloud-manager/assets/deploy-testingscreen.png)





## 部署過程{#deployment-process}

下節說明AEM和Dispatcher套件在階段階段和生產階段的部署方式。

Cloud Manager會將建立程式產生的所有目標/*.zip檔案上傳至儲存位置。  在管線的部署階段，會從此位置檢索這些對象。

當Cloud Manager部署到非生產拓撲時，其目標是盡快完成部署，因此對象將同時部署到所有節點，如下所示：

1. Cloud Manager會決定每個對象是AEM還是分派程式套件。
1. Cloud Manager會從負載平衡器中刪除所有調度程式，以在部署期間隔離環境。

   除非另行配置，否則您可以跳過開發和階段部署中的負載平衡器更改，即分離和附加非生產管線中的步驟，以用於開發環境，以及生產管線中的步驟，用於階段環境。

   >[!NOTE]
   >
   >此功能預期主要由1-1-1客戶使用。

1. 每個AEM物件都會透過Package Manager API部署至每個AEM例項，並包含套件相依性，以決定部署順序。

   有關如何使用軟體包來安裝新功能、在實例之間傳輸內容以及備份儲存庫內容的詳細資訊，請參閱如何使用軟體包。

   >[!NOTE]
   >
   >所有AEM物件都會部署至作者和發佈者。 當需要特定節點的配置時，應使用運行模式。 若要進一步瞭解「執行模式」如何讓您針對特定用途調整AEM例項，請參閱「執行模式」。

1. 調度器對象按如下方式部署到每個調度器：

   1. 當前配置將備份並複製到臨時位置
   1. 除不可變檔案外，所有配置都將被刪除。 有關詳細資訊，請參閱管理Dispatcher配置。 這會清除目錄，以確保不會留下孤立的檔案。
   1. 該對象被提取到`httpd`目錄。  不會覆寫不可變的檔案。 在部署時，您對git儲存庫中不可變檔案所做的任何更改都將被忽略。  這些檔案是AMS調度器框架的核心檔案，不能更改。
   1. Apache會執行組態測試。 如果未找到錯誤，則重新載入服務。 如果發生錯誤，則從備份中恢復配置，重新載入服務，並將錯誤報告回Cloud Manager。
   1. 在流水線配置中指定的每個路徑都無效或從調度器快取中刷新。

   >[!NOTE]
   >
   >Cloud Manager希望調度器對象包含完整檔案集。  所有調度程式配置檔案都必須存在於git儲存庫中。 缺少檔案或資料夾將導致部署失敗。

1. 成功將所有AEM和Dispatcher套件部署至所有節點後，會將Dispatcher新增至負載平衡器，而部署即告完成。

   >[!NOTE]
   >
   >您可以跳過開發和階段部署中的負載平衡器更改，即在非生產流水線、開發人員環境和生產流水線中分離和附加步驟，以用於階段環境。

### 部署到生產階段{#deployment-production-phase}

部署至生產拓撲的程式略有不同，以盡量降低對AEM網站訪客的影響。

生產部署通常遵循與上述步驟相同的步驟，但是以滾動方式：

1. 部署AEM套件以製作。
1. 從負載平衡器分離dispatcher1。
1. 將AEM封裝部署至publish1，並將dispatcher封裝部署至dispatcher1，以刷新dispatcher快取。
1. 將dispatcher1放回負載平衡器。
1. 在dispatcher1恢復服務後，請從負載平衡器分離dispatcher2。
1. 將AEM套件部署至publish2，將dispatcher套件部署至dispatcher2，以刷新dispatcher快取。
1. 將dispatcher2放回負載平衡器。
此過程將繼續，直到部署到拓撲中所有發佈者和調度程式為止。


