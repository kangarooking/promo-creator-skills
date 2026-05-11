# Promo Creator Skills

[English](README.md) · 中文

> 把一个产品页面、GitHub 仓库，或者一句粗略产品描述，做成一支真正能交付的宣传片：创意简报、分镜、素材、HyperFrames 剪辑、BGM 设计、交付清单，全链路跑通。

Promo Creator Skills 是一套面向 agent 的产品宣传片制作技能组。它不是“给 AI 一句话，吐一个幻灯片视频”的玩具，而是一条有中间产物、有确认节点、有真实素材、有剪辑节奏、有配乐判断的生产流水线。

```bash
npx skills add kangarooking/promo-creator-skills
```

如果你的 skill runner 不支持 `npx skills add`，可以手动把 `promo-*` 文件夹复制到你的 agent skills 目录。

---

## 案例展示

### WorkBuddy OPC · Commercial Product Launch

更像现代产品发布广告片：有 beat、bass、hook 和 CTA 推进感。适合产品上架、新能力发布、商业展示。

[观看 MP4](demos/workbuddy-commercial-launch.mp4)

<video src="demos/workbuddy-commercial-launch.mp4" controls width="100%"></video>

### WorkBuddy OPC · Clean UI Demo Groove

更像高级软件 UI 演示片：节奏干净，服务界面、卡片矩阵、流程线和时间线卡点。

[观看 MP4](demos/workbuddy-ui-groove.mp4)

<video src="demos/workbuddy-ui-groove.mp4" controls width="100%"></video>

### Cangjie Skill · 开源项目宣传片

一支 90 秒瑞士国际主义风开源项目宣传片。Cangjie Skill 的价值不在于“又一个读书总结工具”，而在于把高价值书籍的方法论编译成 Agent 可以调用的触发条件、执行步骤、边界和测试。好的开源项目不是把 README 录一遍，而是把它真正值得被记住的系统讲清楚。

[观看 MP4](demos/cangjie-skill-promo.mp4)

<video src="demos/cangjie-skill-promo.mp4" controls width="100%"></video>

---

## 它能做什么

| Skill | 职责 | 产物 |
|---|---|---|
| `promo-brief` | 产品研究、卖点提炼、叙事定位 | `01-brief.md` |
| `promo-storyboard` | 逐镜头分镜、画面、文案、动效说明 | `02-storyboard.md` |
| `promo-asset-producer` | 生成素材与真实产品素材规划 | `03-asset-plan.md`, `assets/` |
| `promo-editor` | HyperFrames 剪辑、动效、渲染 | `04-edl.md`, `master-edit.html`, `final/promo.mp4` |
| `promo-music-maker` | BGM 方向、卡点表、Mureka Prompt | `06-music-plan.md`, `assets/bgm/` |
| `promo-workflow` | 串联完整制作流程 | 可交付 run 目录 |

整套流程不是一发入魂，而是把宣传片拆成可检查、可修改、可复用的阶段：

```text
产品 / 仓库 / URL
  -> 创意简报
  -> 逐镜头分镜
  -> 素材计划
  -> 编辑决策表
  -> HyperFrames 主剪辑
  -> BGM 方向和候选
  -> 最终 MP4
  -> 交付清单
```

---

## BGM：不再生成那种“泛科技垫底音乐”

这次专门把 BGM 设计升级了：**Apple 风画面不等于 ambient BGM**。产品宣传片需要节奏、hook、bass movement 和段落变化。

软件产品宣传片默认先走两条已验证方向：

- **Commercial Product Launch**：118 BPM，电子鼓、sidechain bass、明亮 pluck hook，更像产品发布广告片。
- **Clean UI Demo Groove**：112 BPM，syncopated digital percussion、rubbery synth bass、短促 glass-pluck motif，更像高级 UI 演示片。

这样不会再出现多个候选都像 `minimal / ambient / soft pulse / glass ticks` 的问题。

Mureka 生成脚本：

```bash
export MUREKA_API_KEY="..."
export MUREKA_API_URL="https://api.mureka.cn" # 国内站可选

python scripts/mureka.py instrumental \
  --prompt "<validated product-promo BGM prompt>" \
  -n 2 \
  --format mp3 \
  --output outputs/promo-runs/<run-id>/assets/bgm/
```

没有 API key 也可以使用这个 skill 设计 BGM prompt；只有用户明确要求实际生成音乐时才调用 Mureka。

---

## 使用方式

对 agent 说：

```text
用 promo-workflow 给这个 GitHub 仓库做一支 60 秒 Apple 风产品宣传片：
https://github.com/owner/project
```

或者：

```text
用这套 promo skills 给我的 SaaS 做发布视频。先出 brief 和 storyboard，我确认后再继续。
```

如果你已经有素材：

```text
直接用 promo-editor 和 promo-music-maker。我已经有分镜和截图。
```

---

## 仓库结构

```text
promo-creator-skills/
├── promo-brief/              # 产品研究与创意简报
├── promo-storyboard/         # 逐镜头分镜
├── promo-asset-producer/     # 素材生产与素材计划
├── promo-editor/             # HyperFrames 剪辑与渲染
├── promo-music-maker/        # BGM Prompt 与 Mureka 工作流
├── promo-workflow/           # 总控流程
├── references/
│   ├── mureka_prompt_guide.md
│   └── product_promo_bgm_prompting.md
├── scripts/
│   └── mureka.py
└── demos/
    ├── workbuddy-commercial-launch.mp4
    ├── workbuddy-ui-groove.mp4
    └── cangjie-skill-promo.mp4
```

仓库根目录的 `SKILL.md` 是一个轻量入口，方便只识别根 skill 的安装器；具体流程仍然在各个 `promo-*` 子 skill 中。

---

## 环境依赖

- Node.js 22+
- HyperFrames CLI
- FFmpeg
- Python 3.10+
- `requests` Python 包
- 可选：`MUREKA_API_KEY`，用于实际生成 BGM

---

## 设计原则

- **中间文件优先**：每个关键决策先落 Markdown，再进入渲染。
- **真实产品信号优先**：UI 截图、文档、GitHub 数据、品牌素材，优先级高于装饰图。
- **先分镜，后素材**：没有 shot plan 的生图只是烧钱随机数。
- **音乐必须服务画面**：产品片需要 rhythm、hook、bass 和 section contrast。
- **暂停点就是质量控制**：在贵的步骤之前，让用户有机会纠偏。

---

## 边界

- 这是 skill pack，不是托管视频编辑器。
- 最终质量取决于产品素材质量和本地渲染环境。
- Mureka 生成有随机性，建议一次生成 2-3 条，放回视频里看，而不是单独听音频决定。
- 本地完整生产过程放在 `outputs/`，默认不进 git；公开案例放在 `demos/`。

---

## License

MIT.
