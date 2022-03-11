---
title: 資料保護和資料隱私法規 — Adobe Experience Manager as a Cloud Service基金會就緒性
description: 瞭解Adobe Experience Manager as a Cloud Service基金會對各種資料保護和資料隱私法規的支援；包括歐盟一般資料保護條例(GDPR)、加利福尼亞消費者隱私法以及實施新as a Cloud Service項目時如AEM何遵守。
exl-id: 3a4b9d00-297d-4b1d-ae57-e75fbd5c490c
source-git-commit: e4527b155179c50e1e423e7e835b3fcde3a4f2af
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 5%

---

# Adobe Experience Manager as a Cloud Service基金會為資料保護和資料隱私法規做好準備 {#aem-foundation-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本檔案的內容不構成法律咨詢，也不是作為法律咨詢的替代。
>
>有關資料保護和資料隱私法規的建議，請咨詢您公司的法律部門。

>[!NOTE]
>
>有關Adobe對隱私問題的響應以及這對您作為Adobe客戶意味著什麼的詳細資訊，請參閱 [Adobe隱私中心](https://www.adobe.com/privacy.html)。

## 基AEM礎資料隱私和保護支援 {#aem-foundation-data-privacy-and-protection-support}

在基AEM礎級別，儲存的個人資料保存在用戶配置檔案中。 因此，本文的資訊主要涉及如何訪問和刪除用戶配置檔案，分別處理訪問和刪除請求。

## 訪問用戶配置檔案 {#accessing-a-user-profile}

### 手動步驟 {#manual-steps}

1. 通過瀏覽以開啟用戶管理控制台 **[!UICONTROL 工具 — 安全性 — 用戶]** 或直接瀏覽 `https://<serveraddress>:<serverport>/security/users.html`

<!--
   ![useradmin2](assets/useradmin2.png)
-->

1. 然後，在頁面頂部的搜索欄中鍵入名稱以搜索有關的用戶：

   ![搜索帳戶](assets/dpp-foundation-01.png)

1. 最後，按一下用戶配置檔案，然後在 **[!UICONTROL 詳細資訊]** 頁籤。

   ![用戶配置檔案](assets/dpp-foundation-02.png)

### HTTP API {#http-api}

如前所述，Adobe提供用於訪問用戶資料的API，以便於自動化。 可以使用以下幾種類型的API:

**用戶屬性API**

```shell
curl -u user:password http://localhost:4502/libs/granite/security/search/profile.userproperties.json\?authId\=cavery
```

**Sling API**

**正在發現用戶主目錄：**

```xml
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

**正在檢索用戶資料：**

使用從以上命令返回的JSON負載的home屬性中的節點路徑：

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile.-1.json'
```

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profiles.-1.json'
```

## 禁用用戶並刪除關聯的配置檔案 {#disabling-a-user-and-deleting-the-associated-profiles}

### 禁用用戶 {#disable-user}

1. 開啟「用戶管理」控制台並搜索有關的用戶，如上所述。
2. 將滑鼠懸停在用戶上，然後按一下「選擇」表徵圖。 配置檔案將變為灰色，表示已選定。

3. 按 **禁用** 按鈕，禁用用戶：

   ![禁用帳戶](assets/dpp-foundation-03.png)

4. 最後，確認操作。

   然後，用戶介面將指示已通過擦除和向配置檔案卡添加鎖定來停用用戶帳戶：

   ![已禁用](assets/dpp-foundation-04.png)

### 刪除用戶配置檔案資訊 {#delete-user-profile-information}

>[!NOTE]
>
>對AEM於as a Cloud Service,UI中沒有可用於刪除用戶配置檔案的手動過程，因為CRXDE不可訪問。

### HTTP API {#http-api-1}

以下過程使用命 `curl` 令行工具說明如何禁用具有預設位置 **[!UICONTROL 的用]**`userId` 戶並刪除其配置檔案。

**正在發現用戶主目錄：**

```shell
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

**禁用用戶：**

使用從以上命令返回的JSON負載的home屬性中的節點路徑：

```shell
curl -X POST -u user:password -FdisableUser="describe the reasons for disabling this user (Data Privacy in this case)" 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN.rw.userprops.html'
```

**刪除用戶配置檔案**

使用從帳戶發現命令返回的JSON負載的home屬性中的節點路徑和已知的開箱配置檔案節點位置：

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```
