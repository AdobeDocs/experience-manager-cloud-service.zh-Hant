---
title: 自訂網域名稱簡介
description: Cloud Manager 的 UI 可讓您新增自訂網域，以自助服務方式使用唯一的品牌名稱識別您的網站。
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 41a67b0747ed665291631de4faa7fb7bb50aa9b9
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 45%

---


# 自訂網域名稱簡介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="管理自訂網域名稱"
>abstract="Cloud Manager 的 UI 可讓您新增自訂網域，以自助服務方式使用唯一的品牌名稱識別您的網站。"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name" text="新增自訂網域名稱"
>additional-url="https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/managing-custom-domain-names" text="檢視和更新自訂網域名稱"

Adobe Experience Manager as a Cloud Service已佈建預設網域名稱，結尾為 `*.adobeaemcloud.com`。您可以使用Cloud Manager的UI，新增自訂網域，以自助方式使用唯一的品牌名稱來識別您的網站。 即使您將自訂網域名稱與您的網站建立關聯，預設的`*.adobeaemcloud.com`網域名稱仍會保留。

## 什麼是自訂網域名稱？ {#what-are-custom-domain-names}

每個網站都有一個與之關聯的電腦可讀取的唯一數字位址，例如 `184.33.123.64`。網域名稱系統 (DNS) 可讓您將數字位址轉換為令人難忘的位址，以將自訂、品牌化網域附加至網站上，例如，`wknd.com`。

為您的網站命名網域名稱是很好的作法，這會讓客戶難忘並反映您的品牌。

您可以向網域名稱註冊機構、管理和銷售網域名稱的公司或組織購買網域名稱。網域名稱註冊機構管理 DNS 伺服器上的網域名稱。

>[!IMPORTANT]
>
>Cloud Manager 不是網域名稱註冊機構，不提供 DNS 服務。

## 自訂網域名稱並使用您自己的CDN {#byo-cdn}

AEM as a Cloud Service提供內建的CDN （內容傳遞網路）服務，也可讓您透過BYO （自攜）CDN搭配AEM使用。 自訂網域可以安裝在 AEM 管理的 CDN 或您管理的 CDN 中。

* Cloud Manager可管理安裝在AEM管理的CDN中的自訂網域名稱和憑證。
* BYO CDN中安裝的自訂網域名稱和憑證會直接在該CDN中管理。

**在您自己的CDN中管理的網域不需要透過Cloud Manager安裝** — 這些網域可透過X-Forwarded-Host供AEM使用，並且符合Dispatcher中定義的vhost。 請參閱 [CDN 文件](/help/implementing/dispatcher/cdn.md)。

在一個環境中，您可以將兩個網域安裝在AEM管理的CDN中，並將它們安裝在BYO CDN中。

## 工作流程 {#workflow}

新增自訂網域名稱需要 DNS 服務和 Cloud Manager 互動。由於此工作流程，安裝、設定和驗證自訂網域名稱需要執行數個步驟。 下表提供所需步驟的概觀，包括完成這些步驟的檔案資源連結。

| 步驟 | 說明 | 文件 |
| --- | --- | --- |
| 1 | 將 SSL 憑證新增到 Cloud Manager | [新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | 新增自訂網域至Cloud Manager | [新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) |
| 3 | 新增指向 AEM as a Cloud Service 的 DNS CNAME 或 Apex 記錄，以設定 DNS 設定 | [新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) |
| 4 | 檢閱網域驗證狀態 | [檢查網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 5 | 檢查 DNS 記錄狀態 | [檢查DNS記錄狀態](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |

>[!TIP]
>
>使用 AEM as a Cloud service 設定自訂網域名稱通常是一個簡單的過程。但是，有時可能會發生網域委派問題，這可能需要1-2個工作日才能解決。 因此，建議您在上線日期之前安裝網域。 如需詳細資訊，請參閱檔案[檢查網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)。

## 限制 {#limitations}

搭配AEMaaCS使用自訂網域名稱有幾項限制。

* Cloud Manager僅支援Sites計畫的發佈和預覽服務的自訂網域名稱。
   * 不支援編寫服務的自訂網域。
* 每個 Cloud Manager 環境最多可以託管 500 個自訂網域。
* 當有一個目前正在執行的管道連接到這些環境時，無法將網域名稱新增到環境中。
* 同一個網域名稱不能在多個環境中使用。
* 一次只能新增一個網域名稱。
* AEM as a Cloud Service 不支援萬用字元網域，例如 `*.example.com`。
* 在新增自訂網域名稱之前，必須為您的計畫安裝包含自訂網域名稱的有效SSL憑證（萬用字元憑證有效）。

## 開始 {#get-started}

* 透過[新增SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)，開始設定專案的新自訂網域名稱。
* 檢閱檔案[管理自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md)，以管理您現有的網域名稱。
