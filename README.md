# Cook-MCP

Node.js 版本的 MCP（Model Context Protocol）示例，提供简单的菜谱工具 `list_recipes` 与 `get_recipe`，便于快速在阿里云百炼 MCP 应用里测试。

## 快速启动（本地）

```bash
npm install
npm start  # 默认端口 3000，可通过 PORT 覆盖
```

启动后 MCP 端点暴露在 `http://localhost:3000/`。

## 目录结构

- `src/server.js`：MCP 入口，注册工具与启动服务。
- `src/recipes.js`：示例菜谱数据。
- `package.json`：依赖与脚本。

## 阿里云百炼 MCP 应用部署步骤

> 前提：拥有百炼控制台访问权限，已开通 MCP 应用功能，具备一个可用的 Git 仓库（或直接上传压缩包）。

1) 准备仓库  
   - 将本工程推送到自己的 Git 仓库，或将项目压缩为 zip。

2) 配置运行命令  
   - 启动命令：`npm install --production && npm start`  
   - 需要保证 `PORT` 环境变量由平台注入；若平台要求固定端口，设置环境变量 `PORT=<平台指定端口>`。

3) 在百炼控制台新建 MCP 应用  
   - 选择「自定义/Node.js」运行时（尽量使用 Node 18+）。  
   - 代码来源选「Git」或「本地上传」对应你上一步的仓库/压缩包。  
   - 设置健康检查端口为 `PORT`（默认 3000，如平台要求其它端口请同步修改）。  
   - 部署后等待实例变为「运行中」。

4) 验证  
   - 在 MCP 工具列表中应看到 `list_recipes`、`get_recipe`。  
   - 尝试调用：  
     - `list_recipes` 输入空对象 `{}` 会返回全部示例菜谱。  
     - `list_recipes` 输入 `{ "tag": "家常" }` 按标签过滤。  
     - `get_recipe` 输入 `{ "id": "tomato-egg" }` 获取详情。

## 常见问题

- **端口不通**：确认平台分配的端口与 `PORT` 一致，并放开安全组/访问白名单。  
- **依赖安装失败**：确保使用 Node 18+，网络可访问 npm 镜像；必要时配置 `NPM_CONFIG_REGISTRY`。  
- **工具未注册**：重启应用并检查日志，确保 `@modelcontextprotocol/sdk` 能被正确加载。  

## 开发脚本

- `npm start`：本地启动  
- `npm run dev`：Node --watch 热重载（开发用）  
- `npm run lint`：基础 ESLint（可按需调整）

