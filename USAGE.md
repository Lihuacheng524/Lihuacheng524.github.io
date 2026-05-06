# 个人博客操作手册

## 📖 目录
1. [快速开始](#一快速开始)
2. [修改栏目（导航菜单）](#二修改栏目导航菜单)
3. [写新博客](#三写新博客)
4. [修改个人信息](#四修改个人信息)
5. [修改目标页面](#五修改目标页面)
6. [修改关于页面](#六修改关于页面)
7. [推送更新上线](#七推送更新上线)

---

## 一、快速开始

### 本地预览博客
在 `d:\Files\blog` 文件夹下打开终端，运行：
```bash
npx hexo server
```
然后打开浏览器访问：http://localhost:4000

---

## 二、修改栏目（导航菜单）

1. 打开文件：`themes\trae-light\_config.yml`
2. 找到 `menu` 部分，修改如下：
   ```yaml
   menu:
     首页: /                    # 格式：显示文字: /链接地址/
     博客文章: /archives/
     我的目标: /goals/
     关于我: /about/
   ```
3. 保存文件

---

## 三、写新博客

### 方法1：用命令创建（推荐）
1. 在 `d:\Files\blog` 文件夹下打开终端
2. 运行：
   ```bash
   npx hexo new "我的文章标题"
   ```
3. 它会在 `source\_posts\` 文件夹里创建新文件
4. 打开那个 `.md` 文件，开始写！

### 方法2：手动创建
1. 在 `source\_posts\` 文件夹里新建一个 `.md` 文件
2. 开头必须写这些配置：
   ```markdown
   ---
   title: 文章标题
   date: 2026-05-06 12:00:00
   tags: [标签1, 标签2]
   categories: 分类
   ---
   
   在这里写文章内容...
   ```

---

## 四、修改个人信息

1. 打开文件：`themes\trae-light\_config.yml`
2. 修改这些部分：
   ```yaml
   avatar: /images/头像.jpg        # 头像放到 source/images/ 文件夹
   greeting: Hi, 我是              # 首页问候语
   subtitle: 热衷于技术探索         # 副标题
   
   social:
     GitHub: https://github.com/Lihuacheng524   # 链接
   ```

---

## 五、修改目标页面

1. 打开文件：`source\goals\index.md`
2. 直接在里面修改你的目标内容

---

## 六、修改关于页面

1. 打开文件：`source\about\index.md`
2. 直接在里面修改你的个人介绍

---

## 七、推送更新上线

### 步骤1：添加修改
```bash
git add .
```

### 步骤2：提交修改
```bash
git commit -m "修改内容描述"
```
（引号里写你改了什么，比如"添加新文章"或"更新个人介绍"）

### 步骤3：推送到GitHub
```bash
git push
```

### 步骤4：等待部署
推送后，**等待2-3分钟**，然后访问：https://lihuacheng524.github.io

---

## ✅ 检查清单
每次更新后确认：
- [ ] 文件保存了
- [ ] `git add .` 了
- [ ] `git commit` 了
- [ ] `git push` 了
- [ ] 等了2-3分钟
