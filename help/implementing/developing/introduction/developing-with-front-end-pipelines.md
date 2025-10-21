---
title: 使用前端管道開發網站
description: 前端管道增強了開發人員的獨立性，並加快了開發流程。 本文概述前端建置流程的主要考量事項，以確保最佳效能和效率。
exl-id: 996fb39d-1bb1-4dda-a418-77cdf8b307c5
feature: Developing
role: Admin, Architect, Developer
recommendations: display, noCatalog
source-git-commit: 0a458616afad836efae27e67dbe145fc44bee968
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 0%

---


# 使用前端管道開發網站 {#developing-site-with-front-end-pipeline}

{{traditional-aem}}

[前端管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#front-end)賦予前端開發人員更大的獨立性，並大幅加快開發速度。 本文說明此程式的運作方式，並著重說明可幫助您充分運用此程式的關鍵考量。

>[!TIP]
>
>如果您尚不熟悉如何使用前端管道及其優點，請參閱[快速網站建立歷程](/help/journey-sites/quick-site/overview.md)指南。 它提供範例，說明如何快速部署新網站並自訂其主題，而不受後端開發的影響。

## 瞭解AEM Cloud Manager中的前端管道設定和建置流程 {#front-end-build-contract}

與[完整棧疊組建環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md)類似，前端管道有自己的環境。 開發人員可透過此管道獲得一些彈性，前提是他們遵循前端建置合約。

前端管道需要前端`Node.js`專案才能使用`build`指令碼指示詞來產生它所部署的組建。 這項需求之所以存在，是因為Cloud Manager使用命令`npm run build`來產生前端組建的可部署專案。

`dist`資料夾的結果內容是Cloud Manager最終部署的內容，並將其作為靜態檔案提供。 這些檔案由外部託管至AEM，但可透過已部署環境上的`/content/...` URL取得。

## 支援的Node.js版本 {#node-versions}

前端組建環境支援下列`Node.js`版本：

* 23
* 22
* 20
* 18
* 16
* 14 (預設)
* 12

您可以使用`NODE_VERSION` [環境變數](/help/implementing/cloud-manager/environment-variables.md)來設定所要的版本。

## 在AEM中命名和管理前端管道的最佳實務 {#single-source-of-truth}

AEM部署的最佳實務是維護單一、明確的信任來源。 Cloud Manager的設計目的是強化此原則。 但是，由於前端管道允許部分計畫碼解耦，因此正確的設定至關重要。 為避免衝突，請確保多個前端管道不會部署到同一環境中的同一站點。

因此，尤其是當建立了多個前端管道時，Adobe建議您保持系統的命名慣例。 您可以使用以下建議：

* 前端模組的名稱（由`name`檔案的`package.json`屬性定義）應包含其套用的網站名稱。 例如，對於位於`/content/wknd`的網站，前端模組的名稱會類似`wknd-theme`。
* 當前端模組與其他模組共用相同的Git存放庫時，其資料夾名稱應等於或包含前端模組的相同名稱。 例如，如果前端模組名為`wknd-theme`，則封入資料夾名稱會類似`wknd-theme-sources`。
* Cloud Manager前端管道的名稱也應包含前端模組的名稱，也應新增其部署的環境（生產或開發）。 例如，對於名為`wknd-theme`的前端模組，管道的名稱可能類似於`wknd-theme-prod`。

此慣例可防止下列部署錯誤：

* 將前端模組套用至錯誤的網站。
* 建立多個套用相同網站的前端模組，這些模組會相互覆寫。
* 為相同來源建立多個前端管道，這可能會導致競爭情況，無法保證部署順序。

## 協調AEM中的前端和後端開發以提高穩定性 {#separation-of-concerns}

任何分離關注點的主要最佳實務是仔細設計和管理定義兩者之間界限的合約。 在前端管道中，此合約是網站轉譯的HTML和JSON輸出。 維持此輸出的穩定性可確保前端管道提供最大的價值，讓前端團隊能夠獨立工作。

目前沒有內建功能可與前端管道同步執行完整棧疊管道。 因此，將前端開發與完整棧疊管道分隔開時，謹慎管理定義其界限的合約至關重要。 此合約通常包含Experience Manager呈現的HTML或JSON （或兩者）。 本合約的任何變更都應在管理不同管道的團隊之間謹慎協調，以確保順利轉換和更新順序的正確。

變更HTML或JSON輸出時，通常建議遵循下列步驟，尤其是當兩個區域都受到影響時。

1. 後端團隊會先使用新的HTML或JSON輸出設定開發環境。
   1. 透過完整棧疊管道，他們會部署轉譯新HTML或JSON輸出（或兩者）所需的程式碼。
   1. 如果這是前端團隊之前無權存取的環境，則必須執行以下步驟。
      1. URL：前端團隊必須知道該開發環境的URL。
      1. ACL：前端團隊必須獲得具有類似「貢獻者」許可權的本機AEM使用者。
      1. Git：前端團隊必須具有針對該開發環境的前端模組的個別Git位置。

         常見的作法是建立`dev`分支，以管理開發環境中所做的變更。 此作法可讓您更輕鬆地合併回`main`分支，以用於部署至生產環境。

      1. 管道：前端團隊必須具有部署到開發環境的前端管道。 如前所述，該管道將部署通常位於`dev`分支中的前端模組。
1. 前端團隊接著會讓CSS和JS程式碼與舊輸出和新輸出搭配使用。
   1. 如往常一樣，若要在本機開發，請執行下列動作：
      1. `npx aem-site-theme-builder proxy`命令會啟動從AEM環境擷取內容的Proxy伺服器。 它以本機`dist`資料夾中的那些檔案取代前端模組的CSS和JS檔案。
      1. 在隱藏的`AEM_URL`檔案中設定`.env`變數，可讓您控制本機Proxy伺服器使用內容的AEM環境。
      1. 因此，變更`AEM_URL`的值可讓您在生產與開發環境之間切換，以調整CSS和JS，使其同時適用於兩個環境。
      1. 它必須與呈現新輸出的開發環境以及呈現舊輸出的生產環境搭配使用。
   1. 前端工作是在更新的前端模組適用於兩個環境時完成，並部署至兩個環境。
1. 然後，後端團隊可以透過完整棧疊管道部署可呈現新HTML或JSON輸出（或兩者）的程式碼來更新生產環境。
1. 前端團隊可以清理其CSS和JS、移除僅用於舊輸出所需的元素，並使用前端管道將最終更新部署到生產環境。

## 其他資源 {#additional-resources}

* 瞭解如何使用AEM網站主題來自訂網站的樣式和設計。

  請參閱[網站主題](/help/sites-cloud/administering/site-creation/site-themes.md)。

* Adobe提供AEM網站主題產生器，作為一組用於建立新網站主題的指令碼。

  請參閱[AEM網站主題產生器](https://github.com/adobe/aem-site-theme-builder)



