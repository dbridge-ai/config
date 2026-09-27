# dbridge-ai/config

DBridge 配置源仓库（三平台镜像：GitHub / Gitee / GitCode）。

本仓库存储 DBridge 自动更新所需的**配置文档**（更新清单、源列表、公钥声明、迁移 SQL），由 CI 发布流水线自动生成并同步（见 `dbridge-desktop` 的 `desktop-release.yml` 阶段 4，设计文档 `docs/pr59-design.md`）。

## 结构

```
.
├── sources.json          # 全局源列表（含三平台地址，含签名 sources.json.sig）
├── keys.json             # 公钥声明（含签名 keys.json.sig）
├── stable/               # stable 通道
│   ├── latest.json       #   最新版本清单（含签名 latest.json.sig）
│   ├── checksums.txt     #   制品 sha256 校验和
│   └── migrations/       #   迁移脚本（v{X}/migrate.sql + manifest.json）
└── beta/                 # beta 通道（结构同 stable）
```

## 三平台地址

| 平台 | 仓库 | raw 前缀 |
|------|------|---------|
| GitHub | `github.com/dbridge-ai/config` | `https://raw.githubusercontent.com/dbridge-ai/config/main/` |
| Gitee | `gitee.com/dbridge-ai/config` | `https://gitee.com/dbridge-ai/config/raw/main/` |
| GitCode | `gitcode.com/dbridge-ai/config` | `https://gitcode.com/dbridge-ai/config/raw/main/` |

## 安全

- 本仓库内容全部由发布流水线用 Ed25519 私钥签名（私钥仅存于 CI Secret，不入库）；
- 客户端使用编译期注入的公钥环验签；
- 请勿手工修改 `latest.json` / `sources.json` 等签名文件，否则签名失效。
