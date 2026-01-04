# 完美许愿器 (Wish Master)

**“So tell me, what is it you truly desire?”**

完美许愿器是一个基于 Vue 3 + Vite 构建的因果律模拟应用。它不再是传统的抽签程序，而是一个深谙逻辑漏洞的“邪恶灯神”。它利用 DeepSeek API 的强大推理能力，在满足用户愿望的同时，精准指出其中的逻辑漏洞并反馈一个毫无收益的反转现实。

## 🌟 项目亮点

* **逻辑反转**：不同于常规的祝福，系统会以幽默且腹黑的视角钻愿望的漏洞。
* **双重 LLM 校验**：集成内容审核与场景生成，确保合规的同时保证文案质量。
* **契约感视觉**：全新的暗黑系/契约感 UI 设计，沉浸式许愿体验。
* **Serverless 架构**：完全部署于 Cloudflare Pages Functions，零成本维护后端逻辑。
* **因果律屏障**：严格的输入限制（50字符以内），模拟“契约纸张有限”的荒诞感。

## 🛠️ 核心架构

### 前端组件

* **HomeView.vue**：契约主控室，管理从输入到生成的单向因果流。
* **WishInput.vue**：欲望输入端口，支持快捷选择“常见欲望”。
* **StepFlow.vue**：展示审查、寻漏、构建现实的仪式感进度。
* **SignCard.vue**：展示最终达成的“崩坏契约”结果。

### 后端逻辑 (Functions)

* **validateWish.js**：核心网关。
1. 拦截敏感内容（暴力、色情等）。
2. 格式化愿望文本。
3. 调用 LLM 进行逻辑漏洞演绎。



## 📡 API 接口说明

### 核心接口：`/api/validateWish`

**Method**: `POST`

**Description**: 一站式处理愿望审核与结果生成。

**请求体**:

```json
{
  "wish": "我想要点石成金的能力"
}

```

**响应体 (Success)**:

```json
{
  "status": "success",
  "result": {
    "category": "allow",
    "confirmed_wish": "我想要点石成金的能力",
    "scenario": "你的愿望实现了，但由于金价暴跌且你触碰的日常用品都变成了无用的重金属，你最终一贫如洗..."
  },
  "debug_audit": { "..." } // 仅供调试参考
}

```

## 🚀 快速开始

### 1. 克隆与安装

```bash
git clone https://github.com/senzi/wish-master.git
cd wish-master
npm install

```

### 2. 环境配置

在根目录创建 `.dev.vars` 文件：

```env
DEEPSEEK_API_KEY=你的API密钥
DEEPSEEK_API_BASE_URL=https://api.deepseek.com

```

### 3. 本地调试

```bash
# 启动前端开发环境
npm run dev

# 或使用 Wrangler 模拟 Cloudflare 全栈环境
npm run build && npx wrangler pages dev dist --compatibility-date=2024-01-01

```

## ⚠️ 规则声明 (Caveat Emptor)

1. **长度限制**：愿望不得超过 50 字符，否则因果律将崩溃。
2. **违规拦截**：涉及暴力、色情或特定敏感词（如国家名）的愿望将被神隐。
3. **后果自负**：本系统生成的场景纯属逻辑推演，若现实中发生类似反转，概不负责w。

---

© 2026 完美许愿器 | 智慧来源：DeepSeek