# 参考教程

**[ 1 ]** [这可能是迄今为止最全的hexo博客搭建教程](https://cloud.tencent.com/developer/article/1520557)

**[ 2 ]** [Hexo攻略-设置分页与显示文章数](https://blog.csdn.net/qq_39181839/article/details/109477431)

**[ 3 ]** [如何使用 GitHub Actions 自动部署 Hexo 博客](https://juejin.cn/post/6943895271751286821)

**[ 4 ]** [Hexo博客配置RSS插件](https://www.jianshu.com/p/2aaac7a19736)

**[ 5 ]** [设置 tags 与 categories 页面](https://github.com/chasehu123/blogFiles#%E7%94%9F%E6%88%90-tags--categories-%E9%A1%B5%E9%9D%A2)

# 零碎步骤

- [ ] npm install hexo-deployer-git --save
- [ ] hexo new "hello-world-post"
- [ ] hexo new page "hello-world-page"
- [ ] hexo clean
- [ ] git clone https://github.com/next-theme/hexo-theme-next themes/next

# 配置 GitHub Actions

1. 创建一个有 **repo** 和 **workflow** 权限的 [GitHub Token](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fsettings%2Ftokens%2Fnew) 

2. blog source 仓库 -> `settings` -> `Secrets` -> `New repository secret` -> 命名 HEXO_DEPLOY。

3. GitHub Action:

   ```
   name: deploying Hexo project to GitHub pages
   on:
     push:
       branches:
         - master # master 分支有 push 行为时就触发这个 action
   
   jobs:
     build-and-deploy:
       runs-on: ubuntu-latest
       steps:
         - name: Checkout
           uses: actions/checkout@master
   
         - name: Build and Deploy
           uses: theme-keep/hexo-deploy-github-pages-action@master # 使用专门部署 Hexo 到 GitHub pages 的 action
           env:
             PERSONAL_TOKEN: ${{ secrets.HEXO_DEPLOY }} # secret 名
             PUBLISH_REPOSITORY: chasehu123/chasehu123.github.io # 公共仓库，格式：GitHub 用户名/仓库名
             BRANCH: gh-pages # 分支，填 gh-pages 就行
             PUBLISH_DIR: ./public # 部署 public 目录下的文件
   ```

