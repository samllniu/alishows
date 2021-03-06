### 阿里百秀笔记
---

#### 零、注意事项

1. 403 和 400 -- 一般是参数错了，这时候看 参数、单词
2. 404 -- 说明是接口地址或者参数错了，优先检查 接口地址，然后是参数
3. 304 -- 忽略，说明是从本地缓存中读取文件
4. 5xx -- 服务器错了……

注意： 后台需要接收作者 `id` 信息，如果用的自己服务器，可能 `sessionId` 过期了，所以需要先退出，再次登录获取最新的 `sessionId` 之后，才能发布文章，如果用的远程服务器，不需要进行退出，因为在我的服务器端，已经写死了一个  `sessionId`

其他：
1. 代码在上线阶段，把项目中的 console.log 以及 alert 全部去掉


#### 疑难 bug 处理

1. 把对应的格式化插件干掉，否则会给参数加上空格，或者其他换行等其他东西，这个非常难查，基本查不出来
2. 参数别写错：type, url 与 ur1 , data
3. ★★★★★ 父级找不到，父级类名可以自己取，
4. 模板引擎错误，又开始就要有闭合
5. 文章上传，如果本地接口，那么需要先退出，登录之后才发布，
   用我的，就不必重新登录啦
 
#### 一、开发模式

1. 混合开发模式

- 就是指前后端没有分离的项目
- 前端只需要写 HTML 和 css 就可以，写好之后给后台
- 后台接收到前端页面之后，开始使用后端模板引擎嵌套页面
- 缺点：代码混合到一块，不易于后期的维护


2. 前后端分离开发模式

- 前端需要写 HTML 和 css 以及 ajax 和 js
- 后台操作数据库，给前端返回 json 格式的数据
- 前端使用 ajax 请求后台提供的接口，后台接口返回 json 格式的数据
  前端开始使用前端模板引擎嵌套页面
- 优点：前后端实现了分离，职责明确，方便后期的维护


#### 二、阿里百秀项目架构

1. 数据库：MongoDB
2. 逻辑层：Node.js、Express 以及 中间件
3. 前  端：jQuery、BootStrap、art-template


#### 三、登录思路

1. 给登录按钮绑定点击事件
2. 获取邮箱和密码
3. 判断邮箱和密码是否为空，如果是空，需要给提示，同时阻止代码往下运行
4. 发送 ajax 请求
5. 后台肯定会返回请求结果，成功的，进入网站的后台，如果失败，就给用户进行提示

#### 四、退出功能

1. 给退出绑定点击事件
2. 询问用户是否确定退出
3. 发送 ajax 请求


#### 五、用户添加

1. 给添加按钮绑定点击事件
2. 给 input 添加 name 属性，**注意：** 属性值需要和接口给的参数一致
3. $(this).serialize() 获取 form 表单中所有的 name 值
4. 发送 ajax 请求
5. 根据返回结果进行下一步的处理 


#### 六、头像上传

1. 给input 绑定 change 事件
2. 创建 new FormData()对象，然后使用 this.files[0] 使用下标获取具体的图片信息，
3. 开发发送 ajax 就可以
4. 在请求成功后的回调函数中，获取到头像的地址，同时赋值给页面上的 image
5. 创建隐藏域，把回调函数中返回的地址赋值给隐藏域


#### 七、用户列表展示

1. 打开页面，发送 ajax 请求，后台返回 json 格式的数据
2. 引用模板文件，定义模板，
3. 调用 template()方法，让数据和模板进行拼接
4. 获取父级，把生成的节点插入到 父级里面去


#### 八、 用户编辑功能

1. 使用事件委托的形式给编辑按钮绑定事件，同时获取唯一的值 id
2. 根据 id 需要发送 ajax 请求，获取所要更改的用户信息
3. 定义模板(**复制源码的模板引擎就可以，不用自己写**)，将数据信息展示到左侧，
4. 开始更新数据，发送 ajax, 然后点击保存按钮，重新刷新页面
  
第 4 步：具体细节：
1. 给修改用户的父级添加一个 id: modifyBox
2. 使用事件委托给模板中的 form 表单添加 submit 默认提交事件，同时给 form 表单自定义一个 id: data-id
3. 使用 serialize() 获取用户信息, 以及 $(this).attr('data-id') 或者id
4. 发送 ajax 请求
5. 将头像上传按钮的方法改成事件委托，代码直接复制就可以


#### 九、 用户删除功能

1. 使用事件委托的形式给删除按钮绑定事件，同时获取唯一的值 id
2. 发送 ajax ，将获取的 id 传入 接口地址



#### 十、 用户批量功能
[1, 2, 3]

1. 点击全选按钮，让每个 input 都勾选上，同时让批量删除显示
2. 点击每个 input 框，如果全部选中，那么让全选按钮也选中，同时让批量删除显示
3. 根据 input 框的状态，获取元素，使用 each 方法进行遍历，遍历之后，获取 id，存放到数组中
4. 使用 join 方法开始对数组数据进行处理，也就是接口需要使用的数据
5. 发送 ajax 请求即可


#### 十一、修改密码

1. 给修改密码绑定事件
<!-- 2. 校验密码是否为空，如果为空，提示用户需要输入密码 -->
3. 开始发送 ajax

#### 十二、添加分类

1. 获取事件源
2. 获取需要添加的数据
3. 发送 ajax 请求


#### 十二、获取分类列表

1. 发送 ajax ，获取数据
2. 声明模板引擎，
3. 使用 template 方法，将数据和模板进行拼接
4. 将生成的 HTML 插入到父级


#### 十三、文章修改功能

1. 给编辑按钮使用事件委托绑定事件，自定义属性 data-id ，用来获取id
2. 根据获取到的 id ，使用 ajax 获取所需要更新的那个分类
3. 将原先的发布布局改成模板，然后数据和模板进行拼接，生成 html, 替换到发布区域
4. 发送 ajax , 刷新页面


#### 十四、文章删除功能

1. 给删除按钮使用事件委托绑定事件，自定义属性 data-id ，用来获取id
2. 发送 ajax , 刷新页面


#### 十五、文章发布功能

1. 进入文章发布页面，获取 分类
2. 图片上传， new FormData() ， this.files[0], 
   然后把图片使用 append 追加到 FormData 对象中里
3. 使用 sumit 事件发送 ajax 之前，给 input 绑定 name 属性 
4. 发送 ajax 


#### 十六、文章筛选功能

1. 首先发送 ajax ，获取分类数据
2. 给 form 表单绑定 id ，绑定自提交事件 submit
3. $(this).serialize() 获取数据， 将数据 放到 ajax 的 data 中







