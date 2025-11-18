<!-- Aegis Logo -->
<p align="center">
  <img src="https://raw.githubusercontent.com/Thoseyearsbrian/Aegis/main/assets/Aegis_Cover_Image.png" alt="Aegis Cover Image"/>
</p>

<h1 align="center">GeoIP2-Country: Auto Build and Update Solution</h1>

<p align="center">
  <img src="https://img.shields.io/badge/License-Apache%202.0-blue.svg" alt="License: Apache 2.0" />
  <img src="https://github.com/Thoseyearsbrian/GeoIP2-Country/actions/workflows/update.yml/badge.svg" alt="GeoIP Auto Update Status" />
  <img src="https://img.shields.io/github/stars/Thoseyearsbrian/GeoIP2-Country?style=social" alt="GitHub stars" />
  <img src="https://img.shields.io/github/v/release/Thoseyearsbrian/GeoIP2-Country?include_prereleases&label=version" alt="Version" />
  <img src="https://img.shields.io/github/last-commit/Thoseyearsbrian/GeoIP2-Country" alt="Last Commit" />
</p>

<p align="center">
  <a href="https://github.com/Thoseyearsbrian/GeoIP2-Country/blob/main/Docs/zh-CN/README.md"><b>【中文文档点此进入】</b></a>
</p>

## **Overview**

This project provides automated scripts and configuration workflows for downloading and building the official MaxMind GeoLite2-Country.mmdb database, generating IP geolocation data covering all countries and regions worldwide. It is designed to provide trusted sourcing, transparent data flow, and automatic updates for tools such as Surge, Clash, Shadowrocket, and Quantumult X, enabling more accurate country-level routing and traffic control.

## **Project Background**

GeoIP databases are widely used in network security and traffic policy routing to determine IP geolocation and assist with smart routing or access control. Many current projects rely on third-party distribution sources, which introduce potential risks:

- **Lack of trust chain**: Non-official sources cannot be audited and may be tampered with;
- **Poor maintainability**: Sources may become unavailable without notice;
- **Outdated data**: Updates may be delayed or irregular.

To address these issues, this project implements a fully self-controlled update mechanism, ensuring the data source is official from MaxMind, structurally traceable, update-controllable, and logically auditable. It is optimized for use in Surge, Clash, Shadowrocket, and Quantumult X, and similar tools.

## **Project Advantages**

- **Official Data Source:** All data is directly fetched from MaxMind, ensuring trust and security;
- **Automated Updates:** GitHub Actions pulls the latest data every 3 days to maintain synchronization;
- **License Compliance:** The project uses GitHub Actions to fetch MaxMind data in accordance with the [GeoLite2 EULA](https://www.maxmind.com/en/geolite2/eula). Users are strongly encouraged to apply for their own License Key to ensure legal, secure, and traceable data usage.
- **Customizable & Controllable:** Users can configure output paths, update frequency, target branches, and other parameters to suit their specific deployment needs.

### **Automated Updates**

This project utilizes GitHub Actions for scheduled updates, pulling the latest database every 3 days. No manual intervention is required.

## **File Path**

| **Filename** | **Build Output Path (for reference only)**                   | **Example Usage**                                        |
| ------------ | ------------------------------------------------------------ | -------------------------------------------------------- |
| Country.mmdb | [data/Country.mmdb](https://raw.githubusercontent.com/Thoseyearsbrian/GeoIP2-Country/main/data/GeoLite2-Country.mmdb) | Used in Surge, Clash, QuantumultX for identifying Country IPs |

## **Configuration Guide**

Configure MaxMind License Key (Required)

This project requires access to the official MaxMind GeoLite2 database. To enable automated updates, you must:

1. Register on [MaxMind](https://www.maxmind.com) and obtain your GeoLite2 License Key

2. Open your repository: GitHub → Settings → Secrets and variables → Actions

3. Create the following Secrets (names must match exactly):

- MAXMIND_ACCOUNT_ID      # Your MaxMind Account ID  (Required)
- MAXMIND_LICENSE_KEY     # Your MaxMind License Key (Required)

## **Usage Guide**

Copy the file URL → Open Surge → Go to General → GeoIP Database → Remove previous configuration (if any) → Paste the new URL → Update Now → Apply → Done!

<p align="center">
  <img src="https://raw.githubusercontent.com/Thoseyearsbrian/GeoIP2-Country/main/Icons/Groups/surge-geoip-config-guide-step-by-step-en.png" width="600">
</p>

## **⚠️ Important Notes**

1. **In this project, only manual commits (made by real developers) are signed with a GPG key.**

   Automated updates (such as GeoLite2 database updates) are executed via GitHub Actions and **do not use GPG signatures**. Please verify the committer as [`github-actions[bot]`](https://github.com/apps/github-actions) to consider the commit valid and trustworthy.

   - Manual commits are still GPG-signed to identify the authentic developer  
   - We do **not recommend** storing any GPG private keys on GitHub to prevent key leakage and signature abuse

2. **It is recommended to combine `China.list` (for domains) with `GEOIP,CN` (for IP ranges) to improve accuracy when matching China-related traffic:**

       RULE-SET,https://raw.githubusercontent.com/Thoseyearsbrian/Aegis/main/rules/China.list, DIRECT   # Accurately match domains related to China
       GEOIP,CN,DIRECT                                                                                  # Match mainland China IPs not covered by domain rules
       FINAL,REJECT                                                                                     # Final default reject rule (do not place GEOIP below this)

3. **The GeoLite2-Country database generated by this project can be used for GEOIP queries (such as US, AU, CN), as it provides a complete country-level IP range structure.**

       GEOIP, US, PROXY   # Valid
       GEOIP, AU, PROXY   # Valid
       GEOIP, CN, DIRECT  # Valid

## **🔐 Disclaimer**

The .mmdb file generated by this project is intended **for testing and educational purposes only**. It must **not be used in any form of commercial activity**.

Users are solely responsible for ensuring compliance with the [MaxMind GeoLite2 EULA](https://www.maxmind.com/en/geolite2/eula) and applicable laws and regulations. **This project accepts no legal liability for any use of the data.**

This project **only provides the logic and scripts for building the database** and does not distribute original MaxMind data. Users are strongly advised to apply for their own License Key directly from MaxMind.

This project is **intended for developers with a technical background and awareness of licensing requirements**.

## **🏅 License Notice**

- The .mmdb file built through this project is for research and educational use only. Please read and comply with the [MaxMind EULA](https://www.maxmind.com/en/geolite2/eula). **This project assumes no responsibility for your use case.**

- This project uses GitHub Actions to automatically pull data from MaxMind. **You must register on MaxMind and obtain your own License Key** to run the build script or automation legally.
- GeoLite2 data is copyrighted by [MaxMind, Inc.](https://www.maxmind.com/) and is licensed under the [GeoLite2 EULA](https://www.maxmind.com/en/geolite2/eula).
- All scripts and configuration files in this project are licensed under the [Apache License 2.0](https://raw.githubusercontent.com/Thoseyearsbrian/GeoIP2-Country/main/LICENSE).
