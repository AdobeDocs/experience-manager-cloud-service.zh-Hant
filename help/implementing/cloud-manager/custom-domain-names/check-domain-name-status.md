---
title: 正在檢查域名狀態
description: 瞭解如何確定您的自定義域名是否已由雲管理器成功驗證。
exl-id: 8fdc8dda-7dbf-46b6-9fc6-d304ed377197
source-git-commit: ba0226b5ad3852dd5f72dd7e0ace650035f5ac6a
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---


# 正在檢查域名狀態 {#check-status}

您可以在雲管理器中確定自定義域名的狀態。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織和程式。

1. 導航到 **環境** 螢幕 **概述** 的子菜單。

1. 按一下 **域設定** 的子菜單。

1. 按一下 **狀態** 表徵圖。

Cloud Manager將通過TXT值驗證域所有權，並顯示以下狀態消息之一。

* **域驗證失敗** - TXT值丟失或檢測到有錯誤。

   * 按照提供的說明解決問題。
   * 準備好後，必須選擇 **再次驗證** 表徵圖。

* **正在進行域驗證**  — 正在進行核查。

   * 此狀態通常在您選擇 **再次驗證** 表徵圖。

* **已驗證，部署失敗** - TXT驗證成功，但CDN部署失敗。

   * 在此類情況下，請與您的Adobe代表聯繫。

* **域驗證和部署**  — 此狀態表示您的自定義域名已準備好使用。

   * 此時，您的自定義域名已準備好進行測試並指向Cloud Manager域名。
   * 請參閱文檔 [配置DNS設定](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) 來瞭解更多資訊。

* **刪除**  — 正在刪除自定義域名。

* **刪除失敗**  — 刪除自定義域名失敗，必須重試。

   * 請參閱文檔 [管理自定義域名](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md) 來瞭解更多資訊。

當您選擇時，Cloud Manager將自動觸發TXT驗證 **保存** 的驗證步驟 **添加自定義域** 的子菜單。 對於後續驗證，必須主動選擇狀態旁邊的再次驗證表徵圖。

## 域名錯誤 {#domain-error}

本部分說明您可能看到的錯誤以及如何解決這些錯誤。

**未安裝域**  — 在對TXT記錄進行域驗證時，即使您檢查了記錄是否已正確更新後，仍會收到此錯誤。

**錯誤解釋**  — 快速將域鎖定到註冊該域的初始帳戶，任何其他帳戶都不能在未請求許可的情況下註冊子域。 此外，Apxible只允許您將一個頂點域和關聯的子域指派給一個Apxible服務和帳戶。 如果您有一個現有的Reblish帳戶，該帳戶連結了用於您的AEM Cloud Service域的同一頂點和子域，您將看到此錯誤。

**錯誤解決**  — 錯誤已修復，如下所示：

* 在Cloud Manager中安裝域之前，請從現有帳戶中刪除頂點和子域。 使用此選項將頂域和所有子域連結到AEMas a Cloud ServiceRebish帳戶。 請參閱 [在「快速」文檔中使用域](https://docs.fastly.com/en/guides/working-with-domains) 的雙曲餘切值。

* 如果您的頂域有多個子域，用於您要連結到AEMas a Cloud Service和非as a Cloud Service站點的和非站點，請嘗試在Cloud Manager中安裝該域，如果域安裝失敗，則使用Appriest建立客戶支援票證，以便我們可以代表您跟蹤Apprist。

>[!NOTE]
>
>注：如果域未成功安裝，AEM請勿將站點的DNS路由到as a Cloud ServiceIP。

## 針對自定義域名的預先存在的CDN配置 {#pre-existing-cdn}

如果您的自定義域名具有預先存在的CDN配置，則在 **自定義域名** 和 **環境** 頁面，鼓勵您通過UI添加這些配置，以便它們在雲管理器中可見且可配置。

使用UI遷移所有預先存在的環境配置後，消息將消失。 消息可能需要1-2個工作日才能消失。

請參閱文檔 [添加自定義域名](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) 的子菜單。
