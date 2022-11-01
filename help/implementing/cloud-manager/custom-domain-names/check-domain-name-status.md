---
title: 檢查網域名稱狀態
description: 了解如何確定您的自訂網域名稱是否已透過 Cloud Manager 成功驗證。
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: d22d657361ea6c4885babd76e6b4c10f88378994
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 71%

---


# 檢查網域名稱狀態 {#check-status}

您可以在 Cloud Manager 中確定自訂網域名稱的狀態。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。

1. 從&#x200B;**總覽**&#x200B;頁面瀏覽到&#x200B;**環境**&#x200B;畫面。

1. 在左側瀏覽面板中按一下&#x200B;**網域設定**。

1. 按一下網域名稱的&#x200B;**狀態**&#x200B;圖示。

Cloud Manager 將透過 TXT 值驗證網路擁有權，並顯示以下其中一個狀態訊息。

* **網域驗證失敗** - TXT 值缺失或偵測到錯誤。

   * 按照提供的說明解決問題。
   * 準備就緒後，必須選擇狀態旁邊的&#x200B;**再次驗證**&#x200B;圖示。

* **正在進行網域驗證** - 正在進行驗證。

   * 選擇狀態旁邊的&#x200B;**再次驗證**&#x200B;圖示後，通常會看到此狀態。

* **已透過驗證，部署失敗** - TXT 驗證成功，但 CDN 部署失敗。

   * 如果遇到這種情況，請聯絡您的 Adobe 代表。

* **已驗證和部署網域** - 此狀態代表您的自訂網域名稱隨時可使用。

   * 此時，您的自訂網域名稱名已可進行測試，並指向 Cloud Manager 網域名稱。
   * 如需了解詳細資訊，請參閱文件：[設定 DNS 設定](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md)。

* **正在刪除** - 正在刪除自訂網域名稱。

* **刪除失敗** - 自訂網域名稱刪除失敗，必須重試。

   * 如需了解詳細資訊，請參閱文件：[管理自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)。

當您在&#x200B;**新增自訂網域**&#x200B;精靈的驗證步驟中選擇&#x200B;**儲存**&#x200B;時，Cloud Manager 將自動觸發 TXT 驗證。對於後續驗證，您必須主動選擇狀態旁邊的再次驗證圖示。

## 網域名稱錯誤 {#domain-error}

以下是常見的網域名稱錯誤及其典型解析度。

### 未安裝域錯誤 {#domain-not-installed}

即使您已檢查記錄是否已適當更新，在TXT記錄的網域驗證期間仍可能發生此錯誤。

#### 錯誤原因 {#cause}

以快速方式將域鎖定到註冊該域的初始帳戶，而沒有其他帳戶可以在未請求權限的情況下註冊子域。 此外，Fastly 只允許您將一個頂點網域和關聯的子網域指派給一個 Fastly 服務和帳戶。如果您有現有的 Fastly 帳戶，該帳戶連結了用於 AEM Cloud Service 網域的相同頂點和子網域，您將看到此錯誤。

#### 錯誤解決 {#resolution}

錯誤已修正如下：

* 在 Cloud Manager 中安裝網域之前，從現有帳戶中移除頂點和子網域。

* 使用此選項可將頂點網域和所有子網域連結到 AEM as a Cloud Service Fastly 帳戶。如需詳細資訊，請參閱[在 Fastly 文件中使用網域](https://docs.fastly.com/en/guides/working-with-domains)。

* 如果您的Apex網域有多個子網域，供您要連結至不同Abply帳戶的AEMas a Cloud Service和非AEMas a Cloud Service網站之用，請嘗試在Cloud Manager中安裝網域。 如果域安裝失敗，請使用Ampley建立「客戶支援」票證，以便Adobe可以代表您跟進Amply。

>[!TIP]
>
>使用Ampley解決網域委派問題通常需要1至2個工作天。 因此，強烈建議您在網域上線日期之前先安裝網域。

>[!NOTE]
>
>如果未成功安裝網域，請勿將網站的DNS路由至AEMas a Cloud ServiceIP。

## 自訂網域名稱的現有CDN設定 {#pre-existing-cdn}

如果您有自訂網域名稱的預先存在 CDN 設定，則&#x200B;**自訂網域名稱**&#x200B;和&#x200B;**環境**&#x200B;頁面上將顯示一則資訊訊息，鼓勵您透過 UI 新增這些設定，以便在 Cloud Manager 中顯示和設定它們。

使用 UI 移轉所有預先存在的環境設定後，該訊息就會消失。訊息可能需要 1-2 個工作日才能消失。

如需了解詳細資訊，請參閱文件：[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。
