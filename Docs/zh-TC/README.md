<!-- Aegis Logo -->
<p align="center">
  <img src="https://raw.githubusercontent.com/Thoseyearsbrian/Aegis/main/assets/Aegis_Cover_Image.png" alt="Aegis Cover Image"/>
</p>

<h1 align="center">GeoIP2-Country 自動構建與更新方案</h1>

<p align="center">
  [<a href="https://github.com/Thoseyearsbrian/GeoIP2-Country/blob/main/Docs/zh-CN/README.md">簡體中文</a>]
  [<a href="https://github.com/Thoseyearsbrian/GeoIP2-Country/blob/main/Docs/zh-TC/README.md">繁體中文</a>]
  [<a href="https://github.com/Thoseyearsbrian/GeoIP2-Country/blob/main/Docs/en-US/README.md">English</a>]
</p>

<p align="center">
  <img src="https://img.shields.io/badge/License-Apache%202.0-blue.svg" alt="License: Apache 2.0" />
  <img src="https://github.com/Thoseyearsbrian/GeoIP2-Country/actions/workflows/update.yml/badge.svg" alt="GeoIP Auto Update Status" />
  <img src="https://img.shields.io/github/stars/Thoseyearsbrian/GeoIP2-Country?style=social" alt="GitHub stars" />
  <img src="https://img.shields.io/github/v/release/Thoseyearsbrian/GeoIP2-Country?include_prereleases&label=version" alt="Version" />
  <img src="https://img.shields.io/github/last-commit/Thoseyearsbrian/GeoIP2-Country" alt="Last Commit" />
  <a href="https://github.com/Thoseyearsbrian/GeoIP2-Country">
    <img src="https://img.shields.io/badge/Mirror--Prohibited-red" alt="Mirror Prohibited" />
  </a>
</p>

## 項目概述

本項目提供自動下載並構建 MaxMind 官方 GeoLite2-Country.mmdb 數據庫的腳本與配置方案，使使用者能夠基於自身的 MaxMind License Key 自動生成覆蓋全球各國家與地區的 IP 地理定位數據文件。項目旨在為 Surge、Clash、Shadowrocket、Quantumult X 等網路工具提供來源可信、鏈路透明、自動更新的國家級 IP 定位支援，實現更精確的國家級分流策略與路由控制。

## 項目背景

在網路安全與策略分流配置中，GeoIP 數據庫被廣泛用於判斷 IP 屬地，輔助智慧路由或存取控制。當前不少項目使用二手分發來源，存在以下潛在問題：

- **缺乏信任鏈：** 非官方來源內容不可審計，存在被污染或篡改的風險；
- **可維護性差：** 不可預測是否隨時中斷；
- **更新滯後：** 間隔時間不可控。

為此，本項目實現完全自控化更新機制，確保數據來源為 MaxMind 官方，結構可追溯、更新可控、邏輯可審計，適配 Surge、Clash、Shadowrocket、Quantumult X 等配置使用。

## 項目優勢

- **官方數據來源：** 所有數據均直接來自 MaxMind，可信、安全；
- **自動更新：** 透過 GitHub Actions 每 3 天拉取最新版本，持續同步；
- **遵循授權機制：** 項目基於 GitHub Actions 自動拉取 MaxMind 數據，並根據其 [GeoLite2 使用協議](https://www.maxmind.com/en/geolite2/eula) 提供更新邏輯。建議使用者自行申請 License Key 使用本項目，確保數據來源合規、安全、可追溯。
- **自訂可控：** 使用者可根據實際需求自由配置輸出路徑、更新頻率、目標分支等參數，滿足個性化部署場景。

### 自動化更新

項目採用 GitHub Actions 實現自動更新機制，每隔 3 天拉取最新數據，確保始終保持最新狀態，無需人工干預。

## 文件路徑

| 文件名稱     |                  構建後文件路徑（僅供參考）                  | 示例用途                                                     |
| ------------ | :----------------------------------------------------------: | ------------------------------------------------------------ |
| Country.mmdb | [`data/Country.mmdb`](https://raw.githubusercontent.com/Thoseyearsbrian/GeoIP2-Country/main/data/GeoLite2-Country.mmdb) | Surge、Clash、QuantumultX 等支援 GeoIP 的工具作為 國家級 區域判斷依據 |

## 配置方式

配置 MaxMind License Key（必需）

本項目需要存取 MaxMind 官方 GeoLite2 數據庫，因此您需要：

1.前往 [MaxMind 官網](https://www.maxmind.com) 註冊帳戶並取得 GeoLite2 License Key

2.打開倉庫：Secrets 配置列表（在 GitHub → Settings → Secrets → Actions 中新增）

3.新增以下 Secrets（名稱必須完全一致）：

- MAXMIND_ACCOUNT_ID      # 你的 MaxMind Account ID （必填）
- MAXMIND_LICENSE_KEY     # 你的 MaxMind License Key（必填）

## 使用教學

複製文件路徑 -> 打開 Surge -> 打開 通用 -> GeoIp資料庫 -> 刪除歷史配置（如有） -> 貼上連結 -> 立即更新 -> 套用 -> 完成!

<p align="center">
  <img src="https://raw.githubusercontent.com/Thoseyearsbrian/GeoIP2-Country/main/Icons/Groups/surge-geoip-config-guide-step-by-step.png" width="600">
</p>

## ⚠️  注意事項

1. **本項目中，僅人工提交（由真實開發者進行）使用 GPG 金鑰進行簽名驗證。**

自動化更新（如 GeoLite2 數據更新）由 GitHub Actions 執行，不會使用 GPG 簽名。請認準提交者為 [`github-actions[bot]`](https://github.com/apps/github-actions) 即可視為有效與可信。

- 人工提交仍啟用 GPG 簽名驗證，用於標識真實開發者身份  
- 我們不建議將任何 GPG 私鑰託管於 GitHub，以避免金鑰洩露和簽名濫用

2. **推薦將 `China.list`（域名）與 `GEOIP,CN`（IP段）規則組合使用，以提高對中國流量的匹配準確性：**

```bash
RULE-SET,https://raw.githubusercontent.com/Thoseyearsbrian/Aegis/main/rules/China.list, DIRECT   # 精確匹配中國域名
GEOIP,CN,DIRECT                                                                                  # 匹配未在域名規則中出現的中國大陸 IP
FINAL,REJECT                                                                                     # 最終預設拒絕規則（請勿將 GEOIP 放於其後）
```

3. **本項目生成的 GeoLite2-Country 資料庫可用於 GEOIP 查詢（如 US、AU、CN 等），因為該資料庫本身提供完整的國家級 IP 區段結構。**

```bash
GEOIP, US, Proxy   # 正確
GEOIP, AU, Proxy   # 正確
GEOIP, CN, DIRECT  # 正確
```

## 🔐  免責聲明

本項目構建所得 `.mmdb` 文件僅用於測試與學習研究用途，**不得用於任何形式的商業用途**。

使用者需自行確保符合 [MaxMind EULA](https://www.maxmind.com/en/geolite2/eula) 協議及其地區相關法規，**本項目對因使用數據產生的任何行為或後果不承擔任何法律責任**。

本項目**僅提供構建邏輯與腳本**，不直接分發原始數據。建議使用者透過 MaxMind 官網申請並使用專屬 License Key。

**如您對授權合規性有疑問，建議聯絡 MaxMind 官方取得協助。**

**本項目僅面向具備基礎技術背景與合規意識的開發者群體使用。**

## 🏅  版權聲明

- 本項目透過自動構建流程生成 `.mmdb` 文件供測試與研究用途，訪問者請確保已閱讀並接受 [MaxMind EULA](https://www.maxmind.com/en/geolite2/eula)。**本項目不對使用者的任何用途或行為承擔法律責任，使用者需自行確保合規；**
- 本項目使用 GitHub Actions 自動拉取 MaxMind 官方數據。**使用本項目前，使用者需前往 MaxMind 官網註冊並取得屬於自己的 License Key**，以便合規運行腳本或自動更新流程；
- GeoLite2 數據版權歸 [MaxMind, Inc.](https://www.maxmind.com/) 所有，遵循其 [GeoLite2 資料庫授權協議](https://www.maxmind.com/en/geolite2/eula)；
- 本項目中所含腳本和配置文件遵循 [Apache License 2.0](https://raw.githubusercontent.com/Thoseyearsbrian/GeoIP2-Country/main/LICENSE)。
- 此外，Aegis 項目已啟用 GPG 簽名（Git Commit Signing）機制，以確保項目程式碼來源真實可信、未被篡改。你可透過 GPG 簽名驗證每一次提交操作的完整性，從而獲得更高的安全保障。