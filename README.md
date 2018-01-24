[Usage](## Usage)
[Hexo](# Hexo)
# Hexo-Theme-Huxblog

> Ported Theme of [Hux Blog](https://github.com/Huxpro/huxpro.github.io), Thank [Huxpro](https://github.com/Huxpro) for designing such a flawless theme.

## [Demo &rarr;](http://kaijun.github.io/hexo-theme-huxblog)

![](http://huangxuan.me/img/blog-desktop.jpg)

## Usage

I didn't publish it as a single theme folder because a few of the pages are added and modified manually, so you should manually create some extra folders in `source` for the new pages and modify the `_config.yml` if you only have the single theme folder.

So i just pushed the whole hexo project for your convenience, all pre settings and boilerplates are included, have a look and go ahead customizing your own blog!

### 1.Init

```
git clone https://github.com/Kaijun/hexo-theme-huxblog.git
cd hexo-theme-huxblog
npm install
```

### 2.Modify
Modify `_config.yml` file with your own info.
Especially the section:

```
deploy:
  type: git
  repo: yourRepo SSH or HTTPS
  branch: master
```
Replace with your own repo!

### 3.Writting/Serve/Deploy

```
hexo new post IMAPOST
hexo serve // run hexo in local environment
hexo clean && hexo deploy // hexo will push the static files automatically into the specific branch(gh-pages) of your repo!
```

### 4.Change Log

-  當上傳github-page出現404問題時，可以在source目录里加入.nojekyll文件，然后更改Hexo的_config.yml加入以下配置，这样在hexo -g的时候就会包含.nojekyll文件了
```
include:
  - .nojekyll
```

## Ref
[Document](https://github.com/Huxpro/huxpro.github.io)  
[GitPage部署Hexo NexT主题的CSS/JS错误](http://awhisper.github.io/2016/11/21/GitPage-Next%E7%9A%84CSS-JS%E9%94%99%E8%AF%AF/)  
[有关博客传到github css js 404的问题 解决方案](https://github.com/iissnan/hexo-theme-next/issues/1220)  

# Hexo 
在 Dev 的 branch 下進行以下操作

## 新增blog
```
$ hexo new <title>  #命名方式 year-month-day-title
```

## 插入圖片方式
```
![](image.jpg)  # 圖片放在以title命名的文件夾目錄下

```

## 預覽&發布
```
$ hexo s		# 啟動本地瀏覽，用於預覽 blog
$ hexo clean    # 清楚已產生的靜態文件
$ hexo g        # 產生靜態文件
$ hexo d -g     # 產生靜態文件，并部署上 Github

```



