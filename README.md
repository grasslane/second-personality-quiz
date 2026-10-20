# 你的第二人格是什么？（趣味心理测试）

十二道题，照见你白天与深夜不同的那一面。输入测试码即可开始，答完全部题目生成人格画像报告。

## 技术架构
- **前端**：GitHub Pages 静态托管（本仓库 `main` 分支根目录）
- **后端/数据库**：Supabase（Postgres + RLS + 数据库函数）
  - `validate_code`：校验测试码（不扣次数）
  - `consume_code`：答完扣次数（服务端原子扣减，每码限 2 次）+ 写入测试记录
  - 管理后台函数：`admin_list_codes` / `admin_generate_codes` / `admin_toggle_code` / `admin_list_attempts`

## 访问入口
- 用户测评页：`https://grasslane.github.io/second-personality-quiz/`
- 管理后台（密钥管理）：`https://grasslane.github.io/second-personality-quiz/admin.html`

## 管理后台使用
1. 打开 `admin.html`，用管理员邮箱 + 密码登录（见交付说明）。
2. 「生成新码」：输入数量一键生成（明文只显示一次，请立即复制分发）。
3. 码列表：查看每个码的用量，可停用/启用。
4. 测试记录：查看每次测试的时间、结果类型、所用测试码。

## 买家修改指南
- 品牌名 / 标题 / 题目 / 结果 / 配色：改 `index.html` 里 JS 的 `CONFIG`（文件头部有详细注释）。
- 每个码限测次数：改数据库 `codes` 表的 `max_uses` 字段（默认 2）。
- 测试码：全部在管理后台一键生成，无需改代码。

## 数据安全
- 测试码在数据库只存 SHA-256 哈希，不存明文。
- 匿名用户只能调用校验/扣次函数，无法读取码表；管理函数仅管理员可调用。
- 分享结果链接只包含答题序号，不含任何个人信息。
