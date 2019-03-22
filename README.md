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
#发布的时候，执行命令。不会启动server
spack pro

#默认执行这两个命令是有缓存的。如果要全新编译 -c是 clean 的意思，一般不需要全新编译，除非发现页面有问题，可以尝试全新编译排除下
spack dev -c
spack pro -c
```
## 用spack项目编译的项目有一些规定
1. 所有代码在一个目录中，src为源代码目录。dev执行 spack dev 自动生成的目录，dist是执行spack pro自动生成的目录，node是spack 读node 模块用到的目录。
2. .spack是系统目录。配置文件放在这里（这个不用管，如果有需要我来修改）
3. 都用绝对路径。这个不是spack要求，而是客户端拉到代码后需要替换为本地路径，为了方便替换，我们都用"/" 开头的绝对路径。
4. 代码统一用 es6模块语法，import ,export 。import 的文件如果省略后缀会自动补全为 *.js，如果以 '/'结尾 会自动补全为 "*/index.js"。不会去尝试其它文件后缀或做其它补全。
5.如果用到node模块，我来加。
6. 可以用动态import 语法。
7. 不可以用 async ,for(var a of as)这两个语法。因为用的是buble来转码
8. 所有图片都放到 image目录。image里可以有子目录。所有字体都放到　font 目录，可以有子目录。
9. node模块如果用到前端代码中，node模块导出的只有default，只能这样引用 import spritevue from 'sprite-vue',不能这样引用 import {Vue} from 'sprite-vue'
