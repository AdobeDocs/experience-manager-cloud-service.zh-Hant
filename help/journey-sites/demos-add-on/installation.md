---
title: 了解參考示範附加元件安裝
description: 了解Cloud Manager及其如何用來安裝附加元件。
exl-id: 9418aac6-a8c4-43f7-b329-b02149fe2d53
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---

# 了解參考示範附加元件安裝 {#understand-installation}

了解Cloud Manager及其如何用來安裝附加元件。

>[!TIP]
>
>如果您已熟悉Cloud Manager，或想直接跳至設定及使用附加元件，可跳至 [建立方案和管道](create-program.md)
>
>如果您想要了解Cloud Manager和AEM如何合作以建立您的示範環境，以及如何設定和使用您自己的環境，請繼續閱讀目前的檔案。

## 目標 {#objective}

本文檔可幫助您了解「參考演示」附加元件的安裝過程如何工作，並說明不同元件如何協同工作。 閱讀後，您應：

* 對Cloud Manager有基本的了解。
* 了解管道如何將內容和設定傳送至AEM。
* 了解範本如何只按幾下，就能建立預先填入示範內容的新網站。

本檔案著重於了解AEM參考示範附加元件的這些基本部分，然後再繼續進行您開始安裝的歷程的下一個步驟。

雖然建議您逐步完成此歷程，但如果您已熟悉Cloud Manager，或想直接跳至設定及使用附加元件，您可跳至 [建立方案和管道](create-program.md)

## 負責角色 {#responsible-role}

此歷程適用於身為 **業務負責人** 角色。

## 需求與必要條件 {#requirements-prerequisites}

了解和開始使用「參考演示」附加元件的要求最低。

### 知識 {#knowledge}

* Cloud Manager基本知識

### 工具 {#tools}

* 成為 **業務負責人** 在Cloud Manager中為貴組織扮演的角色

## 了解Cloud Manager {#cloud-manager}

Cloud Manager是AEMas a Cloud Service的必要元件，是平台的單一進入點。

Cloud Manager用於管理支援您的AEM專案的雲端資源，包括所需的環境和工具。 就本歷程而言，您不需要完全了解Cloud Manager。 但您必須熟悉一些基本概念。

>[!TIP]
>
>如果您想深入了解Cloud Manager，請參閱 [其他資源](#additional-resources) 本文章的章節，以取得詳細資訊的連結。

### 計劃 {#programs}

當您登入Cloud Manager時，可以存取一或多個 **方案**. 方案可以以多種不同的方式定義，但最簡單的做法是，將它視為與單一品牌識別相關聯的網站和體驗。

如果您登入Cloud Manager，代表 **WKND旅遊和探險企業**，您可以建立 **WKND夜生活** 方案和 **WKND後院項目** 程式。 這兩個方案都會有AEM環境，可管理其相關網站。

### 沙箱 {#sandboxes}

方案可以是生產方案或沙箱方案。

* **生產計畫** 會建立，當您的程式準備上線時，最終允許即時流量。
* **沙箱方案** 為培訓、運行演示、培訓、POC等而建立 且不適用於即時流量。

若要安裝AEM參考示範附加元件，您需要建立新的沙箱方案。

>[!NOTE]
>
>AEM參考示範附加元件僅適用於沙箱方案。

## 安裝和使用流程 {#installation-flow}

現在您已了解Cloud Manager的一些基本概念，安裝AEM參考示範附加元件在概念上相當簡單。

1. 登入Cloud Manager。
1. 建立新的沙箱AEM方案，將AEM參考示範附加元件啟用為方案的選項。
1. 演示內容和配置已部署到程式中。 示範內容包含：
   * 使用AEM功能建立各種AEM網站的網站範本，已預先填入最佳實務範例。
   * 管理示範內容的設定工具。
1. 登入您新沙箱方案的AEM，使用快速網站建立工具，並根據範本建立示範網站。
1. 使用設定工具來管理這些示範網站和範本，包括在不再需要時刪除示範網站和範本。

## AEM網站範本 {#site-templates}

AEM網站範本是包含網站預先定義內容和結構的套件。 可自訂網站範本，以符合特定專案的需求，因此當AEM管理員建立新網站時，可以選擇適用於其業務案例的範本。

AEM參考示範附加元件包含多個範本，以滿足各種測試和示範需求。 建立程式並部署管道以安裝附加元件後，您就可以登入AEM，並根據許多示範範本建立網站

## 下一步 {#what-is-next}

現在您已完成AEM參考示範附加元件歷程的這一部分，您應：

* 對Cloud Manager有基本的了解。
* 了解管道如何將內容和設定傳送至AEM。
* 了解範本如何只按幾下，就能建立預先填入示範內容的新網站。

基於此知識，並透過接下來檢閱檔案，繼續建立AEM快速網站的歷程 [建立程式和管道，](create-program.md) 您將在這裡學習如何設定新程式和管道來部署附加元件。

## 其他資源 {#additional-resources}

建議您透過檢閱檔案，繼續進行快速網站建立歷程的下一個階段 [建立程式和管道，](create-program.md) 以下是一些額外的選用資源，可更深入探討本檔案中提及的一些概念，但您不需要這些資源即可繼續進行歷程。

* [了解方案和方案類型](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/understand-program-types.html)  — 從這裡開始了解即時方案和沙箱方案之間的差異。
* [網站範本](/help/sites-cloud/administering/site-creation/site-templates.md)  — 如果您想進一步了解網站範本的結構，以及如何使用範本建立網站，請參閱本檔案。
* [Cloud Manager檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html)  — 如果您想要取得Cloud Manager功能的詳細資訊，可直接參閱深入的技術檔案。
