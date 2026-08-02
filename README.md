# pi-init-template

> opencode `/init` 移植：生成或更新 `AGENTS.md` 的 pi prompt template。

安装后 pi 内输入 `/init`（支持 `/init <focus>`）即可自动分析仓库并生成/更新 AGENTS.md。

## 安装

```bash
# git 方式（GitHub）
pi install git:github.com/elephanttalkheads/pi-init-template

# git 方式（Gitee 镜像）
pi install git:gitee.com/xuhuitalker/pi-init-template

# 本地开发
pi install D:/github-Clone/pi-init-template
```

## 用法

```
/init                          # 生成；若 AGENTS.md 已存在则原地改进
/init 关注类型安全             # 带 focus 约束
/init 完全重写 AGENTS.md       # 强制重写（默认是原地改进）
```

## 与 opencode /init 的差异

| opencode 原版 | 本移植 |
| ---- | ---- |
| `${path}` 运行时注入仓库根 | 模型用 `git rev-parse --show-toplevel` 自定位 |
| `question` 工具向用户提问 | 无交互工具：按最佳假设执行，疑问列在结果末尾 |
| 读取 `opencode.json` 等 | 额外读取 `.pi/`、`.codex/`，并提示 pi 的 AGENTS.md/CLAUDE.md 祖先链机制 |

写作准则（高信号/宁可省略/原地改进）与调研顺序完整保留自原版。

## 许可证

MIT
