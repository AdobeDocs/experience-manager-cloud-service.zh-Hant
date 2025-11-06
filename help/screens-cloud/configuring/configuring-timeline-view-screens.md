---
title: 設定AEM Screens的時間軸檢視
description: 本頁面說明如何在Screens as a Cloud Service中設定時間表檢視。
exl-id: 53afe1f5-8f0b-4cca-a819-d3e9375cbe37
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
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
評論為AEM使用者提供了一個良好的整合方式，讓他們得以討論可持續的方式，讓其他人瞭解關鍵決策。

1. 導覽至您要新增註解的管道。
1. 選取頻道。
1. 開啟&#x200B;**時間表**&#x200B;欄。
1. 新增您的註解並按&#x200B;**Enter**。

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
1. 開啟&#x200B;**時間表**&#x200B;欄。
1. 按一下頁面底部評論欄位旁的按鈕（三個點）。

   ![新增註解](/help/screens-cloud/assets/configure/screens-timeline5.jpg)

1. 選取&#x200B;**另存為版本**。
1. 輸入版本的&#x200B;**標籤**&#x200B;和&#x200B;**註解**。

   ![新增註解](/help/screens-cloud/assets/configure/screens-timeline6.jpg)

1. 選取&#x200B;**建立**&#x200B;以確認新版本。時間軸中的資訊會更新以指示新版本。

#### 還原為版本 {#revertversion}

若要將選取的頁面回覆成先前的版本：

1. 導覽至該管道以新增評論。
1. 選取頻道。
1. 開啟&#x200B;**時間表**&#x200B;欄。
1. 從篩選下拉式清單中選取&#x200B;**顯示全部**&#x200B;或&#x200B;**版本**。 會列出所選頻道的頻道版本。
1. 選取您想要還原到的版本。 可能的選項如下所示：

   ![新增註解](/help/screens-cloud/assets/configure/screens-timeline7.jpg)

1. 選取&#x200B;**還原為此版本**。 選取的版本會還原，且時間軸中的資訊會更新。

#### 預覽版本 {#previewversion}

您可以預覽特定版本：

1. 導覽至該管道以新增評論。
1. 選取頻道。
1. 開啟&#x200B;**時間表**&#x200B;欄。
1. 從篩選下拉式清單中選取&#x200B;**顯示全部**&#x200B;或&#x200B;**版本**。 會列出所選頻道的頻道版本。
1. 選取您要預覽的版本。 可能的選項如下所示：

   ![預覽版本](/help/screens-cloud/assets/configure/screens-timeline8.jpg)

1. 選取&#x200B;**預覽**。 此頻道會顯示在新的索引標籤中。

#### 比較版本與目前版本 {#compareversion}

您可以比較特定版本與目前版本：

1. 導覽至您要新增註解的管道。
1. 選取頻道。
1. 開啟&#x200B;**時間表**&#x200B;欄
1. 從篩選下拉式清單中選取&#x200B;**顯示全部**&#x200B;或&#x200B;**版本**。 會列出所選頻道的頻道版本。
1. 選取要比較的版本。 可能的選項如下所示：

   ![比較版本](/help/screens-cloud/assets/configure/screens-timeline9.jpg)

1. 選取&#x200B;**與目前**&#x200B;比較。 快顯視窗會開啟並顯示差異。

### 開始工作流程 {#workflowstart}

編寫時，您可以叫用工作流程以在管道上採取行動；也可以套用多個工作流程。
套用工作流程時，請指定下列資訊：

* 要套用的工作流程。
* （可選）有助於識別使用者收件匣中的工作流程例項的標題。
* 工作流程裝載。

#### 啟動工作流程

1. 導覽至您要新增註解的管道。
1. 選取頻道。
1. 開啟&#x200B;**時間表**&#x200B;欄。
1. 按一下底部評論欄位旁的按鈕（三個點）。

   ![開始工作流程](/help/screens-cloud/assets/configure/screens-timeline10.jpg)

1. 選取&#x200B;**啟動工作流程**。
1. 將會開啟「建立工作流程」精靈，以指定工作流程詳細資訊。
1. 從下拉式清單中選取&#x200B;**工作流程模型**，然後輸入工作流程標題。

   ![開始工作流程](/help/screens-cloud/assets/configure/screens-timeline11.jpg)

1. 按[下一步] **&#x200B;**&#x200B;繼續。
1. 在範圍步驟中，您可以：
   * **新增內容**&#x200B;以新增其他資源至工作流程。
   * **包含子項**&#x200B;以指定該資源的子項將包含在工作流程中。
   * **移除選取專案**&#x200B;以從工作流程移除該資源。

   ![開始工作流程](/help/screens-cloud/assets/configure/screens-timeline12.jpg)

1. 選取&#x200B;**建立**&#x200B;以關閉精靈並建立工作流程執行個體。
1. 根據所選的工作流程模型，您可能需要執行一些其他動作以完成工作流程。

   ![開始工作流程](/help/screens-cloud/assets/configure/screens-timeline13.jpg)
