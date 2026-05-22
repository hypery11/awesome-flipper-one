# Awesome Flipper One [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> Curated resources for [Flipper One](https://blog.flipper.net/flipper-one-we-need-your-help/) — Flipper Devices' open-source portable Linux multi-tool, currently in active community-driven development.

Flipper One is **not the same device as Flipper Zero**. Where Flipper Zero focuses on offline radio protocols (NFC, RFID, Sub-1 GHz), Flipper One is a network-layer tool built around a Rockchip RK3576 SoC, a Raspberry Pi RP2350 co-processor, a 7-inch touchscreen, dual Gigabit Ethernet, Wi-Fi 6E, and an M.2 slot. The hardware isn't shipping yet and the team has called for community contributions across seven sub-projects.

This list tracks what's currently public, what's being worked on, and where to plug in.

## Contents

- [Official resources](#official-resources)
- [Sub-projects](#sub-projects)
- [Hardware](#hardware)
- [Boot, kernel, and userspace](#boot-kernel-and-userspace)
- [MCU firmware](#mcu-firmware)
- [Testing and developer tooling](#testing-and-developer-tooling)
- [Adjacent ecosystems](#adjacent-ecosystems)
- [Community](#community)
- [Articles and announcements](#articles-and-announcements)
- [Contributing to this list](#contributing-to-this-list)

## Official resources

- [Developer portal](https://docs.flipper.net/one) - The canonical entry point. Start here.
- [Open tasks](https://docs.flipper.net/one/open-tasks) - Auto-generated from `help wanted` issues across all sub-project repos. Refreshed by CI in the docs repo.
- [Tech specs](https://docs.flipper.net/one/general/tech-specs) - RK3576, RP2350, MT7921AUN, M.2 Key-B (S3), display, battery, ports.
- [How to join](https://docs.flipper.net/one/how-to-join) - Recommended reading before opening your first PR.
- [Project organisation on GitHub](https://github.com/orgs/flipperdevices/projects) - Each sub-project has its own Kanban.

## Sub-projects

Development is split across seven GitHub repositories. Each has its own Kanban, contribution guide, and `help wanted` queue.

| Area | Repo | Kanban |
|---|---|---|
| 🔌 Hardware | [flipperone-hardware](https://github.com/flipperdevices/flipperone-hardware) | [board #9](https://github.com/orgs/flipperdevices/projects/9) |
| ⚙️ Mechanics | [flipperone-mechanics](https://github.com/flipperdevices/flipperone-mechanics) | [board #15](https://github.com/orgs/flipperdevices/projects/15) |
| 🐧 Linux (CPU software) | [flipperone-linux-build-scripts](https://github.com/flipperdevices/flipperone-linux-build-scripts) | [board #11](https://github.com/orgs/flipperdevices/projects/11) |
| 🕹️ MCU firmware | [flipperone-mcu-firmware](https://github.com/flipperdevices/flipperone-mcu-firmware) | [board #8](https://github.com/orgs/flipperdevices/projects/8) |
| 🎨 User interface | [flipperone-ui](https://github.com/flipperdevices/flipperone-ui) | [board #12](https://github.com/orgs/flipperdevices/projects/12) |
| 🧪 Testing | [flipperone-testing](https://github.com/flipperdevices/flipperone-testing) | [board #14](https://github.com/orgs/flipperdevices/projects/14) |
| 📚 Docs | [flipperone-docs](https://github.com/flipperdevices/flipperone-docs) | [board #10](https://github.com/orgs/flipperdevices/projects/10) |

## Hardware

### Application processor

- [Rockchip RK3576 brief datasheet (PDF)](https://cdn.flipper.net/RK3576-Brief-Datasheet-V1.2-20240311.pdf) - Hosted by Flipper. Use this as the working reference until something more complete is published.
- [Collabora RK3576 mainline status](https://gitlab.collabora.com/hardware-enablement/rockchip-3588/notes-for-rockchip-3576/-/blob/main/mainline-status.md) - Tracks which RK3576 subsystems are mainlined upstream. The single most useful file for anyone working on the Linux side.

### Co-processor

- [RP2350 datasheet (Raspberry Pi)](https://datasheets.raspberrypi.com/rp2350/rp2350-datasheet.pdf) - Used for power management, display, buttons, touchpad, LEDs.

### Pinout and connectors

- [GPIO port docs](https://docs.flipper.net/one/hardware/gpio-port) - Pin-by-pin functions.
- [M.2 port docs](https://docs.flipper.net/one/hardware/m2-port) - Key-B (S3), USB 3.0 + PCIe 2.1 ×1, supports 30×52 and 30×42 modules.
- [GPIO module examples](https://docs.flipper.net/one/hardware/gpio-port/modules) - Reference designs for community-built modules.

### Wireless

- MediaTek MT7921AUN - Wi-Fi 6E + Bluetooth combo. The team has noted they're still validating this choice and welcome alternative chip suggestions in the [help-wanted Wi-Fi testing thread](https://docs.flipper.net/one/hardware/wifi-bluetooth).

## Boot, kernel, and userspace

- [RK3576 boot flow](https://docs.flipper.net/one/resources/rockchip/boot-flow) - On-chip ROM → RKNS → FIT → U-Boot → Linux. Flash offsets and what lives where.
- [RK3576 mainlining](https://docs.flipper.net/one/cpu-software/rk3576-mainlining) - Why Flipper One targets mainline-first instead of vendor BSP, and what that means for component support.
- [Flipper One Linux kernel fork](https://github.com/flipperdevices/flipper-linux-kernel) - Flipper-specific patches on top of mainline.
- [Flipper One U-Boot fork](https://github.com/flipperdevices/u-boot) - Tracks mainline U-Boot with Flipper-specific board support.
- [How to build the Linux image](https://docs.flipper.net/one/cpu-software/how-to-build-linux-image)
- [Flipper RnD Debian (build scripts for several RK3576 SBCs)](https://github.com/flipperdevices/rk3576-linux-build) - Build pipeline also used for Radxa 4D, ArmSom Sige5, EVB1, Omni3576.

## MCU firmware

- [MCU firmware architecture](https://docs.flipper.net/one/mcu-firmware/architecture)
- [MCU ↔ CPU interconnect](https://docs.flipper.net/one/mcu-firmware/mcu-cpu-interconnect)
- [bsb-protobuf](https://github.com/flipperdevices/bsb-protobuf) - Protocol definitions used for inter-chip communication.
- [fbtng-freertos](https://github.com/flipperdevices/fbtng-freertos) - FreeRTOS port used in the firmware build system.

## Testing and developer tooling

- [flipperone-testing](https://github.com/flipperdevices/flipperone-testing) - Official test-bench scripts. The README is honest about the state: "Dirty vibe-coded tests scripts for Flipper One. To be completely rewrited." Useful entry points:
  - `fake-flipctl` / `fake-flipctl2` - In-browser device emulators (Node.js + websockets). Lets you develop and screenshot UI without real hardware.
  - `temperature/` - Continuous thermal monitoring with Plotly HTML reports. Works on any RK3576 SBC.
  - `cpu/sbc-bench.sh` - Bundled copy of [sbc-bench](https://github.com/ThomasKaiser/sbc-bench), the standard SBC benchmark tool.
- [Archbee starter](https://github.com/Archbee/starter) - Docs are built on Archbee. The official Flipper One developer portal is generated from `flipperone-docs` via Archbee's GitHub integration.

## Adjacent ecosystems

The following aren't Flipper One specifically but are part of the wider Flipper Devices ecosystem and worth knowing about.

- [awesome-flipperzero](https://github.com/djsime1/awesome-flipperzero) - Sister list for Flipper Zero.
- [Flipper Zero firmware](https://github.com/flipperdevices/flipperzero-firmware) - The other Flipper. Shares the `fbt` build tooling that Flipper One inherits parts of.
- [Flipper Zero µFBT](https://github.com/flipperdevices/flipperzero-ufbt) - The micro-fbt CLI. Conceptually a sibling to whatever build tool Flipper One eventually settles on.
- [qFlipper](https://github.com/flipperdevices/qFlipper) - Desktop companion app for Flipper Zero. The Flipper One companion app, when it exists, is likely to share patterns.

## Community

- [Flipper Devices Discord](https://discord.com/invite/flipper) - The `#flipper-one` channel is where most live discussion happens.
- [@Flipper_RND on X](https://x.com/Flipper_RND) - R&D account; this is where Flipper One progress gets announced.
- [Flipper Devices blog](https://blog.flipper.net/) - Long-form posts. Casper-themed: [Casper-flipper-blog-theme](https://github.com/flipperdevices/Casper-flipper-blog-theme).

## Articles and announcements

- [Flipper One. We need your help](https://blog.flipper.net/flipper-one-we-need-your-help/) (May 2026) - The call for community contribution that effectively launched the public development phase. Worth reading in full if you want to understand what the team is asking for.

(Open a PR to add more as they're published.)

## Contributing to this list

This list is intentionally honest about gaps. If a section is short, that usually means there genuinely isn't a lot of public material yet — not that the section is "coming soon".

To add a resource:

1. Open a PR with the addition in the most appropriate section.
2. Format: `- [Name](URL) - One-line description.` (one sentence, period at the end).
3. Keep it about Flipper **One** specifically. Resources that are equally about Flipper Zero belong in [awesome-flipperzero](https://github.com/djsime1/awesome-flipperzero).
4. Prefer primary sources (official docs, vendor datasheets, repos) over secondary write-ups.

## License

[![CC0](https://mirrors.creativecommons.org/presskit/buttons/88x31/svg/cc-zero.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

To the extent possible under law, the contributors to this list have waived all copyright and related or neighbouring rights to this work.
