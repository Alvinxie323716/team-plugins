# 把你的技能加入团队技能市场（team-plugins）

我们建了一个统一的团队技能市场 `team-plugins`，使用者添加这一个市场就能装上大家的技能，而且每个技能各自从作者自己的仓库**自动更新**。按下面步骤把你的技能接进来。

---

## 作者：3 步接入

**前提**：你的技能已经是一个 GitHub 仓库，根目录有 `SKILL.md`。

### 第 1 步：给仓库加一个 plugin.json

在仓库根目录新建 `.claude-plugin/plugin.json`（按你的技能改 `name` 和 `description`）：

```json
{
  "name": "你的技能名",
  "description": "一句话描述你的技能",
  "author": { "name": "你的GitHub账号" }
}
```

注意：
- `name` 建议和 `SKILL.md` 里的技能名一致，用小写 + 连字符（如 `my-cool-skill`）。
- **`version` 字段不要写**。留空时 Claude Code 会按每次 commit 自动算新版本——你以后只管 push，使用者就能收到更新，无需手动改版本号。
- `SKILL.md` 和脚本/资源**保持在仓库根目录原位**，只新增 `.claude-plugin/` 这个文件夹。

### 第 2 步：（可选）校验 + 推送

```
claude plugin validate .
git add .claude-plugin/plugin.json
git commit -m "Add plugin manifest"
git push
```

看到 `Validation passed` 即可。

### 第 3 步：把两项信息发给市场维护者（@Alvinxie323716）

1. 仓库 HTTPS 地址，形如 `https://github.com/你的账号/你的仓库.git`
2. 你的技能 `name`（和 plugin.json 一致）

登记后，使用者执行 `/plugin install 你的技能名@team-plugins` 即可安装。之后你**只管往自己仓库 push**，使用者（开了自动更新的）下次启动自动收到——无需改动本市场仓库。

---

## 维护者：如何登记一个新技能

在本仓库 `.claude-plugin/marketplace.json` 的 `plugins[]` 数组里追加一条。**`source` 用 `url` 形式**（强制 HTTPS 克隆，避免使用者因未配置 SSH 而安装失败）：

```json
{
  "name": "技能名",
  "description": "一句话描述",
  "source": {
    "source": "url",
    "url": "https://github.com/作者账号/作者仓库.git"
  }
}
```

> 经实测：`source` 用 `github` 形式（`{"source":"github","repo":"..."}`）会默认走 SSH 克隆，未配置 SSH 的机器会失败；改用上面的 `url` 形式即走 HTTPS，所有使用者都能直接安装。

追加后校验并推送：

```
claude plugin validate .
git add .claude-plugin/marketplace.json
git commit -m "Add <技能名> to marketplace"
git push
```
