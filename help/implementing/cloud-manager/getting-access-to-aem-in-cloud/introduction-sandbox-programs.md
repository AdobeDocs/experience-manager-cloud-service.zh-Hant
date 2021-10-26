---
title: '沙箱方案簡介 '
description: 沙箱方案簡介
exl-id: 4606590c-6826-4794-9d2e-5548a00aa2fa
source-git-commit: 1892900ea3f365e1b5f7d31ffae64d45256d2a3a
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 沙箱方案簡介 {#sandbox-programs}

## 簡介 {#introduction}

沙箱方案是AEM Cloud Service提供的兩種方案之一，另一種是生產方案。

沙箱的建立通常是為了提供訓練、執行示範、培訓或概念驗證(POC)。它們不能承載即時流量。 它們不受 [AEMas a Cloud Service承諾](https://www.adobe.com/legal/service-commitments.html).

在沙箱中建立的環境沒有針對自動縮放進行設定。 因此，這些環境不適合進行效能或負載測試。

沙箱方案包括 [!DNL Sites] 和 [!DNL Assets] 和會自動填入Git存放庫、開發環境和非生產管道。  Git存放庫會根據AEM專案原型填入範例專案。

>[!IMPORTANT]
>沙箱方案只會有一個開發環境。

>[!NOTE]
>沙箱方案中無法使用自訂網域和IP允許清單。

請參閱 [了解方案和方案類型](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/understand-program-types.html?lang=en) 以深入了解方案類型。

### 沙箱方案的屬性 {#attributes-sandbox}

沙箱方案具有下列屬性：

1. **方案建立：** 沙箱方案建立包括自動：
   * 包含范常式式碼和內容的專案設定
   * 開發環境的創造
   * 建立非生產管道部署至開發環境（主分支部署至開發環境）

1. **解決方案：** 沙箱方案包括AEM [!DNL Sites] 和 [!DNL Assets].

1. **AEM更新：** AEM更新可手動套用至沙箱方案中的環境，且不會自動推送。
請參閱 [AEM沙箱環境的更新](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md#aem-updates-sandbox) 以取得更多詳細資訊。

1. **休眠：** 如果在特定期間內未偵測到任何活動，沙箱方案中的環境會自動休眠。 閒置8小時後，沙箱會放入休眠節點，等到沙箱休眠後，即可解除休眠狀態。 休眠環境可以手動解除休眠狀態。
請參閱 [休眠和解除休眠沙箱環境](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md) 以取得更多詳細資訊。

1. **刪除**:沙箱會在6個月處於連續休眠模式後刪除，經過6個月後，便可重新建立。
