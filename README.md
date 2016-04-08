#HTML5 Based File Uploader
#Dropup

##使用方法

#####引入Dropup文件

CommonJS 方式引用
```
var Dropup = require('dropup.js');
```

AMD 方式引用
```
define(['./dropup'], function(Dropup) {
    // ...
});
```

全局方式，在HTML页面中引入:
```
<script src="dropup.min.js"></script>
```


###HTML代码
__提示:__</br>
1、上传多个文件时，file input要添加multiple属性</br>
2、android系统选择文件，file input要添加capture="camera"属性，才能打开相机</br>
3、如果未添加html代码或未指定fileInput参数，插件会自动生成一个图片选择控件
```
<input class="du-fileinput" type="file" accept="image/*" capture="camera" style="display:none;" />
```
###Javascript代码
```
new Dropup(container, params);
```
Example：
```
new Dropup(".dropup-avatar", {
    url: "http://localhost/upload",
    fileInput: ".du-fileinput",
    maxFilesize: 500,
    onSuccess: function(du, file, response) {
        $('.album-image').attr('src', 'http://localhost/' + file.url);
        $('#album-image').val(file.url);
    },
    onError: function(du, file, message) {
        alert(message);
    }
});
```
###服务器端
数据返回格式必须为json格式，数据结构如下：</br>
code: 0：表示正常，> 0的值表示有错误</br>
message: 提示信息</br>
data: 返回数据
```
{"code": 0, "message": "ok", "data": {"url": "upload/avatar/example.jpg"}}
```
__提示:__</br>
如果返回的数据格式和上面的不一样，插件也会触发onSuccess()回调，但是需要自己处理返回结果

##参数
### 
<table>
<thead>

<tr>
  <th>参数</th>
  <th>类型</th>
  <th>默认值</th>
  <th>说明</th>
</tr>
</thead>
<tbody>
<tr><th colspan="4">构造参数</th></tr>
<tr>
  <td>container</td>
  <td>string or HTMLElement</td>
  <td></td>
  <td>拖拽敏感区域</td>
</tr>
<tr>
  <td>params</td>
  <td>object</td>
  <td>{}</td>
  <td>可选参数</td>
</tr>
<tr>
  <th colspan="4">params参数</th>
</tr>
<tr>
  <td>url</td>
  <td>string</td>
  <td>null</td>
  <td>ajax上传地址</td>
</tr>
<tr>
  <td>method</td>
  <td>string</td>
  <td>POST</td>
  <td>提交方式</td>
</tr>
<tr>
  <td>multipart_params</td>
  <td>object</td>
  <td>{}</td>
  <td>表单参数，和上传请求同时发送</td>
</tr>
<tr>
  <td>withCredentials</td>
  <td>boolean</td>
  <td>false</td>
  <td>支持跨域发送cookies</td>
</tr>
<tr>
  <td>allowExts</td>
  <td>string</td>
  <td>null</td>
  <td>允许的文件类型, 格式: 扩展名[,扩展名], 如: <code>jpeg,jpg,png,gif</code>,多个类型使用逗号<code>,</code>隔开</td>
</tr>
<tr>
  <td>maxFilesize</td>
  <td>int</td>
  <td>256</td>
  <td>单个文件限制 KB</td>
</tr>
<tr>
  <td>maxFiles</td>
  <td>int</td>
  <td>null</td>
  <td>最大上传数</td>
</tr>
<tr>
  <td>parallelUploads</td>
  <td>int</td>
  <td>2</td>
  <td>并行上传量，在进行多文件同时上传时的并发量</td>
</tr>
<tr>
  <td>auto</td>
  <td>boolean</td>
  <td>true</td>
  <td>自动上传，选择文件后自动执行上次文件动作</td>
</tr>
<tr>
  <td>multi</td>
  <td>boolean</td>
  <td>true</td>
  <td>允许多文件上传，头像修改建议设为false，或者将file input的multiple去掉</td>
</tr>
<tr>
  <td>init</td>
  <td>boolean</td>
  <td>true</td>
  <td>默认初始化</td>
</tr>
<tr>
  <td>debug</td>
  <td>boolean</td>
  <td>false</td>
  <td>开启调试信息</td>
</tr>
<tr>
  <td>fileInput</td>
  <td>string or HTMLElement</td>
  <td>null</td>
  <td>HTML file控件, 若此参数不填，会自动生成一个图片控件</td>
</tr>
<tr>
  <td>fileDataName</td>
  <td>string</td>
  <td>file</td>
  <td>file数据名</td>
</tr>
<tr>
  <td>clickable</td>
  <td>boolean</td>
  <td>true</td>
  <td>拖拽敏感区域是否可点击</td>
</tr>
<tr>
  <td>usedFastClick</td>
  <td>boolean</td>
  <td>false</td>
  <td>是否使用了FastClick, 如果同时运行的其他插件有使用FastClick的情况，需要开启这个参数hack BUG</td>
</tr>
<tr>
  <th colspan="4">提示文字(Tips Text)</th>
</tr>
<tr>
  <td>txtFileTooBig</td>
  <td>string</td>
  <td>文件上传限制最大为{{maxFilesize}}.</td>
  <td>文件大小超过限制</td>
</tr>
<tr>
  <td>txtInvalidFileType</td>
  <td>string</td>
  <td>不允许的文件类型</td>
  <td>文件类型不允许</td>
</tr>
<tr>
  <td>txtMaxFilesExceeded</td>
  <td>string</td>
  <td>最多能上传{{maxFiles}}个文件</td>
  <td></td>
</tr>
<tr>
  <td>txtCancelUploadTips</td>
  <td>string</td>
  <td>“您确定要取消上传吗？</td>
  <td></td>
</tr>
<tr>
  <th colspan="4">回调函数（Callback)</th>
</tr>
<tr>
  <td>onDragHover</td>
  <td>function()</td>
  <td></td>
  <td>文件拖放，(注意)dragover事件一定要清除默认事件，不然会无法触发后面的drop事件</td>
</tr>
<tr>
  <td>onDragOver</td>
  <td>function()</td>
  <td></td>
  <td>拖拽到敏感区域</td>
</tr>
<tr>
  <td>onDragLeave</td>
  <td>function()</td>
  <td></td>
  <td>离开敏感区域</td>
</tr>
<tr>
  <td>onDrop</td>
  <td>function(du, file)</td>
  <td></td>
  <td>文件选择后</td>
</tr>
<tr>
  <td>onProgress</td>
  <td>function(du, file)</td>
  <td></td>
  <td>上传进度</td>
</tr>
<tr>
  <td>onSuccess</td>
  <td>function(du, file, response)</td>
  <td></td>
  <td>上传成功</td>
</tr>
<tr>
  <td>onError</td>
  <td>function(du, file, response)</td>
  <td></td>
  <td>上传失败</td>
</tr>
<tr>
  <td>onCanceled</td>
  <td>function(du, file)</td>
  <td></td>
  <td>上传取消</td>
</tr>
<tr>
  <td>onDelete</td>
  <td>function(du, file)</td>
  <td></td>
  <td>文件删除</td>
</tr>
<tr>
  <td>onComplete</td>
  <td>function(du)</td>
  <td></td>
  <td>文件全部上传完毕</td>
</tr>
<tr>
  <th colspan="4">回调函数（Callback)</th>
</tr>
<tr>
  <td>file</td>
  <td>object</td>
  <td></td>
  <td>文件对象数据结构，例如: <code>{id: "kQtmYe2Mi07w0Z-T67cTzMmHixHB3Chx", name: "example.jpg", percent: "100.00", size: 8172, src: "", status: "success", type: "image/jpeg"}</code></td>
</tr>
</tbody></table>
