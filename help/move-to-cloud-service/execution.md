---
title: 執行階段
description: 執行階段
exl-id: 176dd79d-0d72-443c-87db-dab24fb48b96
source-git-commit: dfbd0f38017d02810da05ccadbc5f2fbd5826aa3
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 96%

---

# 執行 {#execution-phase}

在開始「執行」階段之前，您應該先加入雲端服務。您也需要熟悉 Cloud Manager，因為這是將程式碼部署至 AEM 雲端服務的唯一辦法。

Cloud Manager 可讓組織在雲端中自行管理 AEM。其內容包含持續整合與持續傳送 (CI/CD) 架構，可讓 IT 團隊與實作合作夥伴加快提供自訂或更新的傳送速度，而不會影響效能或安全性。

如需詳細資訊，請參考下列資源：

* [加入 Experience Manager as a Cloud Service](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/onboarding/home.html)，了解有關加入 Experience Manager as a Cloud Service 的自助資源。

* [整合 Git 與 Adobe Cloud Manager](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/managing-code/integrating-with-git.html)，了解如何使用 Single Git 存放庫來部署程式碼。

* [Adobe Experience as a Cloud Service 設定](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/security/ims-support.html#aem-configuration)，了解如何「在 Admin Console 中管理產品與使用者存取」。


## 簡介 {#introduction}

轉換至雲端服務的確切步驟取決於您購買的系統，以及所遵循的軟體開發生命週期作法。

下圖將展示「執行」階段中的主要步驟：

![影像](/help/move-to-cloud-service/assets/exec-image1.png)

## 內容轉移 {#content-transfer}

如果要將內容從您目前的 AEM 例項轉移至雲端服務例項，您可以使用 Adobe 的「內容轉移工具」。

使用此工具，即可指定想從您的 AEM 例項轉移至雲端服務例項的內容。

>[!NOTE]
>建議您先頻繁地執行追加差異內容，以縮短最終差異化內容轉移的內容凍結時間，然後再於雲端服務上線。

如需詳細資訊，請參考[內容轉移工具](/help/move-to-cloud-service/content-transfer-tool/overview-content-transfer-tool.md)。

>[!IMPORTANT]
>「內容轉移工具」的最低系統需求為 AEM 6.3 + 和 JAVA 8。如果您使用較舊版本的 AEM，您必須將內容存放庫升級至 AEM 6.5 才能使用「內容轉移工具」。

## 程式碼重構 {#code-refactor}

在 AEM as a Cloud Service 中開發及執行程式碼時必須改變習慣。請注意，程式碼必須具復原性，特別是因為例項可能隨時停止。您必須了解，在雲端服務中執行程式碼時，一律會在叢集中執行。這表示執行中的例項永遠多於一個。

AEM Maven 專案必須進行某些變更，才能與 AEM as a Cloud Service 相容。AEM as a Cloud Service 需要將&#x200B;*內容*&#x200B;和&#x200B;*程式碼*&#x200B;分離為離散封裝，以便部署至 AEM。

* `/apps` and `/libs` are consed inmumable areas of AEM as they cannot be changed(create, update, delete)after AEM starts(i.e. at runtime)。在運行時更改不可變區域的任何嘗試都將失敗。

* 存放庫中的所有其它項目如 `/content`、`/conf`、`/var`、`/home`、`/etc`、`/oak:index`、`/system`、`/tmp` 等都是可變區域，這表示可在執行時期變更它們。

如需詳細資訊，請參考[建議封裝結構](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/developing/aem-project-content-package-structure.html#recommended-package-structure)。

在使用 AEM as a Cloud Service 開發時，您需要留意一些額外的開發准則。請參考 [AEM as a Cloud Service 開發准則](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/developing/development-guidelines.html)以深入了解。

您應該從「規劃」階段開始，便列出需要重構以便與雲端服務相容的區域。您也應該檢視[開發准則](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/developing/development-guidelines.html)以取得詳細資訊，了解如何重構和最佳化程式碼以便移轉至雲端服務。

如果要加速某些程式碼重構任務，您可以使用下列工具：

* [資產工作流程移轉](/help/move-to-cloud-service/moving-to-aem-assets/asset-workflow-migration-tool.md)
* [Dispatcher 轉換工具](/help/move-to-cloud-service/refactoring-tools/dispatcher-transformation-utility-tools.md)
* [現代化工具](/help/move-to-cloud-service/refactoring-tools/aem-modernization-tools.md)

建議您先在本機上重構並測試程式碼，然後再透過 Cloud Manager Git 推送至雲端服務環境。

請檢視 [AEM SDK](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/deploying/overview.html#aem-as-a-cloud-service-sdk) 文件以深入了解。

以下列出其他資源：

* 觀看「安裝 Dispatcher SDK」，了解如何安裝 Dispatcher SDK：

   >[!VIDEO](https://video.tv.adobe.com/v/30601)

* 觀看「設定 Dispatcher SDK」，了解如何設定 Dispatcher SDK：

   >[!VIDEO](https://video.tv.adobe.com/v/30602)

* 檢視[本機開發設定](https://docs.adobe.com/content/help/en/experience-manager-learn/cloud-service/local-development-environment-set-up/overview.html)文件，以便設定本機開發環境


如果要管理您正在作用中 AEM 上開發的程式碼，以及轉換過程中的程式碼重構任務，建議先排程程式碼凍結期間，直到您的 Maven 專案重建完畢、可以與 AEM as a Cloud Service 相容為止。

專案一旦重建完畢，即可根據這個新結構繼續開發新的程式碼。這將減少 Cloud Manager 管線在程式碼部署和測試期間的故障情形。

>[!NOTE]
>「內容轉移」和「程式碼重新調整」任務並未依順序進行。這些任務可以各自獨立完成。不過，您需要正確的專案結構，以確保內容能在雲端服務環境中成功轉譯。

## 程式碼部署和測試的最佳作法 {#best-practices}

使用 Cloud Manager 進行雲端服務管線執行時，會支援針對預備環境執行的測試。

請參考[程式碼品質測試](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/developing/understand-test-results.html#code-quality-testing)，了解如何編寫測試指令碼。當中會建議您將涵蓋範圍設為至少 50%。

此外，請參考[了解自訂程式碼品質規則](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/using-cloud-manager/custom-code-quality-rules.html)，深入了解 Cloud Manager 根據 AEM Engineering 最佳作法建立並執行的自訂程式碼品質規則。

使用 Cloud Manager 是將程式碼部署至雲端服務環境的唯一辦法。

請依照以下資源，了解如何使用 Cloud Manager 管理和部署您的程式碼。

* [管理環境](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html)

* [設定 CI-CD 管線](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html)

* [部署程式碼](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html)

## 上線準備作業的最佳作法 {#go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_prep"
>title="上線準備"
>abstract="為確保順利成功地在AEM as aCloud Service上線，您應針對程式碼和內容凍結期間、測試反覆項目、內容追加、效能測試、安全性測試等進行規劃。"

如果要確保順利成功地上線至 AEM as a Cloud Service，您應該考慮執行下列步驟：

* 排程程式碼和內容凍結期間
* 執行最終追加內容
* 完成測試反覆項目
* 執行效能與安全性測試
* 完全移轉
