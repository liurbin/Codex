# 使用 Azure OpenAI Key 在 Codex 中启用 GPT-5（直接配置版）

本项目示例展示如何通过 **Azure AI Studio (ai.azure.com)** 提供的 API Key 配置 Codex，并在 `config.toml` 中启用 `gpt-5`。  
此方式 **不依赖环境变量**，Key 直接写入配置文件。  

> ⚠️ 注意：此方法仅适用于本地开发与测试。  
> 千万不要将包含真实 Key 的配置文件提交到 GitHub 公共仓库。  
> 建议在发布前用占位符（如 `your-key-here`）替换。

---
## 1. 安装Codex

全局安装 Codex
```bash
npm i -g @openai/codex
```

验证是否安装成功
```bash
codex --help
```
---

## 2. 获取 Azure OpenAI Key
1. 登录 [Azure AI Studio](https://ai.azure.com/)  
2. 打开你创建的 **Azure OpenAI 项目**  
3. 在左侧导航选择 **Resource details（资源详情）**  
4. 找到 **Endpoint** 和 **API Key**  

---

## 3. 配置 `config.toml`

在项目根目录下创建或修改 `config.toml`，并直接写入 Key：

```toml
[model_providers.azure]
name = "Azure"
base_url = "https://<your-resource-name>.openai.azure.com/"
//if not work, try like this: https://<your-resource-name>.openai.azure.com/openai/deployments/gpt-5
api_key = "your-azure-openai-key"     # 直接写入 Key
query_params = { api-version = "2025-04-01-preview" }
wire_api = "chat"

[profiles.azure_gpt]
model_provider = "azure"
model = "gpt-5"
preferred_auth_method = "apikey"

model_reasoning_effort = "high"
model_reasoning_summary = "detailed"
```

## 4. 使用azure_gpt profile启动Codex
```bash
codex --profile azure_gpt
```
## 5. Enjoy Codex with AzureOpenAI

