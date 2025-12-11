# 新增功能说明

## 1. 我的页面 (`/my`)

### 功能特性
- **学习笔记管理**：记录和整理学习内容
- **统计信息**：显示总学习天数、笔记数量、收藏数量
- **笔记分类**：支持标签分类，方便查找
- **收藏内容**：查看收藏的药材、药膳、病症

### 主要功能
- ✅ 添加学习笔记（标题、内容、标签）
- ✅ 编辑和删除笔记
- ✅ 时间线展示笔记
- ✅ 本地存储，数据持久化

## 2. 锻炼记录页面 (`/exercise`)

### 功能特性
- **锻炼记录**：记录每次锻炼的详细信息
- **本周统计**：自动统计本周锻炼时长和次数
- **多维度筛选**：按全部/本周/本月查看记录
- **锻炼类型**：支持多种运动类型（跑步、游泳、瑜伽等）

### 主要功能
- ✅ 记录锻炼类型、时长、强度
- ✅ 添加备注信息
- ✅ 时间线展示历史记录
- ✅ 本周统计自动计算
- ✅ 本地存储，数据持久化

## 3. 健康管理页面 (`/health`)

### 功能特性
- **AI 健康助手**：智能问答，提供健康建议
- **健康记录**：记录生病、不适、体检等情况
- **智能分析**：AI 根据健康记录给出建议
- **快速提问**：预设常见问题快速提问

### 主要功能
- ✅ AI 聊天对话（支持模拟回复）
- ✅ 记录健康情况（生病、不适、体检、用药等）
- ✅ 编辑和删除健康记录
- ✅ 聊天历史保存
- ✅ 本地存储，数据持久化

### AI 功能说明
- 当前使用模拟 AI 回复（基于关键词匹配）
- 支持接入真实 AI API（如 OpenAI、百度文心等）
- AI 可以分析健康记录并给出建议
- 支持上下文对话

## API 接口

### 学习相关 (`/api/learning`)
- `GET /api/learning/notes` - 获取笔记列表
- `POST /api/learning/notes` - 创建笔记
- `PUT /api/learning/notes/:id` - 更新笔记
- `DELETE /api/learning/notes/:id` - 删除笔记

### 锻炼相关 (`/api/exercise`)
- `GET /api/exercise/records` - 获取锻炼记录
- `POST /api/exercise/records` - 创建记录
- `PUT /api/exercise/records/:id` - 更新记录
- `DELETE /api/exercise/records/:id` - 删除记录
- `GET /api/exercise/statistics` - 获取统计数据

### 健康相关 (`/api/health`)
- `GET /api/health/records` - 获取健康记录
- `POST /api/health/records` - 创建记录
- `PUT /api/health/records/:id` - 更新记录
- `DELETE /api/health/records/:id` - 删除记录

### AI 相关 (`/api/ai`)
- `POST /api/ai/chat` - AI 聊天
- `POST /api/ai/analyze` - AI 健康分析

## 接入真实 AI API

要接入真实的 AI API，需要修改 `src/api/health.ts` 中的 `aiApi.chat` 方法：

```typescript
// 示例：接入 OpenAI
export const aiApi = {
  chat: async (message: string, healthRecords: HealthRecord[]): Promise<string> => {
    const response = await fetch('https://api.openai.com/v1/chat/completions', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': `Bearer ${YOUR_API_KEY}`,
      },
      body: JSON.stringify({
        model: 'gpt-3.5-turbo',
        messages: [
          {
            role: 'system',
            content: '你是一个专业的中医健康助手，可以根据用户的健康记录提供建议。',
          },
          {
            role: 'user',
            content: message,
          },
        ],
      }),
    })
    const data = await response.json()
    return data.choices[0].message.content
  },
}
```

## 数据存储

- 所有数据默认使用 `localStorage` 进行本地存储
- 后端 API 可用时，会自动同步到服务器
- 数据格式为 JSON，便于迁移和备份

## 使用说明

1. **我的页面**：点击导航栏"我的"，可以添加学习笔记，查看收藏内容
2. **锻炼记录**：点击导航栏"锻炼记录"，记录每次锻炼的详细信息
3. **健康管理**：点击导航栏"健康管理"，使用 AI 助手问答，记录健康情况

所有功能都支持响应式设计，可以在手机和电脑上正常使用。

