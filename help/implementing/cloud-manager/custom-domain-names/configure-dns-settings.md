---
title: '配置DNS設定 '
description: 配置DNS設定
exl-id: 6e294f0b-52cb-40dd-bc42-ddbcffdf5600
source-git-commit: 016954bc712a135886a6031deba05d92e7d5099c
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# 配置DNS設定 {#configure-dns}

在成功驗證和部署自定義域名後，您準備與DNS提供程式一起更新自定義域名的DNS記錄。 這樣，您的站點就可以為訪問者提供服務。 因此，通常在投入使用之前完成此活動。

>[!NOTE]
>您或組織中的相應人員必須能夠登錄或聯繫您的DNS提供商（您從其購買域的公司），並在DNS設定中進行更新。

為此，您必須確定是否必須將DNS設定配置為 `CNAME` 或Apex記錄將您的自定義域名指向Cloud Manager域名。 A `CNAME` 或者，一旦設定了記錄，則會將域的所有Internet通信路由到其指向的任何位置。 如果該位置未設定為為通信服務，則將發生中斷。 如果尚未測試，則內容中可能存在錯誤。 這就是為什麼在測試完成並客戶準備投入使用後始終執行此步驟的原因。

必須按下表所示完成以下步驟：

| 步驟 |  | 責任 | 了解更多 |
|--- |--- |--- |---|
| 添加SSL證書 | 添加SSL證書 | 客戶 | [添加SSL證書](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=en) |
| 域驗證 | 添加TXT記錄 | 客戶 | [添加TXT記錄](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-text-record.html?lang=en) |
| 查看域驗證狀態 |  | 客戶 |  |
|  | 狀態：域驗證失敗 | 客戶 | [正在檢查域名狀態](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
|  | 狀態：已驗證，部署失敗 | 聯繫Adobe代表 | [正在檢查域名狀態](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-domain-name-status.html?lang=en) |
| 通過添加CNAME或APEX記AEM錄添加指向as a Cloud Service的DNS記錄 | 配置DNS設定 | 客戶 | [配置DNS設定](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/configure-dns-settings.html?lang=en) |
| 檢查DNS記錄狀態 |  | 客戶 | [正在檢查DNS記錄狀態](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | 狀態：未檢測到DNS狀態 | 客戶 | [正在檢查DNS記錄狀態](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/check-dns-record-status.html?lang=en) |
|  | 狀態：DNS解析不正確 | 客戶 |  |


## CNAME記錄 {#cname-record}

以下各節將幫助您確定適合DNS配置的記錄類型。

規範名稱或 `CNAME` 記錄是將別名映射到真或規範域名的DNS記錄類型。 CNAME記錄通常用於映射子域，如 `www.example.com`  到承載該子域內容的域。

登錄到域註冊器並建立CNAME記錄，將自定義域名指向目標，如下所示：

| 名稱 | 自定義域名指向目標 |
|--- |--- |
| www.customdomain.com | cdn.adobeaemcloud.com |

## APEX唱片 {#apex-record}

頂點域是不包含子域（如example.com）的自定義域。 頂點域配置有 `A` 。 `ALIAS` 或 `ANAME` 通過DNS提供程式進行記錄。 Apex域必須指向特定的IP地址。

通過域提供程式將以下所有A記錄添加到域的DNS設定：

* `A RECORD`

* `A record for domain @ pointing to IP 151.101.3.10`

* `A record for domain @ pointing to IP 151.101.67.10`

* `A record for domain @ pointing to IP 151.101.131.10`

* `A record for domain @ pointing to IP 151.101.195.10`
