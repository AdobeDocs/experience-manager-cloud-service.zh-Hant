---
title: 建立計畫
description: 了解如何設定新計畫和管道以部署附加元件。
exl-id: 06287618-0328-40b1-bba8-84002283f23f
source-git-commit: d67c5c9baafb9b7478f1d1c2ad924f5a8250a1ee
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 11%

---


# 建立計畫 {#creating-a-program}

了解如何設定新計畫和管道以部署附加元件。

## 到目前為止 {#story-so-far}

在Adobe Experience Manager (AEM)參考示範附加元件歷程的上一個檔案中， [瞭解參考示範附加元件安裝，](installation.md) 您已瞭解參考示範附加元件的安裝程式如何運作，說明不同部分如何共同運作。 您現在應該：

* 基本瞭解Cloud Manager。
* 瞭解管道如何將內容和設定傳送至AEM。
* 瞭解範本如何按幾下即可建立已預先填入示範內容的網站。

本文基於這些基礎之上，並執行第一個設定步驟來建立方案以進行測試，並使用管道來部署附加內容。

## 目標 {#objective}

本檔案可協助您瞭解如何設定新方案和管道以部署附加元件。 閱讀本檔案後，您應該能夠執行下列操作：

* 瞭解並解釋如何使用Cloud Manager建立計畫。
* 啟用新方案的參考示範附加元件。
* 執行管道，以便部署附加內容。

## 建立計畫 {#create-program}

登入Cloud Manager後，您可以建立沙箱程式用於測試和示範目的。

>[!NOTE]
>
>您的使用者必須是 **企業所有者** 在您組織的Cloud Manager中角色以建立計畫。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Adobe Cloud Manager。

1. 登入後，在畫面的右上角檢視組織，確保您在正確的組織。 如果您只是一個組織的成員，則不需要執行此步驟。

   ![Cloud Manager總覽](assets/cloud-manager.png)

1. 點選或按一下 **新增計畫** 在視窗的右上角。

1. 在 **讓我們建立您的程式** 對話方塊：

   1. 提供 **計畫名稱** 描述您的程式。
   1. 點選或按一下 **設定沙箱** 針對您的 **程式目標**
   1. 點選或按一下&#x200B;**繼續**。

   ![建立方案對話方塊](assets/create-program.png)

1. 在 **設定您的沙箱** 對話方塊 **解決方案和附加元件** 表格，展開 **網站** 點選或按一下以進入清單，然後核取 **參考示範**.

   * 如果您也想要建立AEM Screens的示範，請核取 **Screens** 選項時，才會考量此變數。 點選或按一下 **更新**.

   ![在方案設定中選取參考示範的附加元件](assets/select-reference-demo-add-on.png)


1. 點選或按一下 **建立** 並且Cloud Manager開始設定您的沙箱計畫。 您會進入計畫總覽畫面，而簡短的橫幅通知會指出流程已開始。 卡片已新增到新計畫的總覽頁面。 安裝程式需要幾分鐘才能完成。

1. 設定完成後，概覽頁面上的環境卡片會將其狀態顯示為 **就緒**. 點選或按一下卡片，這樣您就可以開啟環境。

   ![程式建立完成](assets/ready.png)

1. 您的環境已準備就緒，現在附加元件已作為一個選項啟用，但示範的內容必須部署到AEM才能使用。 若要這麼做，請點選或按一下中「部署至開發」管道旁的省略符號按鈕 **管道** 卡片並選取 **執行**.

   ![啟動](assets/run.png)

1. 管道隨即啟動，您將進入詳細說明部署進度的頁面。 您可以在建立計畫時離開此畫面瀏覽，並稍後返回（如有必要）。

   ![部署](assets/deployment.png)

管道可能需要幾分鐘才能完成。 完成後，即可在AEM編寫環境中使用附加元件及其示範內容。

## 下一步 {#what-is-next}

現在您已完成AEM參考示範附加元件歷程的這一部分，您應：

* 瞭解如何使用Cloud Manager建立計畫。
* 瞭解如何啟動計畫的參考示範附加元件。
* 能夠執行管道，因此您可以部署附加內容。

在此基礎上繼續您的AEM參考示範附加元件歷程，接著檢閱 [建立示範網站](create-site.md). 在那裡，您將瞭解如何根據管道部署的預先設定範本資料庫在AEM中建立示範網站。

## 其他資源 {#additional-resources}

* [Cloud Manager 文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/onboarding-concepts/cloud-manager-introduction.html) - 如果您想要 Cloud Manager 功能的更多詳細資訊，您可能想要直接查閱深入的技術文件。
