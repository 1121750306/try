### 打包的输出路径配置项

assetsRoot: 打包后的文件放在那个目录下

assetsSubDirectory: 静态资源（例如vue-cli中的static目录的资源）将被打包在assetsRoot的哪个文件夹下

assetsPublicPath: 项目中引用到的资源的路径，会按照什么规则替换，例如 值为'public/'，则会在资源的路径前面增加该字段，制定是public下的资源

以下配置：
```
  assetsRoot: path.resolve(__dirname, '..', '..', 'be/WebRoot/public')

  assetsSubDirectory: 'staticResource'

  assetsPublicPath: 'public'
```
项目中的资源会被打包在be/WebRoot/public路径下

前端项目的static会被打包在staticResource下

其他默认打包在static下（默认未被修改）

而项目中引用的资源，如index.html中引用的资源，则会是public/static/----
