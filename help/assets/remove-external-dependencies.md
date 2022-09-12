---
title: 刪除現有安裝的外部依賴項
description: 刪除現有安裝的外部依賴項
feature: Integrations
exl-id: 5b28ce97-2719-47b8-a386-77d4aaddbe81
source-git-commit: b71a78696d4b347c97b077d84b455f53a1747a07
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 刪除現有安裝的外部依賴項 {#remove-external-depedencies}

Adobe建議您為Workfront的現有增強連接器安裝執行配置步驟，以移除對Hoodoo分佈點的依賴項。

>[!NOTE]
>
>只有在2022年3月之前已安裝Workfront的增強連接器時，才執行設定步驟。 自2022年3月起，Workfront全新增強連接器安裝對Hoodoo分發點沒有相依性。

要刪除外部依賴項：

1. 從父級中刪除以下Hoodoo儲存庫配置 `pom.xml`:

   ```XML
     <repository>
        <id>hoodoo-maven</id>
        <name>Hoodoo Repository</name>
        <url>https://gitlab.com/api/v4/projects/12715200/packages/maven</url>
     </repository>
   ```

1. 從 `settings.xml` 檔案，可在 `./cloudmanager/maven/settings.xml`:

   ```XML
         <server>
            <id>hoodoo-maven</id>
            <configuration>
               <httpHeaders>
                     <property>
                        <name>Deploy-Token</name>
                        <value>xxxxxxxxxxxxxxxx</value>
                     </property>
               </httpHeaders>
            </configuration>
         </server>
   ```

1. 執行 [新安裝步驟](workfront-connector-install.md).
