---
title: 通用編輯器中的內容繼承
description: 瞭解通用編輯器如何支援多網站管理和啟動的內容繼承，以支援內容重複使用和本地化。
solution: Experience Manager Sites
feature: Authoring
role: User
exl-id: 2a1b87c2-29b9-4689-9a15-e17942439160
source-git-commit: 2099a1aecd30eaa2ca3ca33a13729817a30b6c3f
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 3%

---

# 通用編輯器中的內容繼承 {#inheritance}

瞭解通用編輯器如何支援多網站管理和啟動的內容繼承，以支援內容重複使用和本地化。

>[!NOTE]
>
>此功能僅適用於儲存在AEM存放庫中的內容。

## 使用案例 {#use-case}

對AEM的許多使用者而言，建立頁面只是開始。 為了有效縮放內容，建立頁面後通常會涉及以下步驟：

1. **使用語言副本和翻譯工作流程來翻譯頁面**。
1. **使用多網站管理將頁面**&#x200B;當地語系化，以將翻譯的頁面轉出至不同的市場。
1. **使用[啟動]建立新版本**，以準備未來頁面的反複專案並讓這些變更上線。

這些步驟可以加快內容速度並確保內容一致性。 Universal Editor支援內容繼承，這是複製、多網站管理和啟動所依賴的機制。

## 繼承 {#what-is-inheritance}

繼承是可連結內容的機制，如此一來變更一個會自動變更另一個。

MSM和Launches是功能強大的工具，可協助您使用繼承來重複使用內容。 頁面可以從中央來源(Blueprint)複製，讓作者可以針對這些副本的內容進行特定變更，而其餘內容仍會從Blueprint繼承。 這在本地化網站時非常有用。

若要修改某些副本內容，作者會中斷受影響元件的繼承，以確保在副本與Blueprint同步時不會覆寫其本機變更。

## 內容繼承與通用編輯器 {#universal-editor}

當頁面是MSM或Launch的一部分，且內容是使用通用編輯器進行編輯時，編輯器會自動停用該頁面上作者所做所有變更的繼承，以確保在從Blueprint同步更新時保留修改的內容。

在進行本機編輯之前，作者不需要按一下按鈕或採取任何其他步驟來停用繼承。 進行變更後，繼承就會以隱含方式取消。 此工作流程與[頁面編輯器](/help/sites-cloud/authoring/page-editor/edit-content.md#inherited-components)相反。

可透過以下方式還原整個頁面的繼承：

* [即時副本總覽主控台](/help/sites-cloud/administering/msm/live-copy-overview.md)
* [啟動主控台](/help/sites-cloud/authoring/launches/overview.md#the-launches-console)
* 使用&#x200B;**頁面屬性視窗**&#x200B;的&#x200B;**即時副本**&#x200B;索引標籤上的[重設](/help/sites-cloud/authoring/sites-console/page-properties.md)按鈕。

Universal Editor不會影響繼承的基礎機制。 如需繼承如何運作的詳細資訊，請參閱下列檔案。

* [多網站管理(MSM)](/help/sites-cloud/administering/msm/overview.md)
* [啟動](/help/sites-cloud/authoring/launches/overview.md)

### AEM Multi-Site-Management (MSM)擴充功能 {#msm-extension}

如果已安裝，**AEM Multi-Site-Management (MSM) Extension**&#x200B;會顯示所選元件的目前繼承狀態，並可讓您中斷或恢復元件層級的繼承。

請參閱[撰寫檔案以取得有關如何使用此擴充功能的詳細資訊。](/help/sites-cloud/authoring/universal-editor/authoring.md#inheritance)

如需如何啟用此擴充功能的詳細資訊，[請參閱Extension Manager檔案。](https://developer.adobe.com/uix/docs/extension-manager/feature-highlights/#enablingdisabling-extensions)

## 限制 {#limitations}

* 若要還原單一元件的繼承，必須啟用&#x200B;**AEM Multi-Site-Management (MSM) Extension**。
* 若要取得視覺化意見回饋，以檢視哪些元件的繼承已停用，以及哪些元件仍保留繼承，則必須啟用&#x200B;**AEM多網站管理(MSM)擴充功能**。
