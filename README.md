# 中传春游活动报名页

## 文件说明

- `index.html` — 学生报名页
- `admin.html` — 管理员查看页（密码：`cuc2025`，可在文件中修改）

---

## Supabase 配置步骤

### 1. 创建 Supabase 项目

前往 [https://supabase.com](https://supabase.com) 注册并新建项目。

### 2. 执行建表 SQL

在 Supabase 控制台 → SQL Editor 中执行：

```sql
-- 创建报名表
CREATE TABLE registrations (
  id          uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  name        text NOT NULL,
  student_id  text NOT NULL UNIQUE,
  phone       text NOT NULL,
  class_dept  text NOT NULL,
  note        text,
  created_at  timestamptz DEFAULT now()
);

-- 开启 Row Level Security
ALTER TABLE registrations ENABLE ROW LEVEL SECURITY;

-- 允许所有人插入（报名）
CREATE POLICY "allow_insert" ON registrations
  FOR INSERT TO anon WITH CHECK (true);

-- 允许所有人查询（管理页用前端密码控制）
CREATE POLICY "allow_select" ON registrations
  FOR SELECT TO anon USING (true);
```

### 3. 获取配置信息

Supabase 控制台 → Project Settings → API：
- `Project URL` → 填入 `SUPABASE_URL`
- `anon public` key → 填入 `SUPABASE_ANON_KEY`

### 4. 填入配置

在 `index.html` 和 `admin.html` 顶部配置区替换：

```js
const SUPABASE_URL = 'https://YOUR_PROJECT_ID.supabase.co'
const SUPABASE_ANON_KEY = 'YOUR_ANON_KEY'
```

---

## 访问地址

- 报名页：[https://destiny-ax.github.io/spring-trip/](https://destiny-ax.github.io/spring-trip/)
- 管理页：[https://destiny-ax.github.io/spring-trip/admin.html](https://destiny-ax.github.io/spring-trip/admin.html)

## 使用方式

配置完成后，直接访问上方地址即可，无需本地服务器。
