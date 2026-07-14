# B2B 合作意向落地页

一个用于收集 B2B 合作意向的落地页：访客填写表单并提交后，数据会实时写入 Supabase 数据库，可随时查询。

## 项目说明

访客在网页上填写表单 → 点提交 → 数据真实存入数据库 → 可在页面或数据库后台查看。

就这一件事，做到「真的能用」。

## 表单字段

| 字段 | 数据库字段名 | 是否必填 |
|------|-------------|---------|
| 公司名称 | company_name | ✅ |
| 联系人 | contact_name | ✅ |
| 邮箱 | email | ✅ |
| 电话 | phone | ❌ |
| 合作类型 | cooperation_type | ❌ |
| 备注 | note | ❌ |

## 技术方案

- **前端**：纯 HTML + CSS + 原生 JavaScript，无框架
- **数据库**：Supabase（Postgres），表名 `b2b_leads`
- **数据连接**：Supabase JS SDK v2，前端直连数据库（RLS 已关闭，anon key 可直接读写）
- **部署**：Vercel 静态托管

整个项目只有一个 `index.html` 文件，Supabase SDK 通过 CDN 引入，不需要构建步骤、不需要后端服务器。

## 本地运行

直接用浏览器打开 `index.html` 就能使用，不需要任何环境配置。

## 部署到 Vercel

1. 注册 / 登录 [Vercel](https://vercel.com)（建议用 GitHub 账号）
2. 把 `index.html` 上传到一个 GitHub 仓库
3. 在 Vercel 控制台点 **Add New...** → **Project**
4. 选择刚创建的 GitHub 仓库，点 **Import**
5. Framework Preset 选 **Other**，其他默认
6. 点 **Deploy**，等 10-20 秒
7. 拿到 `xxx.vercel.app` 网址，任何人都能访问

## 如何验证数据真的进了数据库

### 方法一：页面查看
打开落地页，点右上角「查看提交记录」，会弹出表格显示所有提交过的数据（直接从数据库读取）。

### 方法二：Supabase 后台查看（最真实）
1. 登录 [Supabase](https://supabase.com)
2. 进入项目 → 左侧菜单 **Table Editor**
3. 选择 `b2b_leads` 表
4. 即可看到所有提交记录，每行对应一次表单提交

## 文件结构

```
.
├── index.html      # 落地页全部代码（HTML + CSS + JS）
└── README.md       # 项目说明
```

## 数据库信息

- **表名**：`b2b_leads`
- **字段**：id, company_name, contact_name, email, phone, cooperation_type, note, created_at
- **连接方式**：Supabase JS SDK（anon key 已内嵌在 index.html 中）

## 备注

本项目为面试作业，测试数据均为虚构信息。
