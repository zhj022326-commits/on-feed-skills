# on-feed-skills

本仓库收录两个可独立安装的 Agent Skills：

- [`life-archive`](skills/life-archive/)：个人档案与访谈工作流。
- [`video-interactive-learning-lite`](skills/video-interactive-learning-lite/)：《信息流学习机·轻量版》，面向豆包等原生支持从视频链接取得完整文字稿的 Agent，负责质量判断、知识整理和互动教学。

本仓库不包含带视频提取程序的《信息流学习机》完整版。完整版位于 [no-feed-skills](https://github.com/zhj022326-commits/no-feed-skills/tree/main/skills/video-interactive-learning)。

## 安装

### 安装 life-archive

```bash
npx -y skills add zhj022326-commits/on-feed-skills --skill life-archive -g
```

这条命令会把 `life-archive` 安装到 Agent 的用户级技能目录。安装后开启新的会话。

### 安装 video-interactive-learning-lite

```bash
npx -y skills add zhj022326-commits/on-feed-skills --skill video-interactive-learning-lite -g
```

轻量版只有 `SKILL.md` 和互动教学规则，无提取程序或运行依赖。宿主必须原生支持从视频链接取得完整文字稿；若宿主缺少该能力，请使用上面链接中的完整版。豆包若要求上传文件，可将 [`skills/video-interactive-learning-lite/`](skills/video-interactive-learning-lite/) 目录单独打包为 ZIP 导入。

### 非交互安装（后台或无终端环境）

上面的命令适用于有人操作的终端。在脚本、后台任务或无终端环境里，安装工具可能停在“选择 Agent”界面。`npx -y` 只跳过 npx 自身的确认；即使再加安装工具的 `-y`，也不要依赖它替你选择 Agent。请显式指定 `--agent`：

安装到工具支持的全部 Agent：

```bash
npx -y skills add zhj022326-commits/on-feed-skills --skill video-interactive-learning-lite --agent '*' -g
```

只安装到指定 Agent，例如 Cursor：

```bash
npx -y skills add zhj022326-commits/on-feed-skills --skill video-interactive-learning-lite --agent cursor -g
```

安装其他 Skill 时，把 `--skill` 后的名称改为对应目录名。`--agent '*'` 指安装工具支持的 Agent，不代表豆包等所有平台都能通过这条命令安装。

如果 npx 冷启动慢，也可跳过 npx，手动取得仓库：

```bash
git clone --depth 1 https://github.com/zhj022326-commits/on-feed-skills.git
```

随后把 `skills/<skill-name>/` 整个目录复制到目标 Agent 的技能目录；轻量版的 `references/` 也要一起保留。豆包等要求上传文件的平台，应按其导入方式上传轻量版 ZIP。

### 手动安装 life-archive

1. 在本仓库点击 **Code → Download ZIP** 并解压。
2. 将解压目录中的整个 `skills/life-archive/` 文件夹复制到目标 Agent 的技能目录。不要只复制 `SKILL.md`；`references/` 和 `assets/` 也要保留。
3. Codex 默认的用户级位置是 `%USERPROFILE%\.codex\skills\life-archive\`。项目级安装可放在项目的 `.agents/skills/life-archive/`。其他 Agent 请使用其文档指定的技能目录。
4. 确认最终路径中直接包含 `life-archive\SKILL.md`，不要多套一层 `skills/life-archive`；然后重启 Agent 或开启新会话。

### 在豆包工作中使用 life-archive

在豆包工作里通过其技能安装入口引用公开 GitHub 仓库，并选择 `life-archive`。若当前安装方式要求本地文件，则按上面的“手动安装”说明导入 `skills/life-archive/`。安装后在技能列表中显式调用；如果宿主把“选中”与“执行”分成两个动作，需使用它的调用入口。

## life-archive 使用

- 显式空调用：归档当前对话。
- 调用时附加“访谈”：启动人生访谈。

首次调用时可选择输入已有档案的完整路径，或创建新档案。新档案会在所选位置下使用带随机后缀的文件夹名；安装版 `SKILL.md` 保存当前路径，公开仓库不保存个人路径。档案绑定后正常使用不更换路径；用户手动移动档案时，可明确要求重新定位，技能核对档案编号后更新路径。卸载重装并重新初始化可选择旧档案或新档案；单开新对话不会重置位置。云端运行环境必须能访问所选存储位置；它不能自动读写用户电脑上不可访问的本地盘符。

## video-interactive-learning-lite 使用

用户提供视频链接后，宿主取得完整文字稿，Skill 判断稿件是否可用、整理视频中的知识，并按领学、启发、测验、实践、复述五种模式互动教学。内容严重混乱时停止并交还选择权；教学不擅自扩充视频没有的知识。

## life-archive 数据

本仓库只包含 Skill 指令、规则和空白模板，不包含任何个人档案。用户档案应保存在用户自己指定的位置，不要提交到本仓库。

## life-archive 结构

```text
skills/life-archive/
├── SKILL.md
├── agents/openai.yaml
├── references/
└── assets/archive-template/
```

## 许可

本仓库尚未附加开源许可证。发布者需在公开前决定是否授权他人复制、修改和再分发。
