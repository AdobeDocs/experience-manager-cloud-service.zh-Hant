---
title: 上線
description: 了解在程式碼和內容雲端準備就緒後，如何執行移轉
source-git-commit: bcbf4e4ba1330bef9f2c8c473419903e40ac0e58
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 0%

---


# 上線 {#go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_prep"
>title="上線準備"
>abstract="為確保順利成功上線至AEMas a Cloud Service，您應針對程式碼和內容凍結期間、測試反覆項目、內容追加、效能測試、安全性測試等進行規劃。"

在歷程的這部分，您將學習如何在程式碼和內容都準備好移至AEM  as a Cloud Service時，規劃及執行移轉。 此外，您也會了解執行移轉時的最佳實務和已知限制。

## 迄今為止的故事 {#story-so-far}

在歷程的前幾個階段：

* 您已了解如何開始在 [快速入門](/help/journey-migration/getting-started.md) 頁面。
* 閱讀 [準備階段](/help/journey-migration/readiness.md)
* 熟悉工具和程式，以便透過這些工具和程式，為您的程式碼和內容雲準備好 [實施階段](/help/journey-migration/implementation.md).

## 目標 {#objective}

本檔案將協助您了解熟悉歷程的先前步驟後，如何執行AEMas a Cloud Service移轉。 您將學習如何執行初始生產移轉，以及移轉至AEM as a Cloud Service時應遵循的最佳實務。

## 初始生產移轉 {#initial-migration}

在執行生產移轉之前，請遵循 [內容遷移策略和時間表](/help/journey-migration/implementation.md##strategy-timeline) 區段 [實施階段](/help/journey-migration/implementation.md).

* 根據您在克隆上執行的AEMas a Cloud Service階段遷移過程中獲得的經驗，從生產環境開始遷移：
   * 作者 — 作者
   * Publish-Publish

>[!NOTE]
>
>擷取期間會顯示AEMas a Cloud Service作者，但擷取期間會顯示as a Cloud Service發佈。

* 驗證內嵌至AEMas a Cloud Service製作和發佈層級的內容。
* 指示內容製作團隊在擷取完成前，避免在來源和目的地上移動內容
* 可以新增、編輯或刪除新內容，但請避免移動內容。 這會同時套用至來源和目的地。
* 記錄 [所花時間](/help/journey-migration/implementation.md#gathering-data) 以完整提取和擷取，並預估未來追加移轉時間。
* 建立 [遷移計畫程式](/help/journey-migration/implementation.md#migration-plan) 供作者和發佈使用。

## 增量追加 {#top-up}

從生產環境進行初始移轉後，您必須執行增量追加，以確保將內容帶入雲端執行個體上為最新。 因此，建議您遵循下列最佳實務：

* 收集內容量的資料。 例如：每週、兩週或一個月。
* 請務必以避免超過48小時的內容擷取和擷取的方式來規劃追加資源。 建議您這麼做，以便將追加內容納入週末時間範圍。
* 規劃所需追加數量，並使用這些估計值在上線日期前後進行規劃。

## 確定遷移的代碼和內容凍結時間表 {#code-content-freeze}

如前所述，您必須排程程式碼和內容凍結期間。 使用下列問題可幫助您規劃凍結期間：

* 必須凍結內容製作活動多久？
* 我應要求我的傳送團隊停止新增功能多久？

若要回答第一個問題，您應考量在非生產環境中執行試用執行所花的時間。 若要回答第二個問題，您需要新增功能的團隊與重構程式碼的團隊之間密切合作。 目標應是確保新增至現有部署的所有程式碼也已新增、測試及部署至雲端服務分支。 一般而言，這表示程式碼凍結量會較低。

此外，當排程最終追加內容時，您需要規劃內容凍結。

## 最佳作法 {#best-practices}

規劃或執行移轉時，您應考量下列准則：

* 從作者移轉至作者，再從發佈移轉至發佈
* 請求可用於下列用途的生產克隆：
   * 捕獲儲存庫統計資訊
   * 移轉活動的證明
   * 準備遷移計畫
   * 確定內容凍結要求
   * 從生產環境進行移轉時，找出生產環境的任何升級需求

**內容轉移工具最佳作法**

請務必在上線時，在生產環境中執行內容移轉，而非原地複製。 一個好辦法是 [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) 進行初始移轉，然後經常（甚至每天）追加擷取，以擷取較小的區塊，並避免來源AEM上出現任何長期負載。

執行生產遷移時，應避免從克隆運行「內容轉移工具」，因為：

* 如果客戶要求在追加遷移期間遷移內容版本，則從克隆執行內容轉移工具不會遷移這些版本。 即使經常從即時作者重新建立原地復本，每次建立原地復本時，內容轉移工具將用來計算增量的查核點都會重設。
* 由於克隆無法整體刷新，因此必須使用ACL查詢包來包裝和安裝要從生產環境添加或編輯到克隆的內容。 此方法的問題是，除非從源實例和克隆中手動刪除，否則源實例上所有已刪除的內容都不會到達克隆。 這樣，在克隆和AEMas a Cloud Service上，刪除的生產內容不會被刪除。

**執行內容移轉時，最佳化AEM來源的載入**

請記住，提取階段期間AEM來源的負載會較大。 請注意：

* 「內容轉移工具」是使用4 GB JVM堆的外部Java進程
* 非AzCopy版本會下載二進位檔，將其儲存在來源AEM作者的暫時空間上，使用磁碟I/O，然後上傳至佔用網路頻寬的Azure容器
* [AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) 將blob直接從blob儲存區傳輸至Azure容器，以節省磁碟I/O和網路頻寬。 AzCopy版本仍使用磁碟和網路頻寬，從段儲存中提取資料並將其上傳到Azure容器中
* 在擷取階段期間，「內容轉移工具」程式會較輕地處理系統資源，因為它只會串流擷取記錄，而且就磁碟I/O或網路頻寬而言，來源執行個體的負載並不多。

## 已知限制 {#known-limitations}

如果在擷取的移轉集中發現下列任何限制，請考慮整個擷取作業會失敗：

* 名稱超過150個字元的JCR節點
* 大於16 MB的JCR節點
* 任何使用者/群組 `rep:AuthorizableID` 已擷取AEMas a Cloud Service上已存在的
* 如果任何擷取和擷取的資產在移轉的下一個迭代之前，移至來源或目的地的不同路徑。

## 資產運作狀況 {#asset-health}

與擷取上方的區段比較 **不** 失敗，原因如下： 不過，強烈建議您在下列情況下採取適當步驟：

* 遺失原始轉譯的任何資產
* 任何缺少的資料夾 `jcr:content` 節點

上述兩個項目將於 [Best Practice Analyzer](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) 報表。

## 上線檢查清單 {#Go-Live-Checklist}

請檢閱下方呈現的活動清單，確保您能順利成功地執行移轉作業：

* 排程程式碼和內容凍結期間。 另請參閱 [移轉的程式碼和內容凍結時間軸](#code-content-freeze).
* 執行最終追加內容
* 完成測試反覆項目
* 執行效能與安全性測試
* 完全移轉 並在生產執行個體上執行移轉

您隨時都可以參考清單，以備在執行移轉時重新校準任務時使用。

## 下一步 {#what-is-next}

了解如何執行AEMas a Cloud Service移轉後，即可檢查 [上線後](/help/journey-migration/post-go-live.md) 頁面，讓執行個體順利執行。