# bjvito

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

``` bash
根据网上的攻略(https://segmentfault.com/a/1190000011265006)，改造成了多页面的开发环境（其实原理就是webpack的多入口）。

改造完成之后，在开发环境运行：local host：8099/#/的时候，发现只出现了phone里的页面，pc里的页面显示不出来。

经过好一段时间的排查，突然醒悟，local host：8099/#/是默认省略了index.html的，它完整的路径应该是：local host：8099/index.html#/.

显然，要显示pc里的页面，正确的路径应该是：local host：8099/main.html#/.
```

``` bash
改造了一点东西，使构建时可以分项目构建。比如正常情况下的命令：

> npm run build

是打包了所有项目。而我们现在只想构建pc项目，用下面的命令来实现：

> npm run build pc

其中关键是build/utils.js里对webpack入口的改造：

> // 拿到命令行里参数，比如执行（npm run build projectA）,这个时候projectName就等于projectA
> // 有了这个变量，就可以根据这个名字来读取projectConfig里面的配置了
> let projectName = process.argv[2] || 'all';

process能获取到script命令的参数，process.argv[2]就是上述命令的pc，拿到项目名称，我们就能做一些操作了。
```