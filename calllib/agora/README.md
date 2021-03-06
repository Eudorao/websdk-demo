## CallLib

### 使用说明

1、开通音视频服务，请参考 [音视频开通指南](http://www.rongcloud.cn/docs/call.html#open)

2、引入 WebSDK

```
<script src="https://cdn.ronghub.com/RongIMLib-2.3.2.js"></script>
```

3、引入 Web CallLib

将以下文件下载到项目中，修改 `src` 的相对路径

```
<script src="./AgoraRTCSDK-2.0.0.js"></script>

<script src="../rong-calllib-util.js"></script>

<script src="./rong-calllib-agora.js"></script>

<script src="../rong-calllib-sendmsg.js"></script>

<script src="../rong-calllib.js"></script>
```

4、WebSDK 连接融云服务器，可参考 https://github.com/rongcloud/websdk-demo/blob/master/calllib/init.js

5、发起音视频通话

### 启动示例

1、修改 `config` 的 `appKey`、`private`、`group` 属性中的 `userid` 和 `token`

2、访问 `private.html` 或者 `group.html`

### API 说明
    
#### videoWatch

方法： `RongCallLib.videoWatch(watcher);` 

描述： 监控视频流，当有人加入、离开会触发此监听
   
示例：

```js
RongCallLib.videoWatch(function(result){
    /*
        
        result 有 3 种情况，具体如下：

        // 有成员加入房间，此时可向页面追加视频流
        result => { 
            type: 'added', 
            data: 'video 节点',
            // true 表示自己的音视频流，反之是对方的
            isLocal: true
        }
        
        // 有成员离开房间，可移除 video 节点
        result => { 
            type: 'removed', 
            data: 'video 节点 Id'
        }

        //有成员加入房间
        result => { 
            type: 'joined', 
            userId: 'userId'
        }
    */
});
```
    
#### commandWatch

方法： `RongCallLib.commandWatch(watcher);` 

描述： 接收指令，根据指令操作 UI，按钮
   
示例：

```js
RongCallLib.commandWatch(function(command){
    // command => 消息指令, 详细可参考：http://www.rongcloud.cn/docs/web_calllib.html#message
});

```
#### call

方法： `RongCallLib.call(params, callback);` 

描述： 发起音视频通话
   
示例：

```js
var CallType = RongIMLib.VoIPMediaType;

var params = {
    // 会话类型，请参考: http://rongcloud.cn/docs/web_api_demo.html#conversation_type
    conversationType: conversationType,
    // 会话目标 Id，群 Id 或者 userId 
    targetId: targetId,
    // 被邀请人 Id , 多人视频填写多个 userId, 一对一和 targetId 值一致
    inviteUserIds: inviteUserIds,
    // 音频类型
    // CallType.MEDIA_VEDIO
    // CallType.MEDIA_AUDIO
    mediaType: CallType.MEDIA_VEDIO
};
RongCallLib.call(params, function(error){
    // do something...
});
```

#### accept

方法： `RongCallLib.accept();` 

描述：接听电话邀请
   

示例：

```js
var CallType = RongIMLib.VoIPMediaType;

var params = {
    // 会话类型，请参考: http://rongcloud.cn/docs/web_api_demo.html#conversation_type
    conversationType: conversationType,
    // 会话目标 Id，群 Id 或者 userId 
    targetId: targetId,
    // 音频类型
    // CallType.MEDIA_VEDIO
    // CallType.MEDIA_AUDIO
    mediaType: CallType.MEDIA_VEDIO
};
RongCallLib.accept(params);
```

#### hungup

方法： `RongCallLib.hungup(params, callback);` 

描述： 挂断音视频通话
   
示例：

```js
var params = {
    // 会话类型，请参考: http://rongcloud.cn/docs/web_api_demo.html#conversation_type
    conversationType: conversationType,
    // 会话目标 Id，群 Id 或者 userId 
    targetId: targetId,   
};
RongCallLib.hungup(params, function(error, summary){
    // summary => 音视频通话汇总信息
});
```
#### reject

方法： `RongCallLib.reject(params);` 

描述： 收到请求音视频指令，拒绝通话
   
示例：

```js
var params = {
    // 会话类型，请参考: http://rongcloud.cn/docs/web_api_demo.html#conversation_type
    conversationType: conversationType,
    // 会话目标 Id，群 Id 或者 userId 
    targetId: targetId
};
RongCallLib.reject(params);
```

#### mute

方法： `RongCallLib.mute();` 

描述： 关闭麦克风

示例：

```js
RongCallLib.mute();
```

#### unmute

方法： `RongCallLib.unmute();` 

描述： 打开麦克风
   
示例：

```js
RongCallLib.unmute();
```

#### videoToAudio

方法： `RongCallLib.videoToAudio;` 

描述： 视频转音频
   
示例：

```js
RongCallLib.videoToAudio();
```

#### audioToVideo

方法： `RongCallLib.audioToVideo();` 

描述： 音频转视频

示例：

```js
RongCallLib.audioToVideo();
```