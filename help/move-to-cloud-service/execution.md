---
title: 執行階段
description: 執行階段
translation-type: tm+mt
source-git-commit: 3478827949356c4a4f5133b54c6cf809f416efef
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 7%

---


# 執行 {#execution-phase}

在開始執行階段之前，您應已登入雲端服務。 您也需要熟悉Cloud Manager，因為它是將程式碼部署至AEM Cloud服務的唯一機制。

Cloud Manager可讓組織在Cloud中自行管理AEM。 其內容包含持續整合與持續傳送 (CI/CD) 架構，可讓 IT 團隊與實作合作夥伴加快提供自訂或更新的傳送速度，而不會影響效能或安全性。

如需詳細資訊，請參閱下列資源：

* [以雲端服務身分登入Experience Manager](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/onboarding/home.html) ，以瞭解有關以雲端服務身分登入Experience Manager的自助資源。

* [將Git與Adobe Cloud Manager整合](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html) ，以瞭解如何使用Single Git儲存庫來部署程式碼。

* [Adobe Experience as a Cloud Service Configuration](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/security/ims-support.html#aem-configuration) ，以瞭解Admin Console中的「管理產品與使用者存取」。


## 簡介 {#introduction}

向雲服務過渡的確切步驟取決於您購買的系統以及遵循的軟體開發生命週期實踐。

下圖顯示了「執行」階段涉及的主要步驟：

![影像](/help/move-to-cloud-service/assets/exec-image1.png)

## 內容傳輸 {#content-transfer}

若要將您目前的AEM實例內容傳輸至您的Cloud Service實例，您可以使用Adobe的內容傳輸工具。

透過此工具，您可以指定您要從來源AEM例項傳輸至AEM Cloud服務例項的內容子集。

>[!NOTE]
>建議在雲端服務上線之前，先頻繁執行差異式內容更新，以縮短最終差異式內容傳輸的內容凍結期。

如需詳細 [資訊，請參閱內容](/help/move-to-cloud-service/content-transfer-tool/overview-content-transfer-tool.md) 傳輸工具。

>[!IMPORTANT]
>內容傳輸工具的最低系統需求為AEM 6.3 +和JAVA 8。 如果您使用較低的AEM版本，您將需要將內容儲存庫升級至AEM 6.5，才能使用內容傳輸工具。

## 程式碼重構 {#code-refactor}

在AEM中以雲端服務形式開發和執行程式碼時，需要改變心意。 應當指出，程式碼必須具有彈性，尤其是當例項可能隨時停止時。 在雲端服務中執行的程式碼必須知道，它一律在叢集中執行。 這表示執行中總有多個執行個體。

AEM Maven專案必須進行某些變更，才能與AEM（雲端服務）相容。 AEM做為雲端服務需要將內容和程 *式碼分**離* 散的套件，以部署至AEM。

* `/apps` and `/libs` are consed inmumable areas of AEM as they cannot be changed(create, update, delete)after AEM starts(i.e. at runtime)。在運行時更改不可變區域的任何嘗試都將失敗。

* 儲存庫中的其 `/content` 它所有項 `/conf` 目， 、 `/var` 、 、 、 `/home` 、 `/etc``/oak:index``/system``/tmp` 、等。 都是可變區域，也就是說，這些區域可在執行時期進行變更。

如需詳細 [資訊，請參閱Recommended Package Structure](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#recommended-package-structure) 。

在以AEM做為雲端服務進行開發時，您需要注意一些其他開發准則。 請參閱「 [AEM雲端服務開發准則」](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html) ，瞭解更多資訊。

在規劃階段，您應列出需要重構為與雲端服務相容的區域。 您也應檢閱開發 [准則](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html) ，以取得如何重新調整和最佳化程式碼以改用雲端服務的詳細資訊。

若要協助加速某些程式碼重構工作，您可以使用下列工具：

* [資產工作流程移轉](/help/move-to-cloud-service/moving-to-aem-assets/asset-workflow-migration-tool.md)
* [Dispatcher Converter](/help/move-to-cloud-service/refactoring-tools/dispatcher-transformation-utility-tools.md)
* [現代化工具](/help/move-to-cloud-service/refactoring-tools/aem-modernization-tools.md)

建議在透過Cloud Manager Git將程式碼推送至雲端服務環境之前，先在本機重新調整並測試程式碼。

請檢閱 [AEM SDK](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#aem-as-a-cloud-service-sdk) 檔案以進一步瞭解。

下面列出一些其他資源：

* 觀看安裝Dispatcher SDK以瞭解如何安裝Dispatcher SDK:

   > [!VIDEO](https://video.tv.adobe.com/v/30601)

* 觀看Configure Dispatcher SDK以瞭解如何設定Dispatcher SDK:

   > [!VIDEO](https://video.tv.adobe.com/v/30602)

* 檢閱 [當地開發設定](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html) 檔案，以設定當地開發環境


若要在您的轉場歷程中，管理您目前在作用中AEM上進行的程式碼開發以及程式碼重構工作，建議您先排程程式碼凍結期，直到您完成重組Maven專案，以便與AEM（雲端服務）相容為止。

一旦完成專案重組，您就可以根據此新結構，繼續開發新的程式碼。 這將減少程式碼部署和測試期間的Cloud Manager管道故障。

>[!NOTE]
>「內容傳輸」和「程式碼重新調整」工作並未依序進行。 這些任務可以相互獨立地完成。 不過，您需要正確的專案結構，以確保內容能在您的雲端服務環境中成功轉譯。

## 程式碼部署與測試的最佳實務 {#best-practices}

Cloud Manager for Cloud Services管道執行將支援對舞台環境運行的測試的執行。

請參閱程 [式碼品質測試](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/understand-test-results.html#code-quality-testing) ，以瞭解如何編寫測試指令碼，並建議至少涵蓋50%。

此外，請參閱「了 [解自訂代碼品質規則」](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/custom-code-quality-rules.html) ，進一步瞭解Cloud Manager根據AEM Engineering的最佳實務所建立的自訂代碼品質規則。

Cloud Manager的使用是將程式碼部署至Cloud Service環境的唯一機制。

請依照下列資源，瞭解如何使用Cloud Manager管理和部署您的程式碼。

* [管理環境](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html)

* [配置CI-CD管道](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html)

* [部署程式碼](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html)

## 上線準備的最佳做法 {#go-live}

若要確保AEM的雲端服務順暢且成功上線，您應考慮執行下列步驟：

* 排程程式碼和內容凍結期
* 執行最終內容向上
* 完成測試迭代
* 執行效能與安全性測試
* 切換
