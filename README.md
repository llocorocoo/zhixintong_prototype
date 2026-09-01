# 职信通 ZhiXinTong

> 个人职业信用管理平台 —— 由候选人自己发起核验，生成职业信用报告、信用评分与可信简历。

一套 Taro 代码同时运行于 **H5 与微信小程序**。本仓库是**跨端演示版**，用 mock 数据完整跑通全流程，无需后端即可访问。

<p>
  <img alt="Taro" src="https://img.shields.io/badge/Taro-4.1.9-0A79F7" />
  <img alt="React" src="https://img.shields.io/badge/React-18-61DAFB" />
  <img alt="NestJS" src="https://img.shields.io/badge/NestJS-10-E0234E" />
  <img alt="TypeScript" src="https://img.shields.io/badge/TypeScript-5.4-3178C6" />
  <img alt="Tailwind" src="https://img.shields.io/badge/Tailwind-v4-38BDF8" />
</p>

## 在线演示

https://project-6wmac.vercel.app **建议用手机打开，或在桌面浏览器按 `F12` 切换手机视图**

登录：**手机号与密码任意填写**即可进入演示环境。新账号数据为空，按以下顺序体验完整流程：

```
① 首页「立即生成」 → ② 支付（模拟） → ③ 隐私声明 → ④ 填写信息 → ⑤ 签署授权书
                                                                      ↓
              ⑦ 可信简历「一键同步」 ←  ⑥ 查看报告与评分  ←  核验进度
```

> 退出登录会清空该账号数据，可反复从头体验。

## 功能

| 模块 | 说明 |
|------|------|
| **信用评分** | 5 维度模型（真实性 20% / 稳定性 15% / 合规性 15% / 安全性 30% / 专业性 20%），基准分 600、满分 1000，评分卡与雷达图呈现 |
| **职业信用报告** | 填写身份、学历、职业资格并签署授权后发起核验，输出可下载分享的报告 |
| **可信简历** | 从报告一键同步生成，支持工作履历、教育背景、技能、证书等分模块编辑 |
| **提升信用** | 补充工作履历 / 学历 / 证书，重新核验后提升评分 |
| **信用修复** | 针对可修复的历史记录提供法规依据与申请指引 |
| **订单与支付** | 报告生成与更新的下单、支付、待支付召回、订单列表与详情 |

## 技术栈

**前端**　Taro 4.1.9 + React 18 + TypeScript + Vite ｜ Tailwind CSS v4 + weapp-tailwindcss（小程序类名兼容）｜ Zustand v5（persist 持久化登录态）｜ 自建 shadcn 风格组件库

**后端**　NestJS 10，全局前缀 `/api`，模块：`auth` / `credit` / `report` / `resume` / `enhancement` / `order` / `upload`。演示态数据存于内存 Map，服务重启即清空。

## 快速开始

```bash
pnpm install

pnpm dev          # H5 前端 + NestJS 后端  → http://localhost:10086
pnpm dev:weapp    # 微信小程序 watch 构建

pnpm build        # 并行构建：lint + tsc + H5 + 微信小程序 + 后端
pnpm validate     # ESLint + TypeScript 检查
```

H5 开发时 `/api` 由 devServer 代理到 `localhost:3000`。部署到 Vercel 时会自动用 `src/network.mock.ts` 替换网络层，构建为无后端的静态演示站。

## 项目结构

```
├── src/                  # Taro 前端
│   ├── app.config.ts     # 路由与 tabBar（新增页面须在此注册）
│   ├── pages/            # 25 个页面
│   ├── components/ui/    # UI 组件库
│   ├── stores/user.ts    # Zustand 全局状态
│   ├── network.ts        # 网络请求封装
│   └── network.mock.ts   # 演示用 mock 网络层
├── server/src/modules/   # NestJS 后端模块
├── h5-prototype/         # 早期静态原型（按页面状态拆分）
├── config/               # Taro 构建配置
└── design_guidelines.md  # 设计规范
```

## 说明

本仓库为**演示 / 原型项目**：后端使用内存存储，核验结果为模拟数据，登录与支付均未接入真实服务，请勿用于处理真实个人信息。
