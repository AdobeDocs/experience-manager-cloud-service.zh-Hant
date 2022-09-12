---
title: 檢查域名狀態
description: 了解如何判斷自訂網域名稱是否已由Cloud Manager成功驗證。
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: ba0226b5ad3852dd5f72dd7e0ace650035f5ac6a
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---


# 檢查域名狀態 {#check-status}

您可以決定Cloud Manager中自訂網域名稱的狀態。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇適當的組織和方案。

1. 導覽至 **環境** 螢幕 **概述** 頁面。

1. 按一下 **網域設定** ，即可取得Advertising Cloud的說明。

1. 按一下 **狀態** 表徵圖。

Cloud Manager會透過TXT值驗證網域擁有權，並顯示下列其中一個狀態訊息。

* **域驗證失敗** - TXT值缺失或檢測到錯誤。

   * 按照提供的說明解決問題。
   * 準備就緒時，您必須選取 **再次驗證** 表徵圖。

* **正在進行域驗證**  — 正在進行核查。

   * 此狀態通常會在您選取 **再次驗證** 表徵圖。

* **已驗證，部署失敗** - TXT驗證成功，但CDN部署失敗。

   * 在這種情況下，請連絡您的Adobe代表。

* **域已驗證並部署**  — 此狀態表示您的自定義域名已準備就緒，可供使用。

   * 此時，您的自訂網域名稱已準備好進行測試，並指向Cloud Manager網域名稱。
   * 請參閱該文檔 [配置DNS設定](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) 了解更多。

* **刪除**  — 正在刪除自定義域名。

* **刪除失敗**  — 刪除自定義域名失敗，必須重試。

   * 請參閱該文檔 [管理自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) 了解更多。

當您選取 **儲存** 在 **新增自訂網域** 嚮導。 對於後續驗證，您必須再次主動選取狀態旁的驗證圖示。

## 域名錯誤 {#domain-error}

本節說明您可能看到的錯誤，以及如何解決這些錯誤。

**未安裝域**  — 在TXT記錄的域驗證期間，您會收到此錯誤，即使您已檢查記錄是否已適當更新。

**錯誤說明**  — 將域快速鎖定到註冊了該域的初始帳戶，任何其他帳戶都不能在未請求權限的情況下註冊子域。 此外，Abmetly僅允許您將一個頂點域和關聯的子域分配給一個Abmett服務和帳戶。 如果您有一個現有的Ampley帳戶，該帳戶會連結您AEM Cloud Service網域所使用的相同頂點和子網域，您就會看到此錯誤。

**錯誤解決**  — 錯誤已修正如下：

* 在Cloud Manager中安裝網域之前，請先從現有帳戶中移除頂點和子網域。 使用此選項可將頂點域和所有子網域連結到AEMas a Cloud ServiceAbmey帳戶。 請參閱 [在「快速」檔案中使用網域](https://docs.fastly.com/en/guides/working-with-domains) 以取得其他詳細資訊。

* 如果您的Apex網域有多個子網域，供您連結至不同的AEMas a Cloud Service和非AEMas a Cloud Service網站，請嘗試在Cloud Manager中安裝網域，如果網域安裝失敗，請建立「Abpley」（快速）的客戶支援票證，以便我們能代表您追蹤Appliet。

>[!NOTE]
>
>注意：如果未成功安裝網域，請勿將網站的DNS路由至AEMas a Cloud ServiceIP。

## 自訂網域名稱的現有CDN設定 {#pre-existing-cdn}

如果您的自訂網域名稱已有CDN設定，系統會在 **自訂網域名稱** 和 **環境** 頁面，鼓勵您透過UI新增這些設定，以便在Cloud Manager中顯示和設定這些設定。

使用UI移轉所有預先存在的環境設定後，訊息會消失。 訊息可能需要1到2個工作天才會消失。

請參閱該文檔 [新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) 以取得更多詳細資訊。
