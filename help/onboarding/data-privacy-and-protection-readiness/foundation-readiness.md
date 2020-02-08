---
title: 資料保護與資料隱私權法規- Adobe Experience Manager作為雲端服務基礎準備
description: '瞭解Adobe Experience Manager如何以雲端服務基礎的身分支援各種資料保護與資料隱私權規範；包括歐盟通用資料保護規則(GDPR)、加州消費者隱私法，以及如何在將新AEM實作為雲端服務專案時符合規定。 '
translation-type: tm+mt
source-git-commit: 2b7ee2b7b0ce351ed48aeb2f3135c947eafe7247

---


# Adobe Experience manager作為雲端服務基礎，為資料保護和資料隱私法規做好準備 {#aem-foundation-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>本檔案內容不構成法律咨詢，不代表法律咨詢。
>
>請洽詢貴公司的法律部門，以取得有關資料保護與資料隱私權法規的建議。

>[!NOTE]
>
>如需Adobe對隱私權問題之回應，以及這對您身為Adobe客戶意味著什麼的詳細資訊，請參 [閱Adobe的隱私權中心](https://www.adobe.com/privacy.html)。

## AEM Foundation資料隱私與保護支援 {#aem-foundation-data-privacy-and-protection-support}

在AEM Foundation層級，儲存的個人資料會保存在「使用者設定檔」中。 因此，本文的資訊主要涉及如何訪問和刪除用戶配置檔案，分別解決訪問和刪除請求。

## 訪問用戶配置檔案 {#accessing-a-user-profile}

### 手動步驟 {#manual-steps}

1. 開啟「使用者管理」主控台，方法是瀏覽至「工 **[!UICONTROL 具」-「安全性」-「使用者」]** ，或直接瀏覽至 `https://<serveraddress>:<serverport>/security/users.html`

<!--
   ![useradmin2](assets/useradmin2.png)
-->

1. 然後，在頁面頂端的搜尋列中輸入名稱，以搜尋有問題的使用者：

   ![搜尋帳戶](assets/dpp-foundation-01.png)

1. 最後，按一下使用者描述檔以開啟該描述檔，然後檢查「詳細資 **[!UICONTROL 訊]** 」標籤下。

   ![用戶配置檔案](assets/dpp-foundation-02.png)

### HTTP API {#http-api}

如前所述，Adobe提供API來存取使用者資料，以利自動化。 您可使用幾種API:

**UserProperties API**

```shell
curl -u user:password http://localhost:4502/libs/granite/security/search/profile.userproperties.json\?authId\=cavery
```

**Sling API**

**搜索用戶首頁：**

```xml
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

**正在檢索用戶資料：**

使用上述命令傳回之JSON裝載之home屬性的節點路徑：

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile.-1.json'
```

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profiles.-1.json'
```

## 禁用用戶並刪除關聯的配置檔案 {#disabling-a-user-and-deleting-the-associated-profiles}

### 禁用用戶 {#disable-user}

1. 開啟「使用者管理」主控台，並依上述說明搜尋相關使用者。
2. 將滑鼠指標暫留在使用者上，然後按一下選取圖示。 描述檔會變成灰色，表示已選取。

3. 按下上 **方功能表** 中的「停用」按鈕，以停用使用者：

   ![禁用帳戶](assets/dpp-foundation-03.png)

4. 最後，確認動作。

   然後，使用者介面會指出已停用使用者帳戶，方法是移除並新增鎖定至描述檔卡：

   ![已禁用帳戶](assets/dpp-foundation-04.png)

### 刪除用戶配置檔案資訊 {#delete-user-profile-information}

>[!NOTE]
>
> 對於AEM做為雲端服務，UI中沒有可刪除使用者設定檔的手動程式，因為無法存取CRXDE。

### HTTP API {#http-api-1}

以下過程使用命 `curl` 令行工具說明如何禁用具有預設位置 **[!UICONTROL 的用]**`userId` 戶並刪除其配置檔案。

**搜索用戶首頁：**

```shell
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

**禁用用戶：**

使用上述命令傳回之JSON裝載之home屬性的節點路徑：

```shell
curl -X POST -u user:password -FdisableUser="describe the reasons for disabling this user (Data Privacy in this case)" 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN.rw.userprops.html'
```

**刪除用戶配置檔案**

使用從帳戶探索命令傳回的JSON裝載首頁屬性中的節點路徑，以及已知的開箱外描述檔節點位置：

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```
