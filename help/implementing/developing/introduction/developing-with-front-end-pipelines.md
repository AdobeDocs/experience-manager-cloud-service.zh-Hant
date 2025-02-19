---
title: 使用前端管道開發網站
description: 有了前端管道，前端開發人員可獲得更多獨立性，開發流程可以獲得大幅度的速度。 本檔案說明應提供的前端建置流程的一些特定考量事項。
exl-id: 996fb39d-1bb1-4dda-a418-77cdf8b307c5
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 1%

---


# 使用前端管道開發網站 {#developing-site-with-front-end-pipeline}

[有了前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)，給前端開發人員更多的獨立性，開發過程可以大幅加速。 本檔案說明此程式的運作方式以及一些需要注意的事項，以便您能夠充分發揮此程式的潛力。

>[!TIP]
>
>如果您還不熟悉如何使用前端管道及其帶來的好處，請檢視[快速網站建立歷程](/help/journey-sites/quick-site/overview.md)，以示範如何快速部署新網站並完全獨立於後端開發來自訂其主題。

## 前端建置合約 {#front-end-build-contract}

與[完整棧疊組建環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)類似，前端管道有自己的環境。 開發人員可使用此管道靈活運用，只要遵循以下前端建置合約。

前端管道需要前端Node.js專案才能使用`build`指令碼指示詞來產生它部署的組建。 這是因為Cloud Manager使用命令`npm run build`產生前端組建的可部署專案。

`dist`資料夾的結果內容將由Cloud Manager最終部署，並作為靜態檔案提供。 這些檔案由外部託管至AEM，但可透過已部署環境上的`/content/...` URL取得。

## 節點版本 {#node-versions}

前端建置環境支援下列Node.js版本。

* 12
* 14 （預設）
* 16
* 18

您可以使用`NODE_VERSION` [環境變數](/help/implementing/cloud-manager/environment-variables.md)來設定所要的版本。

## 真實的單一Source {#single-source-of-truth}

一般的良好做法是維護部署至AEM的單一信任來源。 Cloud Manager的目標是讓該單一真實來源變得顯而易見。 但是，由於前端管道允許將部分代碼的位置解耦，因此前端管道的正確設定需承擔一些額外的責任。 必須注意不要建立多個前端管道來部署到相同環境中的相同網站。

因此，特別是當建立了幾個前端管道時，建議保持如以下的系統化命名慣例：

* 前端模組的名稱（由`package.json`檔案的`name`屬性定義）應包含其套用的網站名稱。 例如，對於位於`/content/wknd`的網站，前端模組的名稱會類似`wknd-theme`。
* 當前端模組與其他模組共用相同的Git存放庫時，其資料夾名稱應等於或包含前端模組的相同名稱。 例如，如果前端模組名為`wknd-theme`，則封入資料夾名稱會類似`wknd-theme-sources`。
* Cloud Manager前端管道的名稱也應包含前端模組的名稱，也應新增其部署的環境（生產或開發）。 例如，對於名為`wknd-theme`的前端模組，管道的名稱可能類似於`wknd-theme-prod`。

此慣例應有效防止下列部署錯誤：

* 將前端模組套用至錯誤的網站
* 建立多個套用相同網站的前端模組，這些模組會相互覆寫
* 為相同來源建立多個前端管道，這可能會導致競爭情況，無法保證部署順序

## 關注點分離 {#separation-of-concerns}

適用於任何關注點分離的另一個良好做法，是特別注意如何設計和管理分離關注點的合約。 在前端管道中，將該程式碼與其餘程式碼分隔的合約是網站轉譯的HTML和JSON。 如果該HTML和JSON保持穩定，則前端管道通過使前端團隊完全獨立來實現其最大價值。

目前沒有與前端管道同步執行完整棧疊管道的特定功能。 因此，當將前端開發與完整棧疊管道分離時，必須在分離這兩個關注領域的合約中格外小心。 該合約通常是Experience Manager呈現的HTML和/或JSON。 因此，該合約的變更必須在操作不同管道的團隊之間妥善規劃，以便他們同意如何排列對應變更的順序。

當需要對HTML和/或JSON輸出執行會影響這兩個關注領域的變更時，通常建議採取以下步驟。

1. 後端團隊會先使用新HTML和/或JSON輸出設定開發環境。
   1. 透過完整棧疊管道，他們部署轉譯新HTML和/或JSON輸出所需的程式碼。
   1. 如果這是前端團隊之前無權存取的環境，則必須執行以下步驟。
      1. URL：前端團隊必須知道該開發環境的URL。
      1. ACL：前端團隊必須獲得具有類似「貢獻者」許可權的本機AEM使用者。
      1. Git：前端團隊必須具有針對該開發環境的前端模組的個別Git位置。
         * 通常的做法是建立`dev`分支，這樣對開發環境所做的變更就可以輕鬆地合併回要部署到生產環境的`main`分支。
      1. 管道：前端團隊必須具有部署到開發環境的前端管道。 如前所述，該管道將部署通常位於`dev`分支中的前端模組。
1. 前端團隊接著會讓CSS和JS程式碼與舊輸出和新輸出搭配使用。
   1. 一如既往，在本機開發：
      1. 在前端模組內執行的`npx aem-site-theme-builder proxy`命令會啟動一個從AEM環境請求內容的Proxy伺服器，同時將前端模組的CSS和JS檔案取代為來自本機`dist`資料夾的檔案。
      1. 設定隱藏`.env`檔案中的`AEM_URL`變數，可控制本機Proxy伺服器使用內容的AEM環境。
      1. 因此，變更此`AEM_URL`的值可讓您在生產環境和開發環境之間切換，以調整CSS和JS，使其適合兩個環境。
      1. 它必須與呈現新輸出的開發環境以及呈現舊輸出的生產環境搭配使用。
   1. 前端工作是在更新的前端模組適用於兩個環境時完成，並部署至兩個環境。
1. 然後，後端團隊可以透過部署程式碼來更新生產環境，該程式碼會透過完整棧疊管道來呈現新HTML和/或JSON輸出。
1. 前端團隊可以接著清理他們的CSS和JS，並移除僅需要舊輸出的專案，透過前端管道將最後一次更新部署到生產環境。

## 其他資源 {#additional-resources}

* [網站主題](/help/sites-cloud/administering/site-creation/site-themes.md) — 瞭解如何使用AEM網站主題來自訂網站的樣式和設計。
* [AEM網站主題產生器](https://github.com/adobe/aem-site-theme-builder) -Adobe提供AEM網站主題產生器，作為建立新網站主題的一組指令碼。
