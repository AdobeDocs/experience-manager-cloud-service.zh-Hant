---
title: 設定AEM Screens的時間軸檢視
description: 本頁面說明如何在Screensas a Cloud Service設定時間軸檢視。
source-git-commit: eb71ea3a1a739b08fb3154a5f41a0706bd81488c
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 1%

---

# 設定AEM Screens的時間軸檢視 {#configuring-timelineview-screens}

## 簡介 {#introduction}

本節說明如何建立AEM Screens的時間軸檢視。

AEM提供了一套功能，可讓組織中的多個群組人員在建立、管理和使用管道時進行共同作業。
時間軸位於左側列，會依時間順序描述頻道、位置或任何熒幕資料夾的生命週期，傳達其整個生命週期中發生的狀況。 這可以依型別篩選。
除了生命週期記錄外，時間軸邊欄還提供下列功能。

![將設定檔套用至資料夾](/help/screens-cloud/assets/configure/Screens-timeline1.jpg)

![將設定檔套用至資料夾](/help/screens-cloud/assets/configure/screens-timeline2.jpg)

若要建立AEM Screens的時間軸檢視，請完成下列步驟：

1. 新增留言
1. 儲存版本
1. 啟動工作流程

以下各節會詳細說明這些步驟。

### 新增註解 {#addcomment}

透過時間軸提供的註解可讓使用者為畫面中發生的頻道、位置或任何資料夾討論，建立集中和歷史記錄。
評論為AEM使用者提供了一個良好的整合方式，以討論可以持續存在的方式，讓其他人瞭解關鍵決策。

1. 導覽至您要新增註解的管道。
1. 選取頻道。
1. 開啟 **時間表** 欄。
1. 新增您的註解並按 **輸入**.

![新增註解](/help/screens-cloud/assets/configure/screen-timeline3.jpg)

時間軸中的資訊會更新，以指出已新增評論。

![新增註解](/help/screens-cloud/assets/configure/screens-timeline4.jpg)

### 儲存版本 {#saveversion}

版本設定功能會在特定時間點建立管道的「快照」。 使用版本設定，您可以執行下列動作：
* 建立頻道的版本。
* 將管道還原至先前的版本；例如：
   * 還原您對頁面所做的變更。
* 比較管道的目前版本與先前版本：
   * 以醒目提示頻道內容中的差異。


#### 建立新版本 {#createnewversion}

1. 導覽至您要新增註解的管道。
1. 選取頻道。
1. 開啟 **時間表** 欄。
1. 按一下頁面底部評論欄位旁的按鈕（三個點）。

   ![新增註解](/help/screens-cloud/assets/configure/screens-timeline5.jpg)

1. 選取 **另存為版本**.
1. 輸入 **標籤** 和 **註解** 適用於此版本。

   ![新增註解](/help/screens-cloud/assets/configure/screens-timeline6.jpg)

1. 透過選取以確認新版本 **建立**.時間軸中的資訊會更新以指示新版本。

#### 還原為版本 {#revertversion}

若要將選取的頁面回覆成先前的版本：

1. 導覽至該管道以新增評論。
1. 選取頻道。
1. 開啟 **時間表** 欄。
1. 選取 **全部顯示** 或 **版本** 篩選器下拉式清單中的。 會列出所選頻道的頻道版本。
1. 選取您想要還原到的版本。 可能的選項如下所示：

   ![新增註解](/help/screens-cloud/assets/configure/screens-timeline7.jpg)

1. 選取 **還原為此版本**. 選取的版本會還原，且時間軸中的資訊會更新。

#### 預覽版本 {#previewversion}

您可以預覽特定版本：

1. 導覽至該管道以新增評論。
1. 選取頻道。
1. 開啟 **時間表** 欄。
1. 選取 **全部顯示** 或 **版本** 篩選器下拉式清單中的。 會列出所選頻道的頻道版本。
1. 選取您要預覽的版本。 可能的選項如下所示：

   ![預覽版本](/help/screens-cloud/assets/configure/screens-timeline8.jpg)

1. 選取 **預覽**. 此頻道會顯示在新的索引標籤中。

#### 比較版本與目前版本 {#compareversion}

您可以比較特定版本與目前版本：

1. 導覽至您要新增註解的管道。
1. 選取頻道。
1. 開啟 **時間表** 欄
1. 選取 **全部顯示** 或 **版本** 篩選器下拉式清單中的。 會列出所選頻道的頻道版本。
1. 選取要比較的版本。 可能的選項如下所示：

   ![比較版本](/help/screens-cloud/assets/configure/screens-timeline9.jpg)

1. 選取 **與目前專案比較**. 快顯視窗會開啟並顯示差異。

### 開始工作流程 {#workflowstart}

編寫時，您可以叫用工作流程以在管道上採取行動；也可以套用多個工作流程。
套用工作流程時，請指定下列資訊：

* 要套用的工作流程。
* （可選）有助於識別使用者收件匣中的工作流程例項的標題。
* 工作流程裝載。

#### 啟動工作流程

1. 導覽至您要新增註解的管道。
1. 選取頻道。
1. 開啟 **時間表** 欄。
1. 按一下底部評論欄位旁的按鈕（三個點）。

   ![開始工作流程](/help/screens-cloud/assets/configure/screens-timeline10.jpg)

1. 選取 **開始工作流程**.
1. 將會開啟「建立工作流程」精靈，以指定工作流程詳細資訊。
1. 選取 **工作流程模型** 從下拉式清單中，輸入工作流程標題。

   ![開始工作流程](/help/screens-cloud/assets/configure/screens-timeline11.jpg)

1. 按一下「 」以繼續 **下一個**.
1. 在範圍步驟中，您可以：
   * **新增內容** 以新增其他資源至工作流程。
   * **包含子項** 以指定該資源的子項將包含在工作流程中。
   * **移除選取專案** 以從工作流程移除該資源。

   ![開始工作流程](/help/screens-cloud/assets/configure/screens-timeline12.jpg)

1. 選取 **建立** 以關閉精靈並建立工作流程例項。
1. 根據所選的工作流程模型，您可能需要執行一些其他動作以完成工作流程。

   ![開始工作流程](/help/screens-cloud/assets/configure/screens-timeline13.jpg)
