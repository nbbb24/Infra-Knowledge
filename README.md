<h1 align="center">Infra Knowledge</h1>

<p align="center">AI 基础设施学习笔记</p>

<p align="center">
| <a href="docs/zh/index.md">中文文档</a> |
</p>

第一阶段整理 NPU 硬件、内存、数据搬运、互联通信和性能分析知识。

## 本地预览

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements/mkdocs.txt
mkdocs serve
```

Windows PowerShell 使用 `.venv\Scripts\Activate.ps1` 激活虚拟环境。服务启动后打开
`http://127.0.0.1:8000`。

## 构建

```bash
mkdocs build --strict
```

生成的网站位于 `site/`，该目录已加入 Git 忽略列表。

## 部署到 Read the Docs

1. 使用能够访问本仓库的 GitHub 账号登录 Read the Docs。
2. 选择 **Add project**，导入 `nbbb24/Infra-Knowledge`。
3. 保持默认分支为 `main`，Read the Docs 会自动读取 `.readthedocs.yaml`。
4. 触发第一次构建并打开生成的网站地址。
5. 首次构建成功后，可以在 **Admin → Domains** 中绑定自定义域名。

不需要提交生成的 HTML。后续推送到 `main` 分支即可触发文档构建。

## 编写约定

- 中文页面统一放在 `docs/zh/` 下。
- 新增页面后，需要同步更新 `mkdocs.yml` 中的 `nav`。
- 缩写首次出现时给出全称，例如 `H2D (Host to Device)`。
- 非通用结论需要注明硬件型号或架构代际。
- 优先用拓扑、数据路径和可观测现象解释概念。
