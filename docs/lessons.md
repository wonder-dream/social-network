# Lessons

- 首次推送新创建的 GitHub 仓库时，Fine-grained PAT 虽有建仓权限但缺 `Contents: Read and write` 导致 `git push` 报 403；通过 `gh auth login` 浏览器 OAuth 设备码授权（8 位码直接显示在终端而非短信）重新配置 Git 凭据解决 [[26-11-26-15-立项与调研留痕]]
- 网上大量老旧医疗知识图谱教程仍使用 `py2neo`，但该库已归档停止维护且不兼容新版 Neo4j；调研阶段已决定一律采用官方 `neo4j` 驱动与参数化 `UNWIND MERGE` 避坑 [[26-11-26-15-立项与调研留痕]]
- 直接硬爬国内商业医疗网站易触发验证码与反爬封禁；改用开源 `medical.json` 子集叠加中文维基官方 MediaWiki API（附带合规 `User-Agent`）可稳定合规地完成双源采集 [[26-11-26-15-立项与调研留痕]]
