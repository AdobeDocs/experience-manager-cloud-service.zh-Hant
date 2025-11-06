---
title: 表單提交與整合
description: 瞭解如何設定表單提交作業，以及將Forms Experience Builder表單與外部系統、API和業務工作流程整合。
feature: Edge Delivery Services
hide: true
index: false
hidefromtoc: true
role: Admin, Developer
exl-id: c772556b-dab6-4fa8-b728-1fe52c6596a4
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '915'
ht-degree: 2%

---

# 表單提交與整合

>[!NOTE]
>
> Forms Experience Builder可透過搶先使用計畫取得。 開始之前，請確定您已提出要求並獲授存取權。

Forms Experience Builder提供強大的整合功能，將您的表單與外部系統、API和業務工作流程連結。 本指南涵蓋如何設定表單提交和設定各種整合案例。

## 提交設定選項

### 電子郵件提交

設定表單以透過電子郵件傳送提交內容：

**基本電子郵件設定：**

- 設定收件者電子郵件地址
- 設定電子郵件範本
- 新增副本和密件副本收件者
- 設定電子郵件通知

**進階電子郵件功能：**

- 動態收件者選擇
- 含有表單資料的電子郵件範本
- 附件處理
- 電子郵件傳遞確認

### REST API整合

將表單連線至外部API和服務：

**API端點組態：**

- 設定REST API URL
- 設定驗證方法
- 設定請求標頭和引數
- 處理回應資料

**資料對應：**

- 將表單欄位對應至API引數
- 轉換資料格式
- 處理巢狀JSON結構
- 管理錯誤回應

### 雲端儲存整合

在雲端儲存服務中儲存表單提交：

**支援的平台：**

- Microsoft Azure Blob儲存體
- Amazon S3
- Google雲端儲存空間
- SharePoint Online

**組態選項：**

- 設定儲存認證
- 設定檔案夾結構
- 設定檔案命名慣例
- 管理存取許可權

### 工作流程整合

將表單連線至業務流程工作流程：

**Microsoft Power Automate：**

- 在表單提交時觸發工作流程
- 將表單資料傳遞至工作流程步驟
- 處理工作流程回應
- 管理核准流程

**Adobe工作流程：**

- 整合AEM工作流程
- 設定核准鏈
- 設定通知步驟
- 管理檔案處理

## 設定表單提交

### 步驟1：存取提交設定

1. 在Forms Experience Builder中開啟表單
2. 瀏覽至提交設定
3. 選取「設定表單提交」
4. 選擇您的整合型別

### 步驟2：設定電子郵件提交

**基本電子郵件設定：**

    設定電子郵件提交至hr@company.com的方式：
     — 主旨：「新員工申請」
     — 在電子郵件內文中包含表單資料
     — 傳送確認給申請者

**進階電子郵件設定：**

    設定動態電子郵件路由：
     — 如果部門等於「IT」，傳送至it-hr@company.com
     — 如果部門等於「銷售」，傳送至sales-hr@company.com
     — 預設為hr@company.com

### 步驟3：設定API整合

**REST API組態：**

    提交表單資料至REST端點：
    - URL： https://api.company.com/forms/submit
     — 方法： POST
     — 驗證：持有人權杖
    - Content-Type： application/json

**資料對應範例：**

    將表單欄位對應到API：
    - firstName -> user.first_name
    - lastName -> user.last_name
    - email -> user.email_address
    - department -> user.department_id

### 步驟4：設定雲端儲存空間

**Azure Blob儲存設定：**

    在Azure中儲存表單提交：
     — 容器：表單提交
     — 資料夾：/{year}/{month}/{day}/
     — 檔案格式：含附件的JSON
     — 存取層級：私人

## 整合範例

### 客戶回饋意見表單

**提交組態：**

- 傳送電子郵件通知給支援團隊
- 透過API在CRM系統中儲存資料
- 自動建立支援票證
- 傳送確認電子郵件給客戶

**實作：**
將客戶意見回饋表單提交至：
1.電子郵件<support@company.com>包含表單詳細資料
2.張貼至CRM API以建立客戶記錄
3.觸發支援票證建立工作流程
4.傳送感謝電子郵件給客戶

### 員工入職表單

**提交組態：**

- 以電子郵件傳送新員工資訊給人力資源團隊
- 在SharePoint中儲存檔案
- 觸發上線工作流程
- 在各種系統中建立使用者帳戶

**實作：**
處理員工上線：
1.電子郵件<hr@company.com>包含員工詳細資料
2.將檔案上傳至SharePoint員工資料夾
3.在Power Automate中開始入門工作流程
4.在HR系統、電子郵件和其他工具中建立帳戶

### 潛在客戶產生表單

**提交組態：**

- 在行銷自動化平台中儲存潛在客戶資料
- 傳送通知給銷售團隊
- 將潛在客戶新增至CRM系統
- 觸發後續追蹤電子郵件順序

**實作：**
處理銷售機會開發：
1.將潛在客戶資料發佈至Marketo API
2.在Salesforce中建立潛在客戶記錄
3.傳送電子郵件給銷售團隊，其中包含潛在客戶詳細資訊
4.開始自動化電子郵件培養程式

## 進階整合案例

### 多步驟表單處理

**複雜的工作流程整合：**

- 針對外部系統驗證表單資料
- 透過付款閘道處理付款
- 產生檔案和合約
- 傳送通知給多位利害關係人

### 即時資料驗證

**API型驗證：**

- 根據公司目錄驗證電子郵件地址
- 檢查存貨系統中的產品可用性
- 驗證CRM中的客戶資訊
- 驗證付款資訊

### 條件式提交路由

**根據表單資料的動態路由：**

- 根據查詢型別到不同部門的路線
- 根據客戶層級傳送至不同的系統
- 根據表單完成狀態進行不同的處理
- 根據地區處理不同的商業規則

## 安全性與合規性

### 資料保護

**加密和安全性：**

- 加密傳輸中的敏感資料
- 安全API憑證和權杖
- 實作適當的存取控制
- 遵循資料保留政策

### 合規性要求

**GDPR和隱私權：**

- 實作同意管理
- 提供資料匯出功能
- 啟用資料刪除請求
- 維護稽核軌跡

**產業標準：**

- 醫療保健表單符合HIPAA規範
- 用於付款處理的PCI DSS
- 適用於財務表單的SOX規範
- 特定產業法規

## 測試和驗證

### 提交測試

**測試案例：**

- 驗證電子郵件傳遞和格式
- 測試API連線和資料對應
- 驗證雲端儲存空間上傳
- 檢查工作流程觸發程式功能

**錯誤處理：**

- 測試網路失敗案例
- 驗證錯誤訊息顯示
- 檢查重試機制
- 驗證遞補選項

### 效能最佳化

**最佳化策略：**

- 實作非同步處理
- 對大量資料使用批次作業
- 最佳化API呼叫頻率
- 快取經常存取的資料

## 疑難排解整合問題

### 常見問題

**電子郵件傳遞問題：**

- 檢查SMTP伺服器設定
- 驗證收件者電子郵件地址
- 檢閱垃圾郵件篩選設定
- 測試電子郵件範本格式

**API整合問題：**

- 驗證API端點URL
- 檢查驗證認證
- 驗證請求格式和標頭
- 檢閱API回應處理

**儲存整合問題：**

- 確認儲存認證
- 檢查檔案夾許可權
- 驗證檔案上傳限制
- 測試網路連線

### 取得協助

若為整合問題：

- 檢視[Forms Experience Builder常見問題集](forms-experience-builder-frequently-asked-questions.md)
- 檢閱[快速入門手冊](forms-experience-builder-getting-started.md)
- 請連絡您的系統管理員以取得技術協助
- 請參閱外部服務的API檔案

## 相關的文章

- [Forms Experience Builder概述](product-overview.md)
- [表單體驗建立工具快速入門](forms-experience-builder-getting-started.md)
- [部署和設定表單體驗建立工具](deploy-forms-experience-builder.md)
- [智慧型匯入和轉換](intelligent-import-conversion.md)
- [常見問題](forms-experience-builder-frequently-asked-questions.md)
