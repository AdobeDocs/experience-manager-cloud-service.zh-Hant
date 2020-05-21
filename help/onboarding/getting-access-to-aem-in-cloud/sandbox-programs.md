---
title: 沙盒程式——雲端服務
description: 沙盒程式——雲端服務
translation-type: tm+mt
source-git-commit: eb874176c71d7f3d03d953f7bae4cb3db2ffb3b9
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---


# 沙盒程式 {#sandbox-programs}

## 簡介 {#introduction}

沙盒程式是AEM Cloud Service中提供的兩種程式類型之一，另一種是一般程式。

建立沙盒通常是為了提供訓練、執行示範、啟用或POC的目的。 他們不是要載著現場交通的。

沙盒程式包括網站和資產，並會自動填入Git分支，其中包含范常式式碼、開發環境和非生產管道。

有關程式類型的詳細資訊，請參閱了 [解程式和程式類型](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/understand-program-types.html)。

### 沙盒程式的屬性 {#attributes-sandbox}

「沙盒程式」具有下列屬性：

1. **方案建立：** 建立沙盒程式包括自動：
   * 使用范常式式碼和內容設定專案
   * 開發環境的創造
   * 建立非生產性管道以部署至開發環境（主分支部署至開發環境）

1. **解決方案包括：** 沙盒程式包括網站和資產。

1. **AEM更新：** AEM更新可手動套用至沙盒程式中的環境，且不會自動推送。

1. **休眠：** 如果在某段時間內未偵測到任何活動，沙盒程式中的環境會自動休眠。 休眠的環境可以手動解除休眠。

### 建立沙盒程式 {#creating-sandbox-program}

程式建立嚮導將要求用戶提交詳細資訊。

有關如何建立沙盒程式的資訊，請參閱 [建立沙盒程式](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/creating-a-program.html#create-demo-program)。

### 建立沙盒環境 {#creating-sandbox-environments}

在程式建立時，將以自動建立的方式提供沙盒程式的開發環境。 依預設，開發環境會隨附作者和發佈層。

當使用者準備好設定生產管線時，可手動將生產階段環境集新增至沙盒程式。

有關如何手動建立環境的資訊，請參閱添加 [環境](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#adding-environments)。

### 刪除沙盒環境  {#deleting-sandbox-environments}

具備必要權限的使用者將可刪除開發或生產／階段環境／集。

有關如何刪除環境的資訊，請參閱刪 [除環境](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/using-cloud-manager/manage-environments.html#deleting-environment)。


## 冬眠和冬眠沙盒環境 {#hibernating-introduction}

執行程式環境在閒置一 *段時間後* ，將進入休眠模式。

>[!NOTE]
>休眠是沙盒程式環境的獨有功能。 常規方案環境不會休眠。

### 冬眠 {#hibernation-introduction}

休眠可以自動或手動進行。 要讓環境冬眠，可能需要幾分鐘的時間。 資料會在冬眠期間保留。

冬眠分為：

* **自動** 「沙盒」程式環境在閒置8小時後會自動休眠，這表示作者或發佈服務都不會收到要求。

* **手動**: 客戶可以手動休眠沙盒程式環境，但無需這樣做，因為休眠將在閒置一段時間後自動發生。

#### 使用手動休眠 {#using-manual-hibernation}


您可從開發人員主控台的兩個畫面中的任一畫面，完成手動休眠。

請依照下列步驟手動休眠您的程式環境：

1. 導覽至Developer Console。
1. 按一下「休眠」
1. 按一下「休眠」進行確認。
1. 冬眠成功後，您會看到下列畫面。
1. 在環境清單螢幕（如下圖所示）中，按一下環境詳細資訊螢幕中的「環境」連結即可訪問該螢幕，可以在所需環境行中按一下Hibernate按鈕。 然後會出現確認畫面。

### 解除休眠 {#de-hibernation-introduction}

>[!IMPORTANT]
>Admin Console中的「Cloud Manager - Developer Role」（雲端管理員——開發人員角色）定義了對Developer Console的存取。 有了這項權限，使用者就可以解除環境的休眠。

### 訪問休眠環境 {#accessing-hibernated-environment}

當針對休眠環境的作者或發佈層提出任何瀏覽器請求時，使用者會遇到一個描述該環境休眠狀態的登陸頁面，如下所示：

具有「雲端管理員——開發人員角色」的使用者可以按一下「開發人員主控台」按鈕，以存取開發人員主控台並解除環境休眠。 有關設定角色的資訊，請參閱Cloud Manager檔案。

如果組織中的使用者無法按一下「開發人員主控台」按鈕以進入「開發人員主控台」，則可能需要給予他們「雲端管理員——開發人員角色」。




## AEM對沙盒環境的更新 {#aem-updates-sandbox}


請參閱 [AEM版本更新](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/implementing/deploying/overview.html#version-updates)。

使用者可手動將AEM更新套用至沙盒程式中的環境（請參閱下圖）。 當顯示的狀態為「更新可用」時，即可執行此操作。 「Environments Card（環境卡）」上的下拉式選單將提供「Update（更新）」選項。 也可以從「環境」螢幕的「管理」菜單中選擇它。

>[!NOTE]
>必須配置部署到感興趣的開發環境的非生產管線，以便啟動手動更新管線。

>[!NOTE]
>必須配置生產管線，以便啟動對Production+Stage環境集的手動更新管線。

>[!NOTE]
>手動更新至生產環境或舞台環境會自動更新另一個環境。 Production+Stage環境集必須位於相同的AEM版本。





