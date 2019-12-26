### 基于AudioContext&Canvas的音乐旋律可视化web应用

##### by 白玉 16307130362

本项目实现了一个音乐可视化的WEB应用，使用AudioContex接口对音频文件进行处理，使用Canvas对音频情况进行可视化。

#### 使用Web-AudioContext接口对音频文件进行解码处理

**`AudioContext`**接口表示由音频模块连接而成的音频处理图，每个模块对应一个[AudioNode](https://developer.mozilla.org/zh-CN/docs/Web/API/AudioNode)。**`AudioContext`**可以控制它所包含的节点的创建，以及音频处理、解码操作的执行[1]。 本项目基于`AudioContext`这一web接口，采用以下的步骤进行音频解码并进行播放

1. 将音频文件以`Arraybuffer`形式读入

2. 使用`AudioContext.decodeAudioData()`接口将上一步骤中`ArrayBuffer`形式的音频对象进行异步解码

3. 使用`AudioContext.createBufferSourece()`接口创建一个`AudioBufferSourceNode`对象，表示一个音频源。

4. 将2中异步解码成功后的`buffer`赋值给3中`AudioBufferSourceNode`对象的`buffer`属性，即定义播放的音频为解码后的音频。
5. 使用`AudioContext.createAnalyser()`创建`AnalyserNode`，获取音频时间和频率数据的相关接口。
6. 使用`AudioBufferSourceNode`对象的`connect()`方法将5中的`AnalyzerNode`连接到4中的`AudioBufferSourceNode`。
7. 使用`AudioBufferSourceNode`对象的`start()`方法进行播放。

#### 使用Canvas进行音频数据可视化

`<canvas>`是一个可以使用脚本(通常为Javascript)来绘制图形的 HTML元素.例如,它可以用于绘制图表、制作图片构图或者制作简单的动画[2]。本项目基于canvas技术，将解码后音频的数据进行可视化，采用以下的步骤

1. 调用6中完成连接后的`AnalyzerNode`对象的`frequencyBinCount`方法获取音频的频率数据
2. 通过1中获取的频率数据进行canvas绘画，本项目实现了柱状矩形与点圆形两种可视化。
   1. 每次绘制时清空上次画布内容。
   2. 使用`canvas`的相关接口进行举行绘制或点圆绘制。
3. 使用·requestAnimationFrame反复进行1.2步骤，即反复收集频率数据与绘画，实现音频频谱动态变化的动画，完成了音频的可视化。

#### 参考资料

[1] https://developer.mozilla.org/zh-CN/docs/Web/API/AudioContext

[2] https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API/Tutorial



