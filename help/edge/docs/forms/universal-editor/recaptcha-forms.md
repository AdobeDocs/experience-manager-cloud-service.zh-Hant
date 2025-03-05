---
title: 使用reCAPTCHA保護您的Forms — 視覺化指南
description: 瞭解如何輕鬆將Google reCAPTCHA新增至Edge Delivery Services表單，以防止垃圾郵件和機器人提交
feature: Edge Delivery Services
keywords: 在表單中使用reCAPTCHA，在通用編輯器中新增reCAPTCHA，表單安全性，垃圾郵件保護
role: Developer
exl-id: 1f28bd13-133f-487e-8b01-334be7c08a3f
source-git-commit: babddee34b486960536ce7075684bbe660b6e120
workflow-type: tm+mt
source-wordcount: '1085'
ht-degree: 1%

---


# 使用Google reCAPTCHA保護您的Forms免受垃圾郵件侵擾

<span class="preview">此功能可透過搶先存取計畫使用。 若要要求存取權，請將您的正式地址電子郵件傳送至<a href="mailto:aem-forms-ea@adobe.com">aem-forms-ea@adobe.com</a>，其中包含您的GitHub組織名稱和存放庫名稱。</span>



## 為何要在表單中使用reCAPTCHA？

| ![安全性](/help/edge/docs/forms/universal-editor/assets/security.svg) | ![機器人保護](/help/edge/docs/forms/universal-editor/assets/bot-protection.svg) | ![使用者體驗](/help/edge/docs/forms/universal-editor/assets/user-experience.svg) |
|:-------------:|:-------------:|:-------------:|
| **增強式安全性** | **機器人與垃圾郵件預防** | **順暢的使用者體驗** |
| 保護您的表單免受詐騙活動和惡意攻擊 | 阻止自動化機器人讓您的表單充斥著無關或有害的內容 | 隱藏的reCAPTCHA可在幕後運作，而不會干擾合法使用者 |

例如，含有敏感財務資訊的稅捐計算表單需要保護，以免遭到濫用。 reCAPTCHA會驗證提交內容是否來自正版使用者，而非自動化系統。

## 選擇您的reCAPTCHA解決方案

Edge Delivery Services Forms支援兩個Google reCAPTCHA選項：

| ![reCAPTCHA Enterprise](/help/edge/docs/forms/universal-editor/assets/enterprise.svg) | ![reCAPTCHA Standard](/help/edge/docs/forms/universal-editor/assets/standard.svg) |
|:-------------:|:-------------:|
| [**reCAPTCHA Enterprise**](#set-up-recaptcha-enterprise) | [**reCAPTCHA Standard**](#set-up-recaptcha-standard) |
| 高階的企業級詐騙偵測，以及額外的功能和客製化 | 免費服務，提供以分數為基礎的偵測功能，可在背景以不可見的方式運作 |
| 最適合：具有複雜安全性需求的大型組織 | 最適合：具有基本保護需求的中小型專案 |

這兩個選項都使用以分數為基礎的偵測（0.0到1.0）來識別人與機器人的互動，而不會中斷使用者體驗。

## 設定reCAPTCHA Enterprise

### 步驟1：取得您的Google Cloud認證

設定reCAPTCHA Enterprise之前，您需要：

- [Google Cloud專案](https://cloud.google.com/recaptcha/docs/prepare-environment#before-you-begin) （含您的[專案ID](https://support.google.com/googleapi/answer/7014113)）
- [reCAPTCHA Enterprise API已啟用](https://cloud.google.com/recaptcha/docs/prepare-environment#enable-api)專案
- 用於驗證的[API金鑰](https://console.cloud.google.com/apis/credentials)
- 您網域的[網站金鑰](https://console.cloud.google.com/security/recaptcha)

### 步驟2：建立雲端設定容器

![逐步雲端組態設定](/help/edge/docs/forms/universal-editor/assets/recaptcha-general-configuration.png)

1. 登入您的AEM作者執行個體
2. 瀏覽至&#x200B;**工具** > **一般** > **設定瀏覽器**
3. 尋找您的表單並選取&#x200B;**屬性**
4. 在對話方塊中啟用&#x200B;**雲端設定**
5. 儲存並發佈您的設定

### 步驟3：設定reCAPTCHA Enterprise Service

![reCAPTCHA Enterprise組態畫面](/help/edge/docs/forms/universal-editor/assets/recaptcha-enterprise.png)

1. 移至&#x200B;**工具** > **雲端服務** > **reCAPTCHA**
2. 導覽至您的表單，然後按一下&#x200B;**建立**
3. 在對話方塊：
   - 選取&#x200B;**ReCAPTCHA Enterprise**&#x200B;版本
   - 輸入標題和名稱
   - 新增您的專案ID、網站金鑰和API金鑰
   - 選取&#x200B;**以分數為基礎的網站金鑰**&#x200B;作為金鑰型別
   - 設定臨界值分數(0-1)以區分人類和機器人
4. 按一下「**建立**」並發佈您的設定

## 設定reCAPTCHA Standard

### 步驟1：取得API金鑰

開始之前，請從Google reCAPTCHA主控台[取得reCAPTCHA API金鑰組](https://www.google.com/recaptcha/admin) （網站金鑰和秘密金鑰）。

>[!IMPORTANT]
>
>Edge Delivery Services 表單僅支援 **reCAPTCHA 分數型**&#x200B;版本。

### 步驟2：建立雲端設定容器

依照與Enterprise版本相同的步驟，建立和發佈雲端設定容器。

### 步驟3：設定reCAPTCHA標準服務

![reCAPTCHA標準組態畫面](/help/edge/docs/forms/universal-editor/assets/recaptcha.png)

1. 移至&#x200B;**工具** > **雲端服務** > **reCAPTCHA**
2. 導覽至您的表單，然後按一下&#x200B;**建立**
3. 在對話方塊：
   - 選取&#x200B;**ReCAPTCHA v2**&#x200B;版本
   - 輸入標題和名稱
   - 新增您的網站金鑰與秘密金鑰
4. 按一下「**建立**」並發佈您的設定

## 將reCAPTCHA新增至您的表單

現在您已設定reCAPTCHA，是時候將其新增至您的表單了：

![正在新增reCAPTCHA元件至表單](/help/edge/docs/forms/universal-editor/assets/add-recaptcha-component.png)

1. 在通用編輯器中開啟您的表單
2. 導覽至內容樹狀結構中的最適化表單區段
3. 按一下&#x200B;**新增**&#x200B;圖示，然後從最適化表單元件清單中選取&#x200B;**驗證碼（隱藏）**
   - *或者，將元件拖放到您的表單中*
4. 按一下&#x200B;**發佈**&#x200B;以使用reCAPTCHA保護更新您的表單

您的表單現在已受保護！ 檢視位置：
`https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form-name>`

![已啟用reCAPTCHA保護的表單](/help/edge/docs/forms/universal-editor/assets/form-with-recaptcha.png)

## 驗證您的reCAPTCHA整合

新增reCAPTCHA至您的表單後，必須確認其正常運作。 以下說明如何驗證實作：

### 視覺驗證

reCAPTCHA v2 （以分數為基礎）以不可見方式運作，但您可以透過以下方式確認其存在：

1. **檢查頁面來源**：用滑鼠右鍵按一下您的表單頁面，然後選取[檢視頁面Source]
   - 尋找包含您的網站金鑰的reCAPTCHA指令碼
   - 範例： `<script src="https://www.google.com/recaptcha/api.js?render=YOUR_SITE_KEY"></script>`

2. **檢查網路要求**：使用瀏覽器開發人員工具(F12)
   - 提交您的表單並尋找`google.com/recaptcha`的網路要求
   - 這些請求表示您的表單上有reCAPTCHA作用中

### 功能測試

若要確認reCAPTCHA是否確實在保護您的表單：

1. **正常提交測試**：
   - 使用有效資料填寫您的表單
   - 以正常的人工步調提交表單
   - 驗證表單是否成功提交

2. **類似機器人的行為測試**：
   - 在無痕瀏覽/私人瀏覽視窗中開啟您的表單
   - 快速填寫表單（類似自動的行為）
   - 連續快速提交多次
   - 如果reCAPTCHA運作正常，這些提交內容可能會被封鎖或標幟

3. **檢查表單提交記錄**：
   - 檢閱您的表單提交資料
   - 每次提交都應包含reCAPTCHA分數
   - 分數接近1.0表示可能是人類使用者
   - 分數接近0.0表示潛在的機器人活動

### 使用Google reCAPTCHA管理控制檯

對於企業使用者，Google Cloud Console提供詳細分析：

1. 前往[Google Cloud Console](https://console.cloud.google.com/)
2. 瀏覽至&#x200B;**安全性** > **reCAPTCHA**
3. 選取您的網站金鑰
4. 檢閱評定圖表和統計資料
5. 尋找：
   - 流量模式
   - 評分分佈
   - 潛在詐騙活動

對於標準reCAPTCHA使用者，[reCAPTCHA Admin Console](https://www.google.com/recaptcha/admin/)中提供基本統計資料。

### 調整實施

根據您的驗證結果：

- 如果合法使用者遭到封鎖，請考慮降低臨界值分數
- 如果您仍收到垃圾郵件，請考慮提高您的臨界值分數
- 對於持續性問題，請檢閱您的reCAPTCHA設定，並確保所有金鑰均已正確輸入

請記住，reCAPTCHA會使用機器學習來隨時間改善，因此在學習您網站的流量模式時，其有效性可能會提高。

## 疑難排解和常見問題( FAQs)

| ![問題](/help/edge/docs/forms/universal-editor/assets/question.svg) | ![答案](/help/edge/docs/forms/universal-editor/assets/answer.svg) |
|:-------------:|:-------------:|
| **如果未建立reCAPTCHA組態怎麼辦？** | 系統會在「全域容器」中尋找設定。 如果不存在任何專案，您將會收到錯誤。 |
| **如果我建立多個設定會發生什麼事？** | 系統會自動使用第一個建立的組態。 |
| **為什麼我的變更沒有顯示在已發佈的URL上？** | 進行變更後，請務必重新發佈表單。 |
| **支援哪些reCAPTCHA服務？** | Edge Delivery Services Forms僅支援以分數為基礎的reCAPTCHA服務。 |

## 後續步驟

現在您已使用reCAPTCHA保護您的表單：

- **驗證您的實作**：請依照[驗證步驟](#-validating-your-recaptcha-integration)操作，以確保reCAPTCHA正常運作
- **監視效能**：定期檢查您的Google reCAPTCHA儀表板是否有可疑活動和分數分佈
- **微調設定**：根據您的安全性需求和使用者體驗意見反應，調整您的臨界值分數
- **保持更新**：透過Google的最新安全性建議，讓您的reCAPTCHA實作保持最新狀態
- **教育您的團隊**：分享有關reCAPTCHA如何運作以及如何解譯分析的知識
- **收集意見回饋**：監視使用者體驗，以確保不會封鎖合法的使用者

請記住，有效的表單保護是一項持續進行的程式，需要定期監控和調整。


