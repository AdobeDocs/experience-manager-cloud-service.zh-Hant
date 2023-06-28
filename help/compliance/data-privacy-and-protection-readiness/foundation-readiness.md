---
title: 資料保護和資料隱私權法規 - Adobe Experience Manager as a Cloud Service 基礎整備
description: 瞭解Adobe Experience Manager as a Cloud Service Foundation對各種資料保護和資料隱私權法規的支援。 本文包含歐盟一般資料保護規範(GDPR)、加州消費者隱私法，以及實作新的AEMas a Cloud Service專案時如何遵守。
exl-id: 3a4b9d00-297d-4b1d-ae57-e75fbd5c490c
source-git-commit: 92c123817a654d0103d0f7b8e457489d9e82c2ce
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 資料保護和資料隱私權法規的 Adobe Experience Manager as a Cloud Service 基礎整備 {#aem-foundation-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本文件的內容並不構成法律建議，其宗旨並非取代專業的法律建議。
>
>如需資料保護與資料隱私權法規的相關建議，請洽詢貴公司的法律部門。

>[!NOTE]
>
>如需有關Adobe對隱私權問題的回應，以及這對於您身為Adobe客戶所代表之意義的詳細資訊，請參閱 [Adobe隱私權中心](https://www.adobe.com/tw/privacy.html).

## AEM Foundation 資料隱私權和保護支援 {#aem-foundation-data-privacy-and-protection-support}

在 AEM Foundation 層級，儲存的個人資料會保存在使用者個人資料中。 因此，本文中的資訊主要說明如何存取和刪除使用者設定檔，以便您可以分別說明存取和刪除請求。

## 存取使用者個人資料 {#accessing-a-user-profile}

### 手動步驟 {#manual-steps}

1. 瀏覽至「**[!UICONTROL 工具 - 安全性 - 使用者]**」或者直接瀏覽至`https://<serveraddress>:<serverport>/security/users.html` 來開啟「使用者管理」主控台

<!--
   ![useradmin2](assets/useradmin2.png)
-->

1. 然後，透過在頁面最上方的搜尋列中輸入名稱來搜尋相關使用者：

   ![搜尋帳戶](assets/dpp-foundation-01.png)

1. 最後，透過按一下使用者個人資料以將其開啟，然後檢查「**[!UICONTROL 詳細資料]**」標籤下方。

   ![使用者個人資料](assets/dpp-foundation-02.png)

### HTTP API {#http-api}

如前所述，Adobe提供用於存取使用者資料的API，以促進自動化。 有多種類型的 API 可供您使用：

**UserProperties API**

```shell
curl -u user:password http://localhost:4502/libs/granite/security/search/profile.userproperties.json\?authId\=cavery
```

**Sling API**

**探索使用者首頁：**

```xml
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

**擷取使用者資料：**

使用上述命令傳回的 JSON 承載的 home 屬性中的節點路徑：

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile.-1.json'
```

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profiles.-1.json'
```

## 停用使用者並刪除相關聯的個人資料 {#disabling-a-user-and-deleting-the-associated-profiles}

### 停用使用者 {#disable-user}

1. 如上所述，開啟「使用者管理」主控台並搜尋相關使用者。
2. 將滑鼠停留在使用者上，並按一下選取圖示。 設定檔會變成灰色，表示已選取它。

3. 在上層功能表中，按一下 **停用** 若要停用（關閉）使用者：

   ![停用帳戶](assets/dpp-foundation-03.png)

4. 最後，確認動作。

   使用者介面會將設定檔卡片變灰並新增鎖定，藉此指出使用者帳戶已停用：

   ![帳戶已停用](assets/dpp-foundation-04.png)

### 刪除使用者個人資料資訊 {#delete-user-profile-information}

>[!NOTE]
>
>對於AEMas a Cloud Service，由於無法存取CRXDE，因此UI中沒有可用的手動程式來刪除使用者設定檔。

### HTTP API {#http-api-1}

下列程式使用 `curl` 命令列工具，說明如何使用 **[!UICONTROL cavery]** `userId` 並刪除預設位置可用的使用者設定檔。

**探索使用者首頁：**

```shell
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

**停用使用者：**

使用上述命令傳回的 JSON 承載的 home 屬性中的節點路徑：

```shell
curl -X POST -u user:password -FdisableUser="describe the reasons for disabling this user (Data Privacy in this case)" 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN.rw.userprops.html'
```

**刪除使用者設定檔**

使用從帳戶探索命令傳回的 JSON 承載的 home 屬性的節點路徑和已知的現成個人資料節點位置：

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```
