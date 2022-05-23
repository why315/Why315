# 1、git

#### git忽略文件  .gitignore 失效解决方法

```bash
    第一步：cd 到项目目录
    第二步：git rm -r --cached .
    第三步：git add .
    第四步：git commit -m 'update .gitignore'
```

### 2、vscode生成项目目录解构

1. vscode安装插件，project-tree
2. 安装之后按ctrl+shift+p，并输入Project Tree回车
3. 点击要生成目录的项目，回车
4. 将项目目录生成并存储到README.md中

### 3、warning: LF will be replaced by CRLF in  xxxxxx

输入命令 ：`git config core.autocrlf false` (仅对当前git仓库有效）

### 4、PostCSS plugin postcss-pxtorem requires PostCSS 8 ？ 

npm i postcss-pxtorem@5.1.1 -D

5、github 远程仓库需要输入密码或者是个人令牌问题

```js
git remote add origin 'xxxxxxxxxx' (xxx是远程仓库得地址，最好使用ssh，不然每次一次都需要重复输入密码)
git push -u origin main 推送到远程仓库
```

6、创建个人令牌，设置有效期

```js
个人设置
settings
developsettings
personal access tokens 
复制令牌，在输入密码的时候输入令牌，可以设置令牌有效期
```

7、移除远程仓库得地址

```js
git remote remove origin
```

