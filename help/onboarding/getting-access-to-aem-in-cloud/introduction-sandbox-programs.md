---
title: '沙盒程式簡介 '
description: '沙盒程式簡介 '
translation-type: tm+mt
source-git-commit: d98e3ba930690627bfbe9b90ce5cb93328c30503
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---


# 沙盒程式簡介{#sandbox-programs}

## 簡介 {#introduction}

沙盒程式是Cloud Service提供的兩種程式類型之AEM一，另一種是生產程式。

建立沙盒通常是為了提供訓練、執行示範、啟用或概念驗證(POC)的目的。他們不是要載著現場交通的。 它們不受[作為AEMCloud Service承諾的約束。](https://www.adobe.com/legal/service-commitments.html)

在沙盒中建立的環境未設定為自動縮放。 因此，這些環境不適合進行效能或負載測試。

沙盒程式包括「網站」和「資產」，並自動填入Git儲存庫、開發環境和非生產管道。  Git儲存庫會填入基於「項目」原型的AEM示例項目。

請參閱[瞭解程式和程式類型](/help/onboarding/getting-access-to-aem-in-cloud/understand-program-types.md)以進一步瞭解程式類型。

### 沙盒程式屬性{#attributes-sandbox}

「沙盒程式」具有下列屬性：

1. **程式建立：沙** 箱程式建立包括自動：
   * 使用范常式式碼和內容設定專案
   * 開發環境的創造
   * 建立非生產性管道以部署至開發環境（主分支部署至開發環境）

1. **解決方案：沙** 盒程式包括AEM Sites和資產。

1. **更新AEM：更** 新可手AEM動套用至沙盒程式中的環境，且不會自動推送。如需詳細資訊，請參AEM閱[沙盒環境更新](/help/onboarding/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md#aem-updates-sandbox)。

1. **休眠：如** 果在某段時間內未檢測到任何活動，則沙盒程式中的環境會自動休眠。休眠的環境可以手動解除休眠。
如需詳細資訊，請參閱[冬眠和解除冬眠沙盒環境](/help/onboarding/getting-access-to-aem-in-cloud/hibernating-de-hibernating-sandbox-environments.md)。