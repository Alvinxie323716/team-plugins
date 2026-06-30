# team-plugins — 团队技能市场

集中收录团队成员的 Claude Code 技能插件。使用者添加这一个市场，即可安装其中所有插件；每个插件各自从作者自己的源仓库**自动更新**。

## 📦 使用者：安装

```
/plugin marketplace add Alvinxie323716/team-plugins
/plugin install drug-marketing-strategy@team-plugins
```

安装后重启 Claude Code（或 `/reload-plugins`）。可在 `/plugin` 菜单里查看市场内的全部插件并按需安装。

## 🔄 开启自动更新（建议开一次）

`/plugin` → **Marketplaces** 标签 → 选中 `team-plugins` → **Enable auto-update**。
开启后每次启动会自动拉取各插件的最新版。

## 👥 作者：把你的技能加入本市场

详细步骤见 [CONTRIBUTING.md](./CONTRIBUTING.md)。简述：给你的技能仓库加一个 `.claude-plugin/plugin.json`，然后把仓库 HTTPS 地址和技能名发给维护者（@Alvinxie323716）登记即可。之后你只管往**自己的仓库** push，使用者（开了自动更新的）即可收到更新——无需改动本市场仓库。
