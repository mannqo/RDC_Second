## 功能

### 1、登录

+ 未登录时，显示“请先进行登录”字样，无法使用其他功能
+ 未登录时，点击写文章按钮，会弹出登录框
+ 登录时，会一些简单的提示(填写账号密码，账号或密码错误，账号在别处登陆过了等)。
+ 登录之后，会渲染主页文章(第一页)，页面右侧布局发生改变

### 2、主页（首页）

+ 不管在哪个页面，点击header上的首页都会跳转到首页

+ 渲染主页文章(懒加载功能，当滚动条滑倒底的时候，触发获取第二页主页文章的请求，以此类推)
+ 点赞、点踩的功能【已点赞(绿)或点踩(蓝)】
+ 点击文章标题进入文章详情
  + 点击作者的名称可以进入作者的个人主页
  + 可以通过关注按钮关注用户
  + 评论和回复可以发表`emoji`表情
+ 评论和回复有显示回复的对象
  
+ 当滚动条滑到一定的位置时，右侧的图片及位置会发生改变

### 3、个人主页

+ 点击文章会显示用户写的文章
+ 点击 赞-文章 显示点赞的文章
+ 点击 更多-关注 显示关注用户
  + 点击关注者显示关注用户
  + 点击昵称进入其个人主页，(昵称点击事件失效，编辑资料按钮消失，当再次进入自己的主页时候会再次出现)
  + 右侧均有关注/未关注按钮
+ 点击 自己的昵称 或者 编辑个人资料 都可以进入编辑个人资料的页面

### 4、编辑资料

+ 可以修改头像，用户名和个人介绍，修改后立刻刷新
+ 点击 返回个人主页 会返回个人主页

### 5、写文章

+ 必填文章标题和内容
+ hover到icon上面会立亮
+ 点击 返回主页或首页 均返回主页
+ 点击 头像-个人主页 跳转到个人主页

## 出现的问题

+ 主页获取时，接口给的数据是每一页10篇文章。最后是通过递归的方式+把一页请求的数据通过`concat`合并在一个数组中进行操作
+ 获取评论还有回复也是通过递归

+ `axios`返回数据使用for循环渲染时有时候会产生乱序的问题

  + 这个是因为同时对一个接口发送请求而请求时间不同导致的
  + 解决方法，把`axios`的返回数据先存储到一个数组中再进行操作
  + 缺点：同步变异步导致请求时间变长。

+ 用户写的文章(接口没有返回`isThumbUp`，点赞按钮初始不会亮)

+ 头像有时会裂开，似乎是因为部分返回数据不完整

  ![image-20210503211200385](C:\Users\MaNqo\AppData\Roaming\Typora\typora-user-images\image-20210503211200385.png)

+ 下面这个是查看文章详情的

![image-20210503211217301](C:\Users\MaNqo\AppData\Roaming\Typora\typora-user-images\image-20210503211217301.png)

+ 操作过快会出现问题
+ 接口：通过正则表达式把style样式去掉