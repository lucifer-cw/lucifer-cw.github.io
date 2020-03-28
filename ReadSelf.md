#   常用方案
> ##  项目结构

*   Actions 		//redux actions
*   components	//封装组件
*   config		//配置和常量
*   Containers	//页面容器
*   I18n			//国际化配置
*   Images		//静态资源
*   Reducers		//redux reducers
*   Store		//redux store 配合数据库，本地化数据
*   utils			//常用工具

>## 常用组件方案
*   导航控制            `react-navigation`
*   热更新              `code-push || react-native-update`
*   国际化		        `react-native-i18n`
*   状态管理		        `react-redux redux(createStore)`
*   数据库		        `react-native-sqlite-storage`
*   本地Storage	        `react-native-storage`
*   状态持久化	        `redux-persist  && redux-persst-sqlite-storage(注意rn>0.6 对路径的影响)`
*   时间格式化	        `moment`
*   启动页		        `react-native-splash-screen`
*   UI组件库		        `teaset || AntDesign`
*   图标			        `react-native-vector-icons`
*   thunk中间件	        `redux-thunk`
*   图片选择		        `react-native-gesture-handler`
*   图片压缩            `react-native-image-resizer`
*   文件上传		        `rn-fetch-blob`
*   键盘防遮挡           `react-native-keyboard-aware-scroll-view`
*   buffer数据            `buffer`    

>## 小窍门
*   常用组件封装TView 可点击View onPress 添加全局的定时器，防止过快点击
*   常用按钮封装TBtn 根据enable && onPress 状态，内部判断按钮是否可点击
*   icon size   `android: 48,72,144,192   ios:58,80,87,120,180`

#   采坑日记 & 填坑小结
>+  node_modules 中不同的包依赖冲突 重复导出  
    把冲突的包放进 主项目的package.json  `"resolutions": {"@name": ^xxx}`  

>+  react-native-image-picker 安卓6.0 以后权限问题  
>在mainActivity 中提前做请求相机权限。否则在使用时要检测权限   

>+  react-native-swiper Text strings must be rendered within a <Text>
 >If you pass children with prop title inside Swiper you will get this error Text strings must be rendered within a <Text> component.

>+ Code-push ios注意 CFBundleShortVersionString 的值    

>+ 网上下载代码运行报错undefined is not an object (evaluating '_react.PropTypes.func')    
    PropTypes 从react 分离出去了。导入如下 `import PropTypes from 'prop-types';`

>+ FATAL EXCEPTION: create_react_context 安卓as run 变成了联系模式，无法连接本地npm 服务  
android 中 `import com.facebook.react.BuildConfig; 替换成自己包名的 import com.xxx.xxxx.BuildConfig`


#   常见问题
### android相关
+   连不上本地npm 服务  
`adb reverse tcp:8081 tcp:8081`


###npm 相关问题  
>+  npm login 409    
npm源不正确，切换官方源 `npm config set registry https://registry.npmjs.org`

>+   Unexpected end of JSON input while parsing near    
清除 .npmrc文件中已经存在的源配置`npm cache clean --force`   

###react-native-create-library 创建原生模块   
+   `react-native-create-library xx` xx模块名(会自动增加rn 前缀)
+ .podspec 文件位置问题
创建出来的.podspec 需要从ios 目录移除与index.js 平级

+   测试：cocoapods 检索主项目的package.json ，在package.json 先添加自己开发的包，注意版本
`cd iOS && pod install`

+ .podspec 中维护cocoapods 项目版本号，与package.json中的版本号无关
+ .podspec 其中s.home git 地址必填，否则pod install 报错
+ 若添加本地 .framework  .a .bundle
  .podspec 文件中添加对应的
  ```
    s.vendored_frameworks = 'WoqiSDK/Classes/*.framework'     
    s.vendored_libraries = 'WoqiSDK/Classes/*.a'    
    s.resource = 'WoqiSDK/Classes/*.bundle'
    //路径依据个人实际设定： 一般 ios/**/*.framework
+   sdk 如需其他系统库依赖，统一在主项目 link binary with libraries 中添加
+   >Rn ios原生模块 .bundle 文件 在build phases -》copy files 添加 //待验证，记不清了

#   各种骚操作

###git 相关问题 
+   合并某次commit 到其他分支    
    `git cherry-pick xxxx //xxx 为commit 版本号`    
+   从分支A 中抽取a,b 文件到分支B  
    ```
    git checkout B			// 首先切换到 B 分支   
    git checktou A a b		// 然后从 A 中抽取 a、b 两个选定的文件    
