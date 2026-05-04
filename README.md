# PartyKeys Lessons

> 音乐版 Duolingo · 为 PartyKeys 36 Keys MIDI 键盘设计的零基础乐理课
> Production: <https://lessons.partykeys.org>

---

## 项目结构

```
PartyKeysLessons/
├── index.html          ← 单文件 SPA，包含全部 HTML/CSS/JS/SVG
├── favicon.svg         ← 鸣鸣 favicon
├── vercel.json         ← 静态站点配置 + cache headers + Permissions-Policy(midi=self)
├── robots.txt          ← 允许所有爬虫
├── sitemap.xml         ← 单页站点地图
├── .gitignore
└── README.md
```

零依赖、零构建。`index.html` 直接双击就能在 Chrome 打开本地试玩。

---

## MVP 范围（v0.1）

40 关大纲设计完整，**首批实装 7 关**：

| 模块 | 关卡 | 题型 |
|------|------|------|
| 入门 0.1 | 你好 PartyKeys | T_ANY |
| 入门 0.2 | 灯告诉你弹哪 | T1 |
| 入门 0.3 | 错了灯会变红 | T1 |
| 入门 0.4 | 第一次小演奏（小星星） | T8 |
| 旋律 1.1 | C D E 三兄弟 | T1 + T3 |
| 旋律 1.2 | 凑齐七个白键 | T1 + T7 |
| 旋律 1.3 | 高八度也叫 C | T1 + T2 + T3 |

题型组件（5 种）：
- **T1** 照亮弹 — 看 LED 弹对应键
- **T2** 听后弹 — 听音回弹
- **T3** 听辨四选一 — 听音选答案
- **T7** 序列复现 — Simon Says
- **T8** 小演奏 — 完整弹一段（带 LED 半提示）

---

## 全套机制

- 顶栏：**3 颗爱心** + 🔥 Streak + ✦ XP + Lv 等级
- 路径地图：Duolingo 竖向 S 弯，SVG path 真实曲线
- 错题 3 次：儿童模式自动 LED 演示，成人模式扣心
- 满分 3 星：触发撒花动画
- localStorage 自动存档（key: `pk_lessons_v1`）
- 中英双语：`data-i18n` 全套切换
- 双语气：🧒 卡通拟人 vs 🧑 简洁说明

---

## 技术细节

- **MIDI 输入**：Web MIDI API，过滤 `/partykey/i` 设备名
- **LED 输出**：SysEx 协议（需固件 v007+）
  - 初始化：`F0 05 30 7F 7F 20 00 0F 05 F7`
  - 点亮：`F0 05 30 7F 7F 20 00 71 [count] [note color]... F7`
  - 全关：`F0 05 30 7F 7F 20 00 71 00 F7`
- **音频**：Web Audio API，4 谐波合成钢琴
- **键盘**：PartyKeys 36 键，MIDI 48-83（C3-B5）
- **降级**：无设备时显示 gate 页 + 屏幕键盘 fallback

LED 颜色语义（贯穿所有课）：
| 颜色 | 含义 |
|------|------|
| 🟢 green 0x07 | 该弹这个键 / 弹对了 |
| 🟡 yellow 0x05 | 候选键 |
| 🔵 blue 0x09 | 当前节拍 |
| 🟣 purple 0x0C | 和弦根音 |
| 🟠 orange 0x03 | 和弦三音 |
| 🩵 cyan 0x08 | 已听过的参考音 |
| 🔴 red 0x01 | 弹错了 |

---

## 视觉风格

Duolingo 明亮卡通 + Apple Music 多层柔阴影 + Linear 极简单线
- 字体：Plus Jakarta Sans 800/700/600/500 + DM Mono 500
- 背景：暖米 #FBF9F2，不用纯白
- 主色：草绿 #58CC02 / 错误红 #FF4B4B / Streak 橙 #FF9600 / 等级紫 #A560E8
- 鸣鸣：渐变绿身体 + 紫色头戴耳机 + 腮红 + 4 表情（happy/scratch/sleep/dance）

---

## 浏览器要求

- Chrome ≥ 105 / Edge ≥ 105 / Opera ≥ 91
- Safari、Firefox **不支持** Web MIDI（会显示 gate 页）
- 移动端：iOS Safari 不支持 Web MIDI；Android Chrome 支持

---

## 后续路线（v0.2+）

- 和弦模块 10 关（顺阶 / I-IV-V / I-V-vi-IV / 12 小节布鲁斯 / ii-V-I）
- 节奏模块 10 关（拍子 / 节奏型 / 多声部）
- 综合能力 6 关（视奏 / 听写 / 完整《小星星》）
- 题型 T4 找错音 / T5 填空 / T6 节奏拍
- 复习关算法（Duolingo 式错题回放）
- v2：账号系统 + 云存档（先 MVP，再考虑）

---

## License

© 2026 视感科技 PartyKeys. All rights reserved.
