### 1.运行项目
1. react-native init AwesomeProject初始化目录
2. react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res/
   运行命令将react-native打包到android目录
3. react-native run-android 安卓执行命令
4. 重复2.3操作

或者运行npm start，此时安卓端摇晃手机打开菜单设置配置pc的ip和端口后，reloadjs 可直接更新js。修改了安卓配置则需要重启项目


### 2.unable to load script from assets 'index.android bundle' ,make sure your bundle is packaged correct

1. 在 android/app/src/main 目录下创建一个 assets空文件夹
2. 项目根目录运行：
```javascript
react-native bundle --platform android --dev false --entry-file index.js --bundle-output android/app/src/main/assets/index.android.bundle --assets-dest android/app/src/main/res/
```
注意，是编译index.js而不是index.android.js
react-native新版本已经没有index.android.js和index.ios.js两个文件了，只有一个index.js文件,所以要编译index.js 

会发现 assets文件夹下多出两个文件
index.android.bundle index.android.bundle.meta

3. 重新react-native run-android
