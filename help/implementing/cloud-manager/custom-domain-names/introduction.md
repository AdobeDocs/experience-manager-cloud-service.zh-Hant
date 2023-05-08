---
title: 自訂網域名稱簡介
description: Cloud Manager 的 UI 可讓您新增自訂網域，以自助方式使用唯一的品牌名稱來識別您的網站。
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
source-git-commit: 1862ae2d0d60ac9ed89a4ba3da82dcf8f032ee65
workflow-type: ht
source-wordcount: '770'
ht-degree: 100%

---


# 自訂網域名稱簡介 {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="管理自訂網域名稱"
>abstract="Cloud Manager 的 UI 可讓您新增自訂網域，以自助方式使用唯一的品牌名稱來識別您的網站。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name.html?lang=zh-Hant" text="新增自訂網域名稱"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.html?lang=zh-Hant" text="檢視和更新自訂網域名稱"

Cloud Manager 的 UI 可讓您新增自訂網域，以自助方式使用唯一的品牌名稱來識別您的網站。Adobe Experience Manager as a Cloud Service已佈建預設網域名稱，結尾為 `*.adobeaemcloud.com`。即使您將自訂網域名稱與您的網站相關聯，此預設網域名稱仍會保留。

## 什麼是自訂網域名稱？ {#what-are-custom-domain-names}

每個網站都有一個與之關聯的電腦可讀取的唯一數字位址，例如 `184.33.123.64`。網域名稱系統 (DNS) 可讓您將數字位址轉換為令人難忘的位址，例如，將自訂、品牌化的網域附加至網站 `wknd.com`。

為您的網站命名網域名稱是很好的作法，這會讓客戶難忘並反映您的品牌。

您可以向網域名稱註冊機構、管理和銷售網域名稱的公司或組織購買網域名稱。網域名稱註冊機構管理 DNS 伺服器上的網域名稱。

>[!IMPORTANT]
>
>Cloud Manager 不是網域名稱註冊機構，不提供 DNS 服務。

## 自訂網域名稱和 BYO CDN {#byo-cdn}

AEM as a Cloud Service 提供內建的內容傳遞網路 (CDN) 服務，但也允許您自攜 (BYO) CDN 以搭配 AEM 使用。自訂網域可以安裝在 AEM 管理的 CDN 或您管理的 CDN 中。

* 安裝在 AEM 管理的 CDN 中的自訂網域名稱 (和憑證) 是透過 Cloud Manager 進行管理。
* 安裝在您自己 CDN 中的自訂網域名稱 (和憑證) 是在特定 CDN 中進行管理。

在您自己 CDN 中管理的網域不需要透過 Cloud Manager 安裝。它們將透過 X-Forwarded-Host 提供給 AEM，並將與 Dispatcher 中定義的虛擬主機相符。[如需詳細資訊，請參閱 CDN 文件。](/help/implementing/dispatcher/cdn.md)

在一個環境中，您可以將兩個網域安裝在 AEM 管理的 CDN 中，和安裝在您自己的 CDN 中。

## 工作流程 {#workflow}

新增自訂網域名稱需要 DNS 服務和 Cloud Manager 互動。因此，安裝、設定和驗證自訂網域名稱需要執行許多步驟。下表總覽了所需的步驟，包括發生常見錯誤時應採取的措施。

| 步驟 | 說明 | 責任 | 了解更多 |
|--- |--- |--- |---|
| 1 | 將 SSL 憑證新增到 Cloud Manager | 客戶 | [新增 SSL 憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | 新增 TXT 記錄以驗證網域 | 客戶 | [新增 TXT 記錄](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) |
| 3 | 查看網域驗證狀態 | 客戶 | [檢查網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3a | 如果網域驗證失敗並顯示狀態為 `Domain Verification Failure` | 客戶 | [檢查網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3b | 如果網域驗證失敗並顯示狀態為 `Verified, Deployment Failed`，請聯絡 Adobe | Adobe 客戶服務 | [檢查網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 4 | 新增指向 AEM as a Cloud Service 的 DNS CNAME 或 Apex 記錄，以設定 DNS 設定 | 客戶 | [正在設定 DNS 設定](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) |
| 5 | 檢查 DNS 記錄狀態 | 客戶 | [檢查 DNS 記錄狀態](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5a | 如果 DNS 記錄狀態失敗：`DNS status not detected` | 客戶 | [檢查 DNS 記錄狀態](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5b | 如果 DNS 記錄狀態失敗：`DNS resolves incorrectly` | 客戶 | [檢查 DNS 記錄狀態](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |

>[!TIP]
>
>使用 AEM as a Cloud service 設定自訂網域名稱通常是一個簡單的過程。但是，有時可能會出現網域委派問題，這可能需要 1-2 個工作日才能解決。出於這個原因，強烈建議在上線日期之前安裝網域。請參閱文件：[檢查網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)以了解詳細資訊。

## 限制 {#limitations}

搭配 AEMaaCS 使用自訂網域名稱有幾項限制。

* Cloud Manager 支援自訂網域名稱用於 Sites 計畫的發佈和預覽服務。不支援作者服務的自訂網域。
* 每個 Cloud Manager 環境最多可以託管 500 個自訂網域。
* 當有目前正在執行的管道連線到這些環境時，無法將網域名稱新增到環境中。
* 同一個網域名稱不能在多個環境中使用。
* 一次只能新增一個網域名稱。
* AEM as a Cloud Service 不支援萬用字元網域，例如 `*.example.com`。
* 在新增自訂網域名稱之前，必須為您的程序安裝包含自訂網域名稱的有效 SSL 憑證 (萬用字元憑證有效)。如需了解更多資訊，請參閱[新增 SSL 憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)。
