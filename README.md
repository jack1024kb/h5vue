# spack 编译

## 环境准备 
```shell
git clone dhw@139.129.27.90:/home/dhw/git-base/spack.git
cd spack
npm install
sudo npm link
```
这样在全局就有了spack　命令

## 拉项目代码
```shell
#开始做的时候我会建一个项目,先用xxx代替
git clone dhw@139.129.27.90:/home/dhw/git-base/template/xxx game
cd game
npm install
#开发的时候，执行命令，页面不会自动刷新，看效果，需要手动刷新页面,会自动起一个server，端口3000
spack dev
# 执行spack dev 后可以访问 your host:3000
#发布的时候，执行命令。不会启动server
spack pro
#发布后如果也想启动server
spack pro -s
#默认是发布到线上 web 环境，如果要发布到 app 环境，用 
spack pro -f '.spack-app'

#默认执行这两个命令是有缓存的。如果要全新编译 -c是 clean 的意思，一般不需要全新编译，除非发现页面有问题，可以尝试全新编译排除下
spack dev -c
spack pro -c
```
## 用spack编译的项目有一些规定
1. 所有代码在一个目录中，src为源代码目录。dev执行 spack dev 自动生成的目录，dist是执行spack pro自动生成的目录，node是spack 读node 模块用到的目录。
2. .spack是系统目录。配置文件放在这里。
3. html文件为编译入口文件，每个html文件对应一个同名的js文件，比如 如果有game.html，一定在同目录下有一个game.js文件，如果没有，就认为是纯html文件。
4. 代码统一用 es6模块语法，import ,export 。import 的文件如果省略后缀会自动补全为 *.js，如果以 '/'结尾 会自动补全为 "*/index.js"。不会去尝试其它文件后缀或做其它补全。可以引用css import '/css/a.css'，不可以用import引用图片，字体等资源。
5.如果用到node模块，需要在配置文件加 alias。
6. 可以用动态import 语法。
7. 不可以用 async ,for(var a of as)这两个语法。因为用的是buble来转码
8. 所有图片,字体，音视频等资源都放到 image目录，image可以有子目录，也可以有多个image目录

9. 从开发目录发布页面到产品路径。会去掉 /pages,文件夹和文件同名，会合并。布规则就是一个函数，是可以自定义的。

   - /pages/index/index.html        => /index.html
   - /pages/withdarw/widthdraw.html =>/withdraw.html
   - /pages/video/tv.html           =>/video/tv.html
   - /pages/video/movie.html        =>/video/movie.html
   
 跳目录有一个副作用，在html中直接引用资源，会找不到文件。比如用<img src='xxx'/> ，需要用 reslovePath 转换<img src=resolvePath('xxx') />
