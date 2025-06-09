# σ₂: System Patterns

_v1.1 | Created: 2024-12-28 | Updated: 2024-12-28_
_Π: 🏗️DEVELOPMENT | Ω: 🔍RESEARCH_

## 🏛️ Architecture Overview

OntaPay 采用现代化的前端架构模式，基于组件化设计和模块化开发理念。

```
┌─────────────────────────────────────────────────────────┐
│                    Presentation Layer                   │
├─────────────────────────────────────────────────────────┤
│  React Components + TailwindCSS + DaisyUI              │
│  ├── routes/          (页面路由组件)                    │
│  ├── components/      (可复用UI组件)                    │
│  └── wallets/         (钱包相关组件: OKX, Phantom, Trust) │
├─────────────────────────────────────────────────────────┤
│                    Business Logic Layer                 │
├─────────────────────────────────────────────────────────┤
│  Hooks + Utils + API                                   │
│  ├── hooks/           (自定义React Hooks)              │
│  ├── utils/           (工具函数)                        │
│  ├── api/             (API调用逻辑)                     │
│  └── types/           (TypeScript类型定义)              │
├─────────────────────────────────────────────────────────┤
│                    Integration Layer                    │
├─────────────────────────────────────────────────────────┤
│  Wallet Adapters + Blockchain SDKs                     │
│  ├── @okxconnect/solana-provider                       │
│  ├── @solana/web3.js                                   │
│  ├── @solana/spl-token                                 │
│  ├── Trust Wallet SDK (计划集成)                       │
│  └── viem (以太坊兼容)                                  │
└─────────────────────────────────────────────────────────┘
```

## 🔧 Core Design Patterns

### 1. 🎯 Provider Pattern

- **WalletProvider**: 统一钱包状态管理
- **Context API**: 全局状态共享
- **适配器模式**: 不同钱包的统一接口

### 2. 🧩 Component Composition

- **通用组件**: 统一的钱包交互界面设计
- **原子化组件**: 基于 Radix UI 的可复用组件
- **复合组件**: 业务逻辑封装，兼容多钱包
- **HOC模式**: 钱包连接状态增强

### 3. 🔄 State Management

- **React Hooks**: 本地状态管理
- **Context + Reducer**: 复杂状态逻辑
- **Custom Hooks**: 业务逻辑抽象

### 4. 🛣️ Routing Architecture

- **文件系统路由**: TanStack Router 自动生成
- **类型安全**: 编译时路由验证
- **嵌套路由**: 支持复杂页面结构

## 🔐 Security Patterns

- **钱包签名验证**: 交易前强制用户确认
- **输入验证**: 所有用户输入的严格校验
- **错误边界**: 组件级错误处理
- **CSP策略**: 内容安全策略配置

## 📱 Mobile-First Design Patterns

- **移动端专用**: 专注手机网页体验设计
- **触摸优化**: 移动端交互和手势支持
- **钱包应用交互**: Deep Link 与移动钱包 App 集成
- **PWA就绪**: 渐进式Web应用支持

## 🔄 Data Flow Patterns

```
User Action → Component → Hook → API/Wallet → Blockchain
     ↓           ↓        ↓       ↓           ↓
   Event    State Update  Logic  Network    Transaction
     ↓           ↓        ↓       ↓           ↓
  UI Update ← Component ← Hook ← Response ← Confirmation
```

## 🧪 Testing Patterns

- **组件测试**: React Testing Library
- **集成测试**: 端到端用户流程
- **钱包模拟**: 测试环境钱包适配器
- **类型检查**: TypeScript 编译时验证
