---
name: promo-creator-skills
description: 产品宣传片制作总控 skill pack。用于从产品说明、官网或 GitHub 仓库制作 60-90 秒宣传视频，串联 brief、storyboard、asset producer、HyperFrames editor、BGM maker 和 delivery workflow。当用户要做宣传片、产品视频、项目介绍视频、launch video 或开源项目 promo 时使用。
---

# Promo Creator Skills

这是一个 skill pack 入口。优先使用 `promo-workflow` 作为总控；只有当用户明确要求某个阶段时，才单独使用子 skill。

## 子 Skill 路由

| 用户目标 | 使用 |
|---|---|
| 从零做完整宣传片 | `promo-workflow` |
| 只做产品分析和创意简报 | `promo-brief` |
| 已有 brief，要写分镜 | `promo-storyboard` |
| 已有分镜，要准备素材 | `promo-asset-producer` |
| 已有素材，要剪辑渲染 | `promo-editor` |
| 要配乐、BGM、卡点音乐 prompt | `promo-music-maker` |

## 默认工作方式

1. 先输出阶段性 Markdown 文件。
2. 在关键节点暂停，让用户确认方向。
3. 使用真实产品素材和可验证来源，避免只靠泛化装饰。
4. 视频用 HyperFrames/HTML/CSS/GSAP 构建，输出 MP4。
5. BGM 默认走产品宣传片双轨：`Commercial Product Launch` 和 `Clean UI Demo Groove`，不要默认生成泛 ambient 科技垫底音乐。

详细流程见 `promo-workflow/SKILL.md`。
