# 李梓琪 · 个人产品集网站

> 最后一次更新：2026-05-29
> 风格基调：磨砂玻璃 (Glassmorphism) × 蓝粉渐变

---

## 一、项目架构

```
personal-site/
├── index.html           ← 单页应用，包含全部 HTML / CSS / JS
├── 个人头像.jpg          ← 个人头像（圆形裁剪）
├── 网站风格.jpg          ← 初始风格参考图（深酒红复古风，已被替换）
├── AI产品经理实习-李梓琪.pdf
├── cankao/              ← 参考图片文件夹
│   ├── 01.jpg ~ 06.jpg
│   └── 参考图片.png      ← 最终风格参考图（磨砂玻璃蓝粉色系）
└── README.md            ← 本文档
```

**核心特征**：单 HTML 文件架构，所有样式、脚本、内容都内聚在 `index.html` 中，无外部构建工具。

---

## 二、本次对话全部改动记录

### 2.1 内容改动

| 改动项 | 文件位置 | 说明 |
|--------|----------|------|
| 添加「硕士」学位信息 | index.html，txt-box .sub | `四川师范大学硕士（省属重点大学）` |
| 移除 Skill 页「零次的内容」 | index.html | 删除了 `.insight-cards` 区块（三个 insight-card 及对应 CSS） |
| 一键复制邮箱按钮 | index.html，首页 .copy-email-wrap | 新增 input + button 组件，点击复制 `2558383953@qq.com` |
| 经历卡片上移 | index.html，.vibe-grid | 调整 `margin-top` 和 `gap`，确保三张经历卡片在页面中完整可见 |
| **头像泡泡效果** | index.html，.photo-box | 鼠标悬停头像时显示6个特质泡泡：极强产品思维、独立开发Agent、两段AI实习、技术驱动决策、Self-Attention落地、学术理论工程化 |
| **邮箱复制优化** | index.html，.copy-email-wrap | 添加圆角边框、粉色按钮样式 |
| **项目板块优化** | index.html，.vibe-grid | 蓝色圆角卡片，简洁展示项目信息 |
| **邮箱图标** | index.html，.mailbox-icon | 页面右下角添加红色邮箱图标，点击可复制邮箱 |
| **导航栏中文** | index.html，.nav-bar | 导航按钮改为中文：首页、项目经验、技能、邮箱 |

### 2.2 风格大改：磨砂玻璃效果

#### 2.2.1 颜色体系 (CSS Variables)

```css
:root{
    --bg:#F8FAFC;           /* 浅色背景 */
    --card-bg:rgba(255,255,255,0.6);  /* 半透明卡片 */
    --accent:#A8C8D8;       /* 蓝色主色调 */
    --accent-pink:#E8B4BC;  /* 粉色点缀 */
    --accent-blue:#7BA7C4;  /* 深蓝色 */
    --radius:12px;          /* 圆角 */
}
```

#### 2.2.2 核心视觉效果

- **磨砂玻璃背景**：使用 `backdrop-filter: blur(20px)` 实现毛玻璃效果
- **蓝色渐变背景**：多层径向渐变模拟磨砂质感
- **圆形头像**：白色边框 + 蓝色阴影
- **装饰泡泡**：圆形半透明装饰元素
- **红色邮箱图标**：CSS 绘制的 3D 邮箱，带有旗帜飘动和信件弹出动画

### 2.2 样式大改：复古拼贴风格

#### 2.2.1 颜色体系 (CSS Variables)

```css
:root{
    --bg:#FFD0CD;           /* 暖粉桃色背景（来自参考图片.png） */
    --card-bg:#FFFFFF;       /* 纯白卡片 */
    --card-border:rgba(0,0,0,0.10);
    --accent:#E8D5C4;        /* 暖米色 */
    --accent-pink:#F4A7B8;   /* 粉色点缀 */
    --accent-blue:#A8C8D8;   /* 蓝色点缀 */
    --ink:#2A1A1A;           /* 深棕文字 */
    --ink-soft:#5A4A4A;
    --ink-light:#9A8A8A;
    --ink-lighter:rgba(0,0,0,0.10);
    --card-ink:#2A1A1A;
    --card-ink-soft:#5A4A4A;
    --card-ink-light:#9A8A8A;
    --radius:0px;            /* 全部直角，契合 cut-out 风格 */
}
```

**颜色演变过程**：
1. **初始状态**：深酒红背景 (`#4A1420`) + 白色文字 — 来自 `网站风格.jpg`
2. **最终状态**：暖粉桃色背景 (`#FFD0CD`) + 深棕文字 — 来自 `cankao/参考图片.png`

#### 2.2.2 背景与质感

- 纯色 `background: var(--bg)` 打底
- 双层径向渐变模拟柔和光晕：
  ```
  background-image:
    radial-gradient(ellipse at 20% 30%, rgba(244,167,184,0.18) 0%, transparent 60%),
    radial-gradient(ellipse at 80% 70%, rgba(168,200,216,0.15) 0%, transparent 60%);
  ```
- SVG 噪点纹理叠加（`body::after`），`opacity: 0.05`

#### 2.2.3 Content Card（核心组件）

所有内容都包裹在 `.content-card` 中：
- 白色背景，`1.5px` 极浅边框
- 柔和阴影 `box-shadow: 0 2px 12px rgba(0,0,0,0.04)`
- 外层 `::before` 做 `1px` 额外描边，营造剪贴画层次感
- 右上角 `::after` 显示 ✁ 剪刀图标，强化 cut-out 意象

#### 2.2.4 装饰元素系统

| 元素 | 符号/样式 | 位置策略 |
|------|-----------|----------|
| retro-deco | `✦` `✧` `◈` `▽` `— 2026 —` | 页面固定定位 |
| retro-star | `✧` `✦` × 4 | 带呼吸动画 `rs` |
| retro-arrow | `→` `←` `↗` `↑` × 5 | 固定定位，多种旋转角度 |
| cut-line | 虚线 `1px dashed` × 3 | 固定定位 |
| pen-nib-deco | `✒` | 顶部居中 |
| gd-tag | `Graphic Designer` | 右下 |

所有装饰元素使用 `rgba(42,26,26,0.07~0.12)` 极低透明度，融为背景的一部分。

#### 2.2.5 导航与交互组件

- **Nav Bar**（右上）：半透明白色毛玻璃 (`rgba(255,255,255,0.7)`)
- **Side Nav**（左右两侧）：半透明背景，hover 加深
- **Bottom Dots**（底部居中）：半透明背景，菱形旋转指示器

#### 2.2.6 卡片与边框系统

所有卡牌类元素（`.vb`, `.exp-card`, `.ec-vid-frame`, `.note-f`, `.video-box` 等）统一使用：
- `border: 1.5px solid rgba(0,0,0,0.08~0.12)`
- `box-shadow: 2~3px 2~3px 0 rgba(0,0,0,0.06~0.08)`
- 无圆角 (`border-radius: 0`)

#### 2.2.7 照片区域（About Me）

- 圆形头像 `120×120`
- 5 个抽象拼接贴片 (`.ap.p1~p5`) 使用 `--accent-pink`, `--accent-blue`, `--accent` 配色
- hover 时贴片旋转归零并放大

### 2.3 其他样式调整

| 元素 | 旧值（深色主题） | 新值（暖色主题） |
|------|-----------------|-----------------|
| body 背景 | `#4A1420` | `#FFD0CD` + 渐变 |
| body 文字色 | `#FFFFFF` | `#2A1A1A` |
| card-bg | `#F5F0E8` | `#FFFFFF` |
| card-border | `rgba(255,255,255,0.18)` | `rgba(0,0,0,0.10)` |
| Nav bar 背景 | `rgba(255,255,255,0.08)` | `rgba(255,255,255,0.7)` |
| 装饰元素颜色 | `rgba(255,255,255,0.05~0.12)` | `rgba(42,26,26,0.07~0.12)` |
| 侧边导航背景 | `rgba(255,255,255,0.06)` | `rgba(255,255,255,0.6)` |
| 底部圆点背景 | `rgba(255,255,255,0.08)` | `rgba(255,255,255,0.6)` |
| Content card 阴影 | `6px 6px 0 rgba(0,0,0,0.15)` | `0 2px 12px rgba(0,0,0,0.04)` |
| 照片头像描边 | `2px solid var(--card-ink)` | `1.5px solid rgba(0,0,0,0.12)` |
| 照片装饰贴片 | `rgba(42,26,26,0.03)` + `var(--card-ink)` | `var(--accent-pink/blue)` + 半透明 |

### 2.4 响应式适配

在 `@media(max-width: 767px)` 和 `@media(max-width: 400px)` 中：
- 缩小头像尺寸 (120px→100px→88px)
- 调整装饰贴片尺寸
- 缩小标题字号 (34px→28px→24px)
- 邮箱复制组件在极窄屏切换为纵向排列
- vibe-grid 切换为单列 (`grid-template-columns: 1fr`)

---

## 三、风格参考来源

| 文件 | 作用 | 使用状态 |
|------|------|----------|
| `cankao/参考图片.png` | **主要风格参考** — 暖粉桃色系，RGB(255,208,205) | ✅ 已作为配色核心 |
| `cankao/01~06.jpg` | 布局与内容区块参考 — 极简清爽、高对比度白色内容区 | ✅ 参考其干净布局 |
| `网站风格.jpg` | 初始风格参考 — 深酒红复古风 | ❌ 已被替换 |

---

## 四、交互功能清单

| 功能 | 触发方式 | 说明 |
|------|----------|------|
| 页面切换 | 点击导航 / 侧边箭头 / 底部圆点 / 键盘方向键 / 触摸滑动 | 4 页轮播 (About / Experience / Skill / Contact) |
| 经历展开/收起 | 点击 `.ec-h` 标题或「展开结果」按钮 | 动画展开 `ec-expand` 区块 |
| Skill 标签弹出动画 | 点击 `.tag` | `pop` 动画 + 随机颜色闪烁 |
| 邮箱一键复制 | 点击「复制」按钮 | `execCommand('copy')` + 2秒视觉反馈 |
| 视频弹窗 | 点击 `.demo-btn` 或 `.ec-vid-frame` | 全屏遮罩 + video-box 弹窗 |
| 键盘导航 | `ArrowDown/Up/Left/Right` | 上下/左右翻页 |
| 触摸滑动 | 上下滑动 > 50px | 移动端翻页 |

---

## 五、关键 JavaScript 函数

```javascript
function goToSec(idx)             // 页面跳转核心函数
function toggleEC(el)             // 经历卡片展开/收起
function copyEmail(btn)           // 一键复制邮箱
function popTag(el)               // 标签弹出动画
function openDemo(e)              // 打开演示视频弹窗
function closeDemo()              // 关闭演示视频弹窗
function updateNav()              // 更新导航栏/圆点高亮状态
```

---

## 六、字体系列

| 用途 | 字体 |
|------|------|
| 正文字体 | `Inter`, `-apple-system`, `PingFang SC` |
| 装饰/手写字体 | `Caveat` (Google Fonts) |
| 图标 | `Font Awesome 6.5.0` (CDN) |

---

## 七、已知注意事项

1. **头像图片**：`个人头像.jpg` 需存在于项目根目录
2. **视频弹窗**：目前为占位符状态 (`v-placeholder`)，需替换为真实视频链接
3. **表单**：留言表单 (`note-f`) 提交触发 `alert`，未接入后端
4. **浏览器兼容**：使用了 `backdrop-filter`（毛玻璃效果），iOS Safari 需要 `-webkit-backdrop-filter`
5. **参考图片**：`cankao/` 目录中的图片仅供风格参考，不参与网站运行时加载

---

## 八、后续可迭代方向

- [ ] 替换视频弹窗中的占位符为真实视频 / YouTube Embed
- [ ] 接入留言表单后端（如 Formspree / 自建 API）
- [ ] 为装饰元素添加更多随机位置/大小变体
- [ ] 添加暗色模式切换（目前仅有暖色模式）
- [ ] 添加作品集图片画廊 (Gallery) 页面