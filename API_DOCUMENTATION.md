# API 接口文档

## 基础信息

- **基础URL**: `http://localhost:8080/api` (可通过环境变量 `VITE_API_BASE_URL` 配置)
- **请求格式**: JSON
- **响应格式**: JSON
- **认证方式**: Bearer Token (通过 Authorization Header)

---

## 1. 中药材相关接口

### 1.1 获取药材列表
- **接口**: `GET /api/herbs`
- **描述**: 获取中药材列表，支持分页和筛选
- **请求参数**:
  ```typescript
  {
    page?: number        // 页码，默认1
    pageSize?: number    // 每页数量，默认12
    nature?: string      // 性味筛选（如：温、寒、热等）
    meridian?: string    // 归经筛选（如：脾、肺、肝等）
    keyword?: string     // 关键词搜索（名称、功效等）
  }
  ```
- **响应数据**:
  ```typescript
  {
    list: Herb[]         // 药材列表
    total: number        // 总数量
  }
  
  // Herb 对象结构
  {
    id: number
    name: string
    image?: string
    nature: string       // 性味
    meridian: string     // 归经
    efficacy: string     // 功效
    description?: string // 详细介绍
    usage?: string       // 用法用量
    contraindications?: string // 注意事项
  }
  ```

### 1.2 获取药材详情
- **接口**: `GET /api/herbs/:id`
- **描述**: 获取单个药材的详细信息
- **路径参数**: `id` (药材ID)
- **响应数据**: `Herb` 对象

### 1.3 收藏药材
- **接口**: `POST /api/herbs/:id/favorite`
- **描述**: 收藏指定的药材
- **路径参数**: `id` (药材ID)
- **响应数据**: 成功消息

### 1.4 取消收藏药材
- **接口**: `DELETE /api/herbs/:id/favorite`
- **描述**: 取消收藏指定的药材
- **路径参数**: `id` (药材ID)
- **响应数据**: 成功消息

---

## 2. 药膳配方相关接口

### 2.1 获取配方列表
- **接口**: `GET /api/recipes`
- **描述**: 获取药膳配方列表，支持分页和搜索
- **请求参数**:
  ```typescript
  {
    page?: number        // 页码
    pageSize?: number    // 每页数量
    keyword?: string     // 关键词搜索
  }
  ```
- **响应数据**:
  ```typescript
  {
    list: Recipe[]       // 配方列表
    total: number        // 总数量
  }
  
  // Recipe 对象结构
  {
    id: number
    name: string
    image?: string
    efficacy: string              // 功效
    mainIngredients: string[]     // 主要食材
    herbs: Array<{                // 所用药材
      id: number
      name: string
    }>
    steps?: string[]              // 制作步骤
    description?: string          // 简介
  }
  ```

### 2.2 获取配方详情
- **接口**: `GET /api/recipes/:id`
- **描述**: 获取单个配方的详细信息
- **路径参数**: `id` (配方ID)
- **响应数据**: `Recipe` 对象

### 2.3 收藏配方
- **接口**: `POST /api/recipes/:id/favorite`
- **描述**: 收藏指定的配方
- **路径参数**: `id` (配方ID)

### 2.4 取消收藏配方
- **接口**: `DELETE /api/recipes/:id/favorite`
- **描述**: 取消收藏指定的配方
- **路径参数**: `id` (配方ID)

---

## 3. 常见病症相关接口

### 3.1 获取病症列表
- **接口**: `GET /api/diseases`
- **描述**: 获取常见病症列表，支持分页和搜索
- **请求参数**:
  ```typescript
  {
    page?: number        // 页码
    pageSize?: number    // 每页数量
    keyword?: string     // 关键词搜索
  }
  ```
- **响应数据**:
  ```typescript
  {
    list: Disease[]      // 病症列表
    total: number        // 总数量
  }
  
  // Disease 对象结构
  {
    id: number
    name: string
    introduction: string  // 简介
    etiology?: string    // 病因病机
    prevention?: string  // 防治方法
    relatedHerbs?: Array<{  // 相关药材
      id: number
      name: string
    }>
    relatedRecipes?: Array<{ // 相关药膳
      id: number
      name: string
    }>
  }
  ```

### 3.2 获取病症详情
- **接口**: `GET /api/diseases/:id`
- **描述**: 获取单个病症的详细信息
- **路径参数**: `id` (病症ID)
- **响应数据**: `Disease` 对象

### 3.3 收藏病症
- **接口**: `POST /api/diseases/:id/favorite`
- **描述**: 收藏指定的病症
- **路径参数**: `id` (病症ID)

### 3.4 取消收藏病症
- **接口**: `DELETE /api/diseases/:id/favorite`
- **描述**: 取消收藏指定的病症
- **路径参数**: `id` (病症ID)

---

## 4. 评论相关接口

### 4.1 获取评论列表
- **接口**: `GET /api/comments`
- **描述**: 获取指定内容的评论列表
- **请求参数**:
  ```typescript
  {
    targetId: number     // 目标ID（药材/配方/病症ID）
    targetType: string   // 目标类型：'herb' | 'recipe' | 'disease'
  }
  ```
- **响应数据**:
  ```typescript
  Comment[]             // 评论列表
  
  // Comment 对象结构
  {
    id: number
    content: string
    userId: number
    username: string
    createdAt: string   // ISO 8601 格式时间
    replies?: Comment[] // 回复列表（可选）
  }
  ```

### 4.2 发表评论
- **接口**: `POST /api/comments`
- **描述**: 发表新评论或回复
- **请求体**:
  ```typescript
  {
    content: string      // 评论内容
    targetId: number     // 目标ID
    targetType: 'herb' | 'recipe' | 'disease'  // 目标类型
    parentId?: number    // 父评论ID（回复时使用）
  }
  ```
- **响应数据**: `Comment` 对象

### 4.3 删除评论
- **接口**: `DELETE /api/comments/:id`
- **描述**: 删除指定的评论
- **路径参数**: `id` (评论ID)

---

## 5. 学习笔记相关接口

### 5.1 获取笔记列表
- **接口**: `GET /api/learning/notes`
- **描述**: 获取当前用户的学习笔记列表
- **响应数据**: `LearningNote[]`
- **数据结构**:
  ```typescript
  {
    id: number
    title: string        // 笔记标题
    content: string      // 笔记内容
    tags?: string[]      // 标签数组
    createdAt: string   // 创建时间
    updatedAt: string   // 更新时间
  }
  ```

### 5.2 创建笔记
- **接口**: `POST /api/learning/notes`
- **描述**: 创建新的学习笔记
- **请求体**: `LearningNote` 对象（id 和 时间字段由后端生成）

### 5.3 更新笔记
- **接口**: `PUT /api/learning/notes/:id`
- **描述**: 更新指定的学习笔记
- **路径参数**: `id` (笔记ID)
- **请求体**: `Partial<LearningNote>` (部分字段)

### 5.4 删除笔记
- **接口**: `DELETE /api/learning/notes/:id`
- **描述**: 删除指定的学习笔记
- **路径参数**: `id` (笔记ID)

---

## 6. 锻炼记录相关接口

### 6.1 获取锻炼记录列表
- **接口**: `GET /api/exercise/records`
- **描述**: 获取当前用户的锻炼记录列表
- **请求参数**:
  ```typescript
  {
    startDate?: string   // 开始日期（ISO 8601）
    endDate?: string     // 结束日期（ISO 8601）
    type?: string        // 锻炼类型筛选
  }
  ```
- **响应数据**: `ExerciseRecord[]`
- **数据结构**:
  ```typescript
  {
    id: number
    type: string         // 锻炼类型（如：跑步、游泳等）
    duration: number     // 时长（分钟）
    intensity: 'low' | 'medium' | 'high'  // 强度
    notes?: string       // 备注
    date: string         // 日期（ISO 8601）
  }
  ```

### 6.2 创建锻炼记录
- **接口**: `POST /api/exercise/records`
- **描述**: 创建新的锻炼记录
- **请求体**: `ExerciseRecord` 对象（id 和 date 由前端生成或后端生成）

### 6.3 更新锻炼记录
- **接口**: `PUT /api/exercise/records/:id`
- **描述**: 更新指定的锻炼记录
- **路径参数**: `id` (记录ID)
- **请求体**: `Partial<ExerciseRecord>`

### 6.4 删除锻炼记录
- **接口**: `DELETE /api/exercise/records/:id`
- **描述**: 删除指定的锻炼记录
- **路径参数**: `id` (记录ID)

### 6.5 获取统计数据
- **接口**: `GET /api/exercise/statistics`
- **描述**: 获取锻炼统计数据
- **请求参数**: 同 6.1（可选）
- **响应数据**:
  ```typescript
  {
    totalDuration: number   // 总时长（分钟）
    totalCount: number      // 总次数
    averageDuration: number // 平均时长（分钟）
  }
  ```

---

## 7. 健康记录相关接口

### 7.1 获取健康记录列表
- **接口**: `GET /api/health/records`
- **描述**: 获取当前用户的健康记录列表
- **响应数据**: `HealthRecord[]`
- **数据结构**:
  ```typescript
  {
    id: number
    type: string         // 记录类型：'生病' | '不适' | '体检' | '用药' | '其他'
    symptoms: string     // 症状/情况描述
    notes?: string       // 备注
    date: string         // 日期（ISO 8601）
  }
  ```

### 7.2 创建健康记录
- **接口**: `POST /api/health/records`
- **描述**: 创建新的健康记录
- **请求体**: `HealthRecord` 对象

### 7.3 更新健康记录
- **接口**: `PUT /api/health/records/:id`
- **描述**: 更新指定的健康记录
- **路径参数**: `id` (记录ID)
- **请求体**: `Partial<HealthRecord>`

### 7.4 删除健康记录
- **接口**: `DELETE /api/health/records/:id`
- **描述**: 删除指定的健康记录
- **路径参数**: `id` (记录ID)

---

## 8. AI 相关接口

### 8.1 AI 聊天
- **接口**: `POST /api/ai/chat`
- **描述**: 与 AI 健康助手对话
- **请求体**:
  ```typescript
  {
    message: string           // 用户消息
    healthRecords: HealthRecord[]  // 用户的健康记录（用于上下文）
  }
  ```
- **响应数据**:
  ```typescript
  {
    reply: string            // AI 回复内容
  }
  ```

### 8.2 AI 健康分析
- **接口**: `POST /api/ai/analyze`
- **描述**: AI 分析用户的健康记录并给出建议
- **请求体**:
  ```typescript
  {
    healthRecords: HealthRecord[]  // 健康记录列表
  }
  ```
- **响应数据**:
  ```typescript
  {
    summary: string          // 健康总结
    suggestions: string[]    // 建议列表
    warnings: string[]       // 警告列表
  }
  ```

---

## 9. 用户相关接口（可选）

### 9.1 获取用户信息
- **接口**: `GET /api/user/info`
- **描述**: 获取当前登录用户信息
- **响应数据**:
  ```typescript
  {
    id: number
    username: string
    email?: string
    avatar?: string
  }
  ```

### 9.2 获取收藏列表
- **接口**: `GET /api/user/favorites`
- **描述**: 获取当前用户的收藏列表
- **请求参数**:
  ```typescript
  {
    type?: 'herb' | 'recipe' | 'disease'  // 收藏类型筛选
  }
  ```
- **响应数据**:
  ```typescript
  {
    herbs: Herb[]
    recipes: Recipe[]
    diseases: Disease[]
  }
  ```

---

## 错误响应格式

所有接口在出错时返回统一格式：

```typescript
{
  code: number          // 错误码（非200表示错误）
  message: string       // 错误消息
  data?: any           // 错误详情（可选）
}
```

### 常见错误码

- `200`: 成功
- `400`: 请求参数错误
- `401`: 未授权（需要登录）
- `403`: 无权限
- `404`: 资源不存在
- `500`: 服务器内部错误

---

## 注意事项

1. **认证**: 所有需要用户身份的接口都需要在请求头中携带 `Authorization: Bearer {token}`
2. **分页**: 列表接口默认使用分页，建议每页数量不超过 100
3. **时间格式**: 所有时间字段使用 ISO 8601 格式（如：`2024-01-01T00:00:00.000Z`）
4. **图片**: 图片字段返回 URL 路径，前端需要拼接完整的图片地址
5. **数据验证**: 前端应对数据进行基本验证，后端也会进行验证

---

## 接口调用示例

### JavaScript/TypeScript 示例

```typescript
import axios from 'axios'

// 获取药材列表
const getHerbs = async () => {
  const response = await axios.get('/api/herbs', {
    params: {
      page: 1,
      pageSize: 12,
      keyword: '人参'
    },
    headers: {
      'Authorization': 'Bearer your-token-here'
    }
  })
  return response.data
}

// 创建学习笔记
const createNote = async (note) => {
  const response = await axios.post('/api/learning/notes', note, {
    headers: {
      'Authorization': 'Bearer your-token-here',
      'Content-Type': 'application/json'
    }
  })
  return response.data
}
```

---

## 接口统计

- **药材相关**: 4 个接口
- **药膳相关**: 4 个接口
- **病症相关**: 4 个接口
- **评论相关**: 3 个接口
- **学习笔记**: 4 个接口
- **锻炼记录**: 5 个接口
- **健康记录**: 4 个接口
- **AI 相关**: 2 个接口
- **用户相关**: 2 个接口（可选）

**总计**: 32 个接口

