---
title: 建立程式
description: 瞭解如何設定新程式和管道以部署載入項。
exl-id: 06287618-0328-40b1-bba8-84002283f23f
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# 建立程式 {#creating-a-program}

瞭解如何設定新程式和管道以部署載入項。

## 到目前為止的故事 {#story-so-far}

在參考演示附AEM加程式的上一文檔中， [瞭解參考演示附加程式安裝，](installation.md) 您瞭解了「參考演示」載入項的安裝過程如何工作，並演示了不同部分如何協同工作。 您現在應該：

* 對雲管理器有基本的瞭解。
* 瞭解管道如何將內容和配置傳送AEM到。
* 查看模板如何通過只需按一下幾下即可預先填充演示內容來建立新站點。

本文基於這些基礎知識，並採取第一個配置步驟建立用於測試的程式，並使用管道來部署附加內容。

## 目標 {#objective}

本文檔可幫助您瞭解如何設定新程式和管道以部署載入項。 閱讀完後，您應：

* 瞭解如何使用雲管理器建立新程式。
* 瞭解如何激活新程式的參考演示載入項。
* 能夠運行管道以部署附加內容。

## 建立程式 {#create-program}

登錄到Cloud Manager後，您可以建立新沙盒程式以用於測試和演示。

>[!NOTE]
>
>您的用戶必須是 **業務所有者** 在組織中的雲管理器中的角色，以便建立程式。

1. 登錄到Adobe雲管理器，位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)。

1. 登錄後，通過在螢幕右上角選中組織，確保您處於正確的組織中。 如果您只是一個組織的成員，則無需執行此步驟。

   ![雲管理器概述](assets/cloud-manager.png)

1. 點擊或按一下 **添加程式** 窗口右上角。

1. 在 **讓我們建立您的程式** 對話，確保 **Adobe Experience Manager** 在 **產品** 然後點擊，按一下 **繼續**。

   ![「建立程式」對話框](assets/create-program.png)

1. 在下一個對話框中：

   * 提供 **程式名稱** 來描述你的程式。
   * 點擊或按一下 **設定沙盒** 為 **計畫目標**

   然後點擊或按一下 **建立**。

   ![程式名稱](assets/program-name.png)

1. 您會進入程式概述螢幕，在螢幕中可以觀察程式的建立過程。 Cloud Manager提供剩餘時間的估計。 在建立程式時，您可以從此螢幕中導航，並在需要時稍後返回。

   ![程式建立](assets/program-creation.png)

1. 完成後，Cloud Manager將提供一個概述，包括自動建立的環境和管道。

   ![程式建立完成](assets/creation-complete.png)

1. 通過按一下頁面左上角的程式名並在下拉清單中選擇，編輯程式詳細資訊 **編輯程式**。

   ![編輯程式](assets/edit-program.png)

1. 在 **編輯程式** 對話框，切換到 **解決方案和附加模組** 頁籤。

   ![編輯程式對話框](assets/edit-program-dialog.png)

1. 在 **解決方案和附加模組** 的 **站點** 清單中的 **參考演示**。 如果還希望為AEM Screens建立演示，請檢查 **螢幕** 的雙曲餘切值。 點擊或按一下 **更新**。

   ![檢查參考演示選項](assets/edit-program-add-on.png)

1. 該載入項現在已作為選項啟用，但必須將其內容部署為AEM可用。 返回程式概述頁面，點擊或按一下 **開始** 啟動管道以將載入項內容部署到AEM。

   ![啟動](assets/deploy.png)

1. 管道將啟動，您將被帶到一個詳細描述部署進度的頁面。 在建立程式時，您可以從此螢幕中導航，並在需要時稍後返回。

   ![部署](assets/deployment.png)

管道完成後，該載入項及其演示內容可在創作環境中AEM使用。

## 下一步是什麼 {#what-is-next}

現在，您已完成了「參考演示附AEM加程式」的這一部分，您應：

* 瞭解如何使用雲管理器建立新程式。
* 瞭解如何激活新程式的參考演示載入項。
* 能夠運行管道以部署附加內容。

在此知識基礎上構建並繼AEM續您的參考演示附加程式，方法是下次查看文檔 [建立演示網站，](create-site.md) 其中，您將學習在中建立演示站AEM點，該演示站點基於管道部署的預配置模板庫。

## 其他資源 {#additional-resources}

* [Cloud Manager文檔](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html)  — 如果您想更詳細地瞭解Cloud Manager的功能，則可能需要直接查閱深入的技術文檔。
