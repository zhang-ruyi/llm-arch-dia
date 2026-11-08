# LLM 推理架构图解

用 [Archify](https://github.com/tt-a1i/archify) 生成的 LLM 推理架构交互图集,聚焦 vLLM 执行引擎与 LMCache KV 缓存层的核心框架。

## 图集

- vLLM V1 架构总览
- vLLM 请求生命周期与连续批处理
- PagedAttention 与前缀缓存
- LMCache 架构
- LMCache KV 命中、加载与写回
- vLLM + LMCache 联合请求链路
- 超长会话:KV 的创建、下沉与命中回载

## 目录

```
site/                 # 可直接部署的交互图 + index.html
.archify/             # 图源候选 JSON
```

## 源码基线

- vLLM:`c724bb35d4e70201cf0fa6f2f1dcd802c6f9dad4`
- LMCache:`a4a688827def88f1df3e9af5fad43245913fca36`

## 预览

```bash
python3 -m http.server 8000 -d site
# http://localhost:8000
```

## 重建单张图

```bash
export ARCHIFY_CHROME=$HOME/.cache/archify-chrome/chrome-headless-shell-linux64/chrome-headless-shell
export ARCHIFY_CHROME_NO_SANDBOX=1

# vLLM 图
node ~/.agents/skills/archify/bin/archify.mjs finalize architecture \
  .archify/architecture-vllm-architecture/candidate.json \
  site/vllm-architecture.html \
  --repo-root /home/zhang/workspace/Git/LLM/vllm --quality showcase --json

# LMCache 图
node ~/.agents/skills/archify/bin/archify.mjs finalize architecture \
  .archify/architecture-lmcache-architecture/candidate.json \
  site/lmcache-architecture.html \
  --repo-root /home/zhang/workspace/Git/LLM/LMCache --quality showcase --json

# 联合链路(无源码证据)
node ~/.agents/skills/archify/bin/archify.mjs finalize sequence \
  .archify/sequence-vllm-lmcache-integration/candidate.json \
  site/vllm-lmcache-integration.html --quality showcase --json
```

更新后重建 `site/index.html` 中的 iframe 不需要变化(文件路径固定)。

## 在博客中使用

本仓库作为 `zhang-ruyi/ruy` 的 submodule 挂在 `subprojects/llm-arch-dia`,构建时复制到站点 `/llm-arch-dia/`。

## 版权

内容版权与使用限制:未经作者书面许可,请勿用于商业用途或直接转载。
