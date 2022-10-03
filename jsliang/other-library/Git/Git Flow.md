Git Flow
===

> Create by **jsliang** on **2020-09-27 23:46:57**  
> Recently revised in **2020-09-27 23:56:54**

<!-- 目录开始 -->
## 一 目录

**不折腾的前端，和咸鱼有什么区别**

| 目录 |
| --- |
| [一 目录](#chapter-one) |
| [二 前言](#chapter-two) |
<!-- 目录结束 -->

## 二 前言



* [Git Flow工作流总结](https://www.jianshu.com/p/34b95c5eedb6)

我们公司，有 4 个环境：
dev - 开发环境
test - 测试环境
sit - 验收环境
master - 线上环境

1. 每次拉新需求（feature）或者解决线上问题（hotfix），都从 master 拉。
2. feature-xxx/hotfix-xxx 分支，编写完之后，合并到 dev 分支，如果合并的时候，Gitlab 发现有冲突，那么执行 2.2
2.2 解决冲突：本地切换到 dev，git pull 拉取最新的，然后从 dev 切换一个新分支 conflict-xxx，在 git merge feature-xxx，将 feature 和 dev 的分支在 conflict 中解决
3. 开发环境经个人和后端检查，以及个人代码 Code Review 之后，确认没问题了，提交到 test。
4. 如果测试发现有问题，那么在个人分支解决，解决完之后再提交 test，如果有冲突，参照步骤 2.2
5. 上验收环境，给产品验收
6. 上线上环境，给用户使用

---

