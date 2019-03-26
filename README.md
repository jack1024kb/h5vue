# h5vue

## 环境准备 
```shell
git clone dhw@139.129.27.90:/home/dhw/git-base/spack.git
cd spack
qnpm install
sudo npm link
```
这样在全局就有了spack　命令

## 拉项目代码
```shell
git clone dhw@139.129.27.90:/home/dhw/git-base/template/h5vue
cd h5vue
qnpm install
#开发的时候，执行命令，页面不会自动刷新，看效果，需要手动刷新页面（自动刷新原来有，后来因为习惯手动刷新，就把自动刷新给去掉了）,会自动起一个server，端口3000
spack dev
# 执行spack dev 后可以访问 youhost:3000
#发布的时候，执行命令。不会启动server
spack pro
#发布后如果也想启动server
spack pro -s

#默认执行这两个命令是有缓存的。如果要全新编译 -c是 clean 的意思，一般不需要全新编译，除非发现页面有问题，可以尝试全新编译排除下
spack dev -c
spack pro -c
```
## 用spack编译的项目有一些规定
1. 所有代码在一个目录中，src为源代码目录。dev执行 spack dev 自动生成的目录，dist是执行spack pro自动生成的目录，node是spack 读node 模块用到的目录。
2. .spack是系统目录。配置文件放在这里（这个不用管，如果有需要我来修改）
3. 都用绝对路径。这个不是spack要求，而是客户端拉到代码后需要替换为本地路径，为了方便替换，我们都用"/" 开头的绝对路径。如果是页面路径都写全 比如 '/index.html' 不要省略index.html,而且都以.html结尾，这也是为了方便客户端替换
4. 代码统一用 es6模块语法，import ,export 。import 的文件如果省略后缀会自动补全为 *.js，如果以 '/'结尾 会自动补全为 "*/index.js"。不会去尝试其它文件后缀或做其它补全。可以引用css import '/css/a.css'
5.如果用到node模块，我来加。
6. 可以用动态import 语法。
7. 不可以用 async ,for(var a of as)这两个语法。因为用的是buble来转码
8. 所有图片,字体，音视频等资源都放到 image目录。image里可以有子目录。
9. 支持rem .这次出图会按 750px宽来出，在750宽下 1rem=100px,所以，如果标注是 16px ,就直接可以写 0.16rem
10. 从开发目录发布页面到产品路径。会去掉 /pages,文件夹和文件同名，会合并。
   /pages/index/index.html        => /index.html
   /pages/withdarw/widthdraw.html =>/withdraw.html
   /pages/video/tv.html           =>/video/tv.html
   /pages/video/movie.html        =>/video/movie.html
 
