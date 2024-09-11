---
title: 檢查網域名稱狀態
description: 瞭解如何確認Cloud Manager已成功確認您的自訂網域名稱。
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 3ff7b76f7892269f6ca001ff2c079bc693c06d93
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 30%

---


# 檢查網域名稱狀態 {#check-status}

瞭解如何確認Cloud Manager已成功確認您的自訂網域名稱。

## 要求 {#requirements}

在Cloud Manager中檢查您的網域名稱狀態之前，請先滿足這些要求。

* 首先為您自訂網域新增TXT記錄，如檔案[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)中所述。

## 檢查自訂網域名稱的狀態 {#how-to}

您可以在Cloud Manager中判斷自訂網域名稱的狀態。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 從&#x200B;**概觀**&#x200B;頁面，瀏覽到&#x200B;**環境**&#x200B;畫面。

1. 按一下左側導覽面板中的&#x200B;**網域設定**。

1. 按一下網域名稱的&#x200B;**狀態**&#x200B;圖示。

狀態詳細資訊隨即顯示。 當顯示狀態&#x200B;**已驗證和部署網域**&#x200B;時，您的自訂網域即可使用。 檢視[下一節](#statuses)，以取得不同狀態及其含義的詳細資訊。

>[!NOTE]
>
>當您在&#x200B;**新增自訂網域**&#x200B;精靈的驗證步驟上選取&#x200B;**建立**&#x200B;時，Cloud Manager會在[將新的自訂網域名稱新增至Cloud Manager](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)時，自動觸發驗證。 對於後續驗證，您必須主動選擇狀態旁邊的再次驗證圖示。

## 驗證狀態 {#statuses}

Cloud Manager透過[TXT值](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)驗證網域擁有權，並顯示下列其中一個狀態訊息。

| 狀態 | 說明 |
| --- | --- |
| 網域驗證失敗 | TXT值遺失或偵測到錯誤。<br>請依照狀態訊息中提供的指示解決問題。 準備就緒後，必須選擇狀態旁邊的&#x200B;**再次驗證**&#x200B;圖示。 |
| 正在進行網域驗證 | 驗證進行中。<br>在您選取狀態旁邊的&#x200B;**再次驗證**&#x200B;圖示後，通常會看到此狀態。 由於 DNS 傳播延遲，DNS 驗證可能需要幾個小時才能完成。 |
| 已驗證 — 部署失敗 | TXT驗證成功，但CDN部署失敗。<br>若是這種情況，請聯絡您的Adobe代表。 |
| 網域已驗證和部署 | 此狀態代表您的自訂網域名稱隨時可使用。<br>此時，您的自訂網域名稱已準備好進行測試，並指向Cloud Manager網域名稱。 請參閱[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)以瞭解更多資訊。 |
| 刪除中 | 正在刪除自訂網域名稱。 |
| 無法刪除 | 刪除自訂網域名稱失敗，必須重試。<br>請參閱[管理自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)以瞭解更多資訊。 |


## 網域名稱錯誤 {#domain-error}

以下是一些常見的網域名稱驗證錯誤及其一般解析度。

### 未安裝網域錯誤 {#domain-not-installed}

此錯誤可能發生在 TXT 記錄的網域驗證期間，即使是您已檢查記錄已正確更新。

#### 錯誤原因 {#cause}

Fastly會將網域鎖定到首先註冊它的帳戶，而其他帳戶必須請求許可權以註冊子網域。 此外，Fastly 只會讓您將一個頂點網域和關聯的子網域指派給一個 Fastly 服務和帳戶。如果您有現有的Fastly帳戶，該帳戶連結了用於AEM Cloud Service網域的相同頂點和子網域，您會看到此錯誤。

#### 錯誤解決 {#resolution}

錯誤可依如下方式修正：

* 在 Cloud Manager 中安裝網域之前，從現有帳戶中移除頂點和子網域。

* 使用此選項可將頂點網域和所有子網域連結到 AEM as a Cloud Service Fastly 帳戶。如需詳細資訊，請參閱[在 Fastly 文件中使用網域](https://docs.fastly.com/en/guides/working-with-domains)。

* 如果您的Apex網域有AEM as a Cloud Service和非AEM網站的多個子網域需要連結到不同的Fastly帳戶，請嘗試在Cloud Manager中安裝網域。 此過程有助於管理不同Fastly帳戶之間的子網域連線。 如果網域安裝失敗，請建立Fastly的客戶支援票證，讓Adobe可以代表您跟進Fastly。

>[!TIP]
>
>與 Fastly 解決網域委派問題通常需要 1-2 個工作天。出於這個原因，強烈建議在上線日期之前安裝網域。

>[!NOTE]
>
>如果網域未成功安裝，請勿將網站 DNS 路由到 AEM as a Cloud Service IP。

## 自訂網域名稱的預先存在CDN設定 {#pre-existing-cdn}

如果您已經有自訂網域名稱的CDN設定，則會在&#x200B;**自訂網域名稱**&#x200B;和&#x200B;**環境**&#x200B;頁面上顯示資訊訊息。 它鼓勵您透過UI新增這些設定，以便在Cloud Manager中管理和檢視這些設定。

使用UI移轉所有預先存在的環境設定後，該訊息就會消失。 訊息可能需要 1-2 個工作日才能消失。

如需詳細資訊，請參閱[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。

## 後續步驟 {#next-steps}

在Cloud Manager中驗證網域狀態後，請新增指向AEM as a Cloud Service的DNS、CNAME或APEX記錄來設定DNS設定。 繼續檔案[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)以繼續設定您的自訂網域名稱。
