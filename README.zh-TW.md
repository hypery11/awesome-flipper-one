# Awesome Flipper One [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

[English](README.md) | 繁體中文

> 精選 [Flipper One](https://blog.flipper.net/flipper-one-we-need-your-help/) 相關資源。Flipper One 是 Flipper Devices 推出的開源可攜式 Linux 多功能工具，目前正由社群積極參與開發中。

Flipper One **和 Flipper Zero 不是同一台裝置**。Flipper Zero 主打離線無線電協定（NFC、RFID、Sub-1 GHz），Flipper One 則是網路層工具，核心是 Rockchip RK3576 SoC，搭配 Raspberry Pi RP2350 協同處理器、256×144 單色 LCD、雙 Gigabit 乙太網路、Wi-Fi 6E 和 M.2 插槽。硬體還沒出貨，團隊已在七個子專案公開徵求社群貢獻。

這份清單整理目前已公開的內容、正在進行的工作，以及可以從哪裡加入。

## 目錄

- [官方資源](#官方資源)
- [子專案](#子專案)
- [硬體](#硬體)
- [開機、核心與使用者空間](#開機核心與使用者空間)
- [Flipper OS 與 FlipCTL](#flipper-os-與-flipctl)
- [MCU 韌體](#mcu-韌體)
- [測試與開發工具](#測試與開發工具)
- [社群工具](#社群工具)
- [相關生態系](#相關生態系)
- [社群](#社群)
- [文章與公告](#文章與公告)
- [如何貢獻這份清單](#如何貢獻這份清單)

## 官方資源

- [Developer portal](https://docs.flipper.net/one) - 官方入口，從這裡開始。
- [Open tasks](https://docs.flipper.net/one/open-tasks) - 從所有子專案 repo 的 `help wanted` issue 自動產生，由 docs repo 的 CI 定期更新。
- [Tech specs](https://docs.flipper.net/one/general/tech-specs) - RK3576、RP2350、MT7921AUN、M.2 Key-B（S3）、螢幕、電池、連接埠。
- [How to join](https://docs.flipper.net/one/how-to-join) - 送出第一個 PR 前建議先讀。
- [Project organisation on GitHub](https://github.com/orgs/flipperdevices/projects) - 每個子專案都有自己的看板。
- [Dev Log](https://docs.flipper.net/one/dev-log) - 定期的開發進度報告，涵蓋各子專案。第 10 篇說明如何在 Flipper One 出貨前，先在支援的 RK3576 開發板上跑 Flipper OS。
- [Community projects page](https://docs.flipper.net/one/community) - 官方的社群 Flipper One 專案索引，透過對 `flipperone-docs` 發 PR 加入。

## 子專案

開發分成七個 GitHub repo，各有自己的看板、貢獻指南和 `help wanted` 佇列。

| 領域 | Repo | 看板 |
|---|---|---|
| 🔌 硬體 | [flipperone-hardware](https://github.com/flipperdevices/flipperone-hardware) | [board #9](https://github.com/orgs/flipperdevices/projects/9) |
| ⚙️ 機構 | [flipperone-mechanics](https://github.com/flipperdevices/flipperone-mechanics) | [board #15](https://github.com/orgs/flipperdevices/projects/15) |
| 🐧 Linux（CPU 軟體） | [flipperone-linux-build-scripts](https://github.com/flipperdevices/flipperone-linux-build-scripts) | [board #11](https://github.com/orgs/flipperdevices/projects/11) |
| 🕹️ MCU 韌體 | [flipperone-mcu-firmware](https://github.com/flipperdevices/flipperone-mcu-firmware) | [board #8](https://github.com/orgs/flipperdevices/projects/8) |
| 🎨 使用者介面 | [flipperone-ui](https://github.com/flipperdevices/flipperone-ui) | [board #12](https://github.com/orgs/flipperdevices/projects/12) |
| 🧪 測試 | [flipperone-testing](https://github.com/flipperdevices/flipperone-testing) | [board #14](https://github.com/orgs/flipperdevices/projects/14) |
| 📚 文件 | [flipperone-docs](https://github.com/flipperdevices/flipperone-docs) | [board #10](https://github.com/orgs/flipperdevices/projects/10) |

## 硬體

### 應用處理器

- [Rockchip RK3576 brief datasheet (PDF)](https://cdn.flipper.net/RK3576-Brief-Datasheet-V1.2-20240311.pdf) - 由 Flipper 托管。在更完整的資料公開前，先以這份當作參考。
- [Collabora RK3576 mainline status](https://gitlab.collabora.com/hardware-enablement/rockchip-3588/notes-for-rockchip-3576/-/blob/main/mainline-status.md) - 追蹤 RK3576 哪些子系統已併入上游主線。做 Linux 端的人最實用的一份檔案。

### 協同處理器

- [RP2350 datasheet (Raspberry Pi)](https://datasheets.raspberrypi.com/rp2350/rp2350-datasheet.pdf) - 負責電源管理、螢幕、按鍵、觸控板和 LED。

### 腳位與連接器

- [GPIO port docs](https://docs.flipper.net/one/hardware/gpio-port) - 每個腳位的功能。
- [M.2 port docs](https://docs.flipper.net/one/hardware/m2-port) - Key-B（S3），USB 3.0 + PCIe 2.1 ×1，支援 30×52 和 30×42 模組。
- [M.2 modules](https://docs.flipper.net/one/hardware/m2-port/modules) - 可擴充 Flipper One 的市售 M.2 模組類別，另有衛星數據機和 GNSS 接收器子頁面。
- [GPIO module examples](https://docs.flipper.net/one/hardware/gpio-port/modules) - 社群自製模組的參考設計。

### 電源與除錯

- [Power subsystem](https://docs.flipper.net/one/hardware/power-subsystem) - 2 芯鋰離子電池、USB-C1 的 USB PD 充電，以及由 RP2350 控制的 DC/DC 轉換器。
- [Debug Probe docs](https://docs.flipper.net/one/hardware/debug-probe) - 以 RP2350 為核心的除錯器，用排線接到背板後方的除錯埠。
- [flipperone-debug-probe](https://github.com/flipperdevices/flipperone-debug-probe) - Debug Probe 的韌體，CI 會產出 `.uf2` 檔，可用來除錯 MCU 和 CPU。

### 無線

- MediaTek MT7921AUN - Wi-Fi 6E + 藍牙二合一晶片。團隊表示仍在驗證這個選擇，歡迎在 [help-wanted Wi-Fi testing thread](https://docs.flipper.net/one/hardware/wifi-bluetooth) 提出其他晶片建議。

## 開機、核心與使用者空間

- [RK3576 boot flow](https://docs.flipper.net/one/hardware/rk3576/boot-flow) - 晶片內 ROM → RKNS → FIT → U-Boot → Linux，以及 flash 偏移位址和各段內容。
- [RK3576 mainlining](https://docs.flipper.net/one/cpu-software/rk3576-mainlining) - 為什麼 Flipper One 優先走主線而不是原廠 BSP，以及這對元件支援的影響。
- [Flipper One Linux kernel fork](https://github.com/flipperdevices/flipper-linux-kernel) - 在主線之上加入 Flipper 專屬修補。
- [Flipper One U-Boot fork](https://github.com/flipperdevices/u-boot) - 追隨主線 U-Boot，並加入 Flipper 專屬的板級支援。
- [How to build the Linux image](https://docs.flipper.net/one/cpu-software/how-to-build-linux-image)
- [How to install a Linux image](https://docs.flipper.net/one/cpu-software/how-to-install-linux-image) - 用裝置上的安裝程式或手動燒錄，把 Flipper OS 裝到 microSD 或 UFS。
- [Supported boards](https://docs.flipper.net/one/cpu-software/supported-boards) - 可執行官方 Flipper OS 映像的 RK3576 開發板，附 target 名稱、開機優先順序和 MaskROM 操作說明。
- [Rockchip MaskROM mode](https://docs.flipper.net/one/cpu-software/maskrom-mode) - RK3576 如何選擇開機裝置，以及如何透過 USB 燒錄。

## Flipper OS 與 FlipCTL

- [Flipper OS docs](https://docs.flipper.net/one/cpu-software/flipper-os) - Flipper OS 的設計概念：在 Debian 之上可切換的 OS 設定檔（profile）。
- [FlipCTL docs](https://docs.flipper.net/one/cpu-software/flipctl) - 驅動裝置螢幕、網頁瀏覽器和 SSH 控制介面的 UI 框架。
- [flipctl](https://github.com/flipperdevices/flipctl) - FlipCTL 原始碼：後端包裝 systemd、網路設定和命令列工具，前端用 HTML/JS。
- [flipctl-slint](https://github.com/flipperdevices/flipctl-slint) - 用 Slint 實作的 Flipper One UI，給 256×144 SPI 面板使用，安裝程式和開機選單共用。
- [flipctl-fonts](https://github.com/flipperdevices/flipctl-fonts) - 為 FlipCTL UI 調整過的像素字型。
- [flipctl-apps](https://github.com/flipperdevices/flipctl-apps) - Flipper One 應用程式管理器可安裝之 App 的目錄（`apps.toml`）與發行下載，例如測試工具、瀏覽器與遊戲。
- [flipperos-installer](https://github.com/flipperdevices/flipperos-installer) - 從 initramfs 執行、把 Flipper OS 裝到 RK3576 開發板上的 Rust 安裝程式，有 TUI 和螢幕 GUI。
- [flipperos-installer-initramfs](https://github.com/flipperdevices/flipperos-installer-initramfs) - 產生執行安裝程式所需 initramfs 的 Buildroot 配方。
- [flipperos-boot-menu](https://github.com/flipperdevices/flipperos-boot-menu) - Buildroot initramfs，在螢幕上列出可開機的設定檔，再用 kexec 進入選中的那一個。
- [flipperos-recovery](https://github.com/flipperdevices/flipperos-recovery) - 最小化、不可變的救援 initramfs，完全在 RAM 中執行，因此可以重新燒錄儲存裝置。
- [flipperos-btrfs-tools](https://github.com/flipperdevices/flipperos-btrfs-tools) - 管理 btrfs OS 設定檔、快照和 BLS 開機項目的 POSIX sh 工具。

## MCU 韌體

- [MCU firmware architecture](https://docs.flipper.net/one/mcu-firmware/architecture)
- [MCU ↔ CPU interconnect](https://docs.flipper.net/one/mcu-firmware/mcu-cpu-interconnect)
- [How to build firmware](https://docs.flipper.net/one/mcu-firmware/how-to-build-firmware) - 從原始碼編出 MCU 的 `.uf2`，再透過 USB 上傳。
- [flipperone-mcu-protobuf](https://github.com/flipperdevices/flipperone-mcu-protobuf) - MCU RPC 協定的 protobuf 定義，MCU 韌體以 submodule 引用。
- [fbtng-corelibs](https://github.com/flipperdevices/fbtng-corelibs) - MCU 韌體中以 `lib/corelibs` 引入的核心函式庫。

## 測試與開發工具

- [flipperone-testing](https://github.com/flipperdevices/flipperone-testing) - 官方測試腳本。README 對現況很坦白：「Dirty vibe-coded tests scripts for Flipper One. To be completely rewrited.」實用入口：
  - `fake-flipctl` / `fake-flipctl2` - 瀏覽器內的裝置模擬器（Node.js + websockets），沒有實機也能開發 UI 和截圖。
  - `temperature/` - 持續監測溫度並輸出 Plotly HTML 報告，任何 RK3576 開發板都能用。
  - `cpu/sbc-bench.sh` - 內附 [sbc-bench](https://github.com/ThomasKaiser/sbc-bench)，常用的開發板效能測試工具。
- [Archbee starter](https://github.com/Archbee/starter) - 文件建置在 Archbee 上。官方 Flipper One 開發者入口網站是透過 Archbee 的 GitHub 整合，從 `flipperone-docs` 產生。

## 社群工具

- [Flipper One Pinout](https://hypery11.github.io/flipper-one-pinout/) - GPIO 排針和 M.2 埠的互動式檢視器。點選腳位可看功能，GPIO 腳位還能看替代功能的 mux 設定；可依協定篩選（I²C、UART、SPI、SAI、PCIe、SIM 等）。原始碼：[`hypery11/flipper-one-pinout`](https://github.com/hypery11/flipper-one-pinout)。*（揭露：本清單維護者的作品。）*
- [Flipper One Lab](https://github.com/kalicyh/flipperone-lab) - 容器映像，可在桌機瀏覽器中執行公開的使用者空間和 `fake-flipctl2` UI 測試環境。已列在官方社群頁面。
- [QEMU Flipper OS](https://github.com/Gelules/qemu-flipperos) - 在 Linux PC 上用 QEMU 開機官方 Flipper OS 建置的腳本，FlipCTL 在瀏覽器中顯示。
- [Bad Apple!! on Flipper One](https://github.com/Gelules/flipperone-bad-apple) - 兩個在 256×144 面板上播放 Bad Apple!! 的 Python FlipCTL App（灰階與 1-bit），目前在 QEMU 中測試。
- [Flipper One VM](https://github.com/plusmalias/flipper-one-vm) - 在 Intel Mac 上用 QEMU 執行官方 Flipper OS 映像，附即時前面板 UI 和 SSH。
- [Flipper One Mac Demo](https://github.com/Nirbhik-Acharya-official/flipper-one-mac-demo) - 非官方 Apple Silicon App，在本機 VM 開機 Flipper OS，並在 macOS 視窗中顯示 FlipCTL。
- [flipper-profile](https://github.com/NetVar1337/flipper-profile) - btrfs + overlayfs 的 OS 設定檔管理工具，是 `flipperone-linux-build-scripts` 一項 RFC 的實作版本。
- [flipper-os-lab](https://github.com/xbizzybone/flipper-os-lab) - Flipper OS 儲存架構 RFC 的本機概念驗證（squashfs + dm-verity，以及全 Btrfs 的替代方案）。
- [RK3576 Open LPDDR4X DDR Trainer](https://github.com/kendun555-svg/ddr-trainer) - 社群嘗試做出開源 DDR trainer，取代開機流程中封閉的 RK3576 DDR blob。

## 相關生態系

以下不是 Flipper One 專屬，但屬於更廣的 Flipper Devices 生態系，值得認識。

- [awesome-flipperzero](https://github.com/djsime1/awesome-flipperzero) - Flipper Zero 的姊妹清單。
- [Flipper Zero firmware](https://github.com/flipperdevices/flipperzero-firmware) - 另一台 Flipper。共用 `fbt` 建置工具，Flipper One 沿用了其中一部分。
- [Flipper Zero µFBT](https://github.com/flipperdevices/flipperzero-ufbt) - micro-fbt 命令列工具。概念上和 Flipper One 未來採用的建置工具是同一類。
- [qFlipper](https://github.com/flipperdevices/qFlipper) - Flipper Zero 的桌面配套 App。Flipper One 的配套 App 推出時，很可能會沿用類似模式。

## 社群

- [Flipper Devices Discord](https://discord.com/invite/flipper) - 大部分即時討論都在 `#flipper-one` 頻道。
- [@Flipper_RND on X](https://x.com/Flipper_RND) - 研發帳號，Flipper One 的進度會在這裡公布。
- [Flipper Devices blog](https://blog.flipper.net/) - 長篇文章。佈景主題基於 Casper：[Casper-flipper-blog-theme](https://github.com/flipperdevices/Casper-flipper-blog-theme)。

## 文章與公告

- [Flipper OS — the operating system for Flipper One](https://blog.flipper.net/flipper-os-the-operating-system-for-flipper-one/)（2026 年 8 月） - Flipper OS 是 Debian 之上的一層，可在預先設定好的系統設定檔之間切換。
- [FlipCTL — Our GUI Framework for Embedded Linux Systems](https://blog.flipper.net/flipctl-our-gui-framework-for-embedded-linux-systems/)（2026 年 6 月） - 為什麼 Flipper One 需要內建 UI，以及 FlipCTL 的運作方式。
- [Flipper One. We need your help](https://blog.flipper.net/flipper-one-we-need-your-help/)（2026 年 5 月） - 號召社群參與的文章，實質上開啟了公開開發階段。想了解團隊需要什麼幫助，值得從頭讀完。

（有新文章發布時，歡迎發 PR 補上。）

## 如何貢獻這份清單

這份清單會老實呈現缺口。某個章節內容少，通常代表公開資料真的不多，而不是「即將推出」。

新增資源的方式：

1. 發 PR，把資源加到最合適的章節。
2. 格式：`- [Name](URL) - One-line description.`（一句話，句尾加句號）。
3. 只收 Flipper **One** 專屬的資源。同樣適用 Flipper Zero 的資源請放到 [awesome-flipperzero](https://github.com/djsime1/awesome-flipperzero)。
4. 優先收第一手來源（官方文件、廠商 datasheet、repo），而不是二手整理。

## 授權

[![CC0](https://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

在法律允許的範圍內，本清單的貢獻者已放棄對本作品的所有著作權及相關權利。
