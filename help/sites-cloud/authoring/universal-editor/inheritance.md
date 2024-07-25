---
title: 通用編輯器中的內容繼承
description: 瞭解通用編輯器如何支援多網站管理和啟動的內容繼承，以支援內容重複使用和本地化。
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 58c58243dc98a21161afe0976da4dcdc235da0d3
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 1%

---


# 通用編輯器中的內容繼承 {#inheritance}

瞭解通用編輯器如何支援多網站管理和啟動的內容繼承，以支援內容重複使用和本地化。

## 使用案例 {#use-case}

對AEM的許多使用者而言，建立頁面只是開始。 為了有效縮放內容，建立頁面後通常會涉及以下步驟：

1. **使用語言副本和翻譯工作流程來翻譯頁面**。
1. **使用多網站管理將頁面**&#x200B;當地語系化，以將翻譯的頁面轉出至不同的市場。
1. **使用[啟動]建立新版本**，以準備未來頁面的反複專案並讓這些變更上線。

這些步驟可以加快內容速度並確保內容一致性。 通用編輯器支援內容繼承，這是這些步驟所依賴的機制。

## 繼承 {#what-is-inheritance}

繼承是可連結內容的機制，如此一來變更一個會自動變更另一個。 繼承的元件可能是各種情況的產物，包括：

* [多網站管理(MSM)](/help/sites-cloud/administering/msm/overview.md)
* [啟動](/help/sites-cloud/authoring/launches/overview.md)

MSM和Launches是強大的工具，可協助您重複使用內容。 頁面可以從中央來源(Blueprint)複製，讓作者可以針對這些副本的內容進行特定變更，而其餘內容仍會從Blueprint繼承。 這在本地化網站時非常有用。

若要修改某些副本內容，作者會中斷受影響元件的繼承，以確保在副本與Blueprint同步時不會覆寫其本機變更。

## 內容繼承與通用編輯器 {#universal-editor}

當頁面是MSM或Launch的一部分，且內容是使用通用編輯器進行編輯時，編輯器會自動停用該頁面上作者所做所有變更的繼承，以確保在從Blueprint同步更新時保留修改的內容。

在進行本機編輯之前，作者不需要按一下按鈕或採取任何其他步驟來停用繼承。 進行變更後，繼承就會以隱含方式取消。 這與[頁面編輯器](/help/sites-cloud/authoring/page-editor/edit-content.md#inherited-components)相反。

## 限制 {#limitations}

* 作者無法還原單一元件的繼承。
   * 只能透過[即時副本總覽主控台](/help/sites-cloud/administering/msm/live-copy-overview.md)或[啟動主控台](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)，為整個頁面還原繼承。
* 作者沒有視覺化意見回饋，無法檢視哪些元件的繼承已停用，以及哪些元件的繼承仍會保留。
* 這些功能目前僅限於頁面中的元件，尚未套用至[內容片段](/help/sites-cloud/administering/content-fragments/overview.md)，儘管這些片段也具有MSM和Launch功能。
