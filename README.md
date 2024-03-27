# 開發兩支 Nest.js API，用於管理應用程式的配置設定。

## 一支 API 用於取得當前設定，另一支 API 用於更新設定。

步驟說明：

1. 建立一份 app.config.json 文件如下，放置於專案根目錄

```json
{
  "maxConnections": 10000,
  "maintenanceMode": false,
  "supportedLocales": [
    "en-US",
    "fr-FR",
    "es-ES"
  ],
  "loggingLevel": "info"
}
```

2. 為資料創建 interface

3. 製作 API

-  GET /get-config 返回當前的 app.config.json 文件內容。
  - 成功也必須回傳狀態碼 200 及成功訊息
- PUT /update-config
  - 允許部分更新配置文件中的項目，必須滿足以下驗證條件
  - maxConnections 必須是數字，限制 0 ~ 10000。
  - maintenanceMode 必須是boolean。
  - supportedLocales 可以接收任意字串傳入。
  - loggingLevel 只能為 "debug" 、"warn"、"error"、"info" 這四種。
  - 如不符合以上條件，需回傳錯誤訊息 400 Bad Request ，及error-message，格式不限
  - 成功也必須回傳狀態碼 200 及成功訊息


### 參考資料

讀取本機檔案的方法：

```typeScript

import * as fs from 'fs';

import * as path from 'path';

// 讀取檔案位址方法
const configPath = path.resolve('app.config.json')

// 讀取檔案的方法，解析為 utf-8 'string'
const configData = fs.readFileSync(configPath, 'utf-8');

// 寫入檔案方法，參數檢查完後進行寫檔 JSON.stringify
fs.writeFileSync(path, JSON.stringify(data, null, 2))

```