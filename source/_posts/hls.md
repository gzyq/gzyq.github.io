---
title: 前端直播协议使用总结 
date: 2017-03-14 21:15:22
tags: [直播,视频]
categories: note
comments: true
---
参与的很多项目是关于直播点播视频这一块的，加上最近直播比较热，有很多小伙伴对前端在移动端及PC这块有兴趣，自己就接触的一些概念和实际项目中遇到的一些问题解决方案，供参考和交流。
<!-- more --> 
## 流媒体 ##
流媒体是指采用流式传输的方式在网络上传输的多媒体文件。
流技术是把视频和声音信息经过压缩处理后放在服务器上，一边下载一边观看收听，而不需要等整个压缩文件下载到自己的终端才能观看。
### 相关 ###
编码器：H.264、H.265
解码器：解码并渲染视频内容
## 直播流程 ##
采集（录制）：视频、音频
处理：水印、美颜、降噪等
编码：将原始视频通过H.264或者H.265编码压缩，满足实时传输需要
封装：类似容器的作用，直播中主要采用的就是 FLV 和 MPEG2-TS 格式，分别用于 RTMP/HTTP-FLV 和 HLS 协议。
推送：推送协议主要RTMP、WebRTC、基于UDP的私有协议等
网络传输：LiveNet、P2P、CDN
解码：解码器将不同封装格式的视频进行解包，并将其内容解码，然后将解码后的视频帧交给操作系统进行渲染，最终让终端用户看到
播放：在终端播放

参考：[《视频直播技术详解》系列](http://blog.qiniu.com/archives/6606)
## 前端视频直播协议 ##
常见的直播协议有RTMP、HLS、HTTP-FLV、RTP，自己对RTMP和HLS接触多一些，前端可选的视频直播协议大致只有两种：HLS和RTMP。下面具体说一下这两种，目前兼容最好的是HLS协议，但HLS比RTMP有较高的延迟。
### HLS ###
#### 概念 ####
HLS（HTTP Live Streaming）是苹果公司针对iPhone、iPod、iTouch和iPad等**移动设备**而开发的基于HTTP协议的流媒体解决方案，可实现流媒体的直播和点播。
#### 原理 ####
原理：将视频流分片成一系列HTTP下载文件，即视频文件或视频流切分成小片(ts)并建立索引文件(m3u8)。支持的视频流编码为H.264，音频流编码为AAC。
简单地理解，当播放视频时，用户下载的是m3u8文件，m3u8里面是ts文件的索引地址，通过m3u8文件的索引地址找到对应的音视频文件的网络地址就可以播放具体的每个小段视频，连接起来就是一段完整的视频。
### RTMP ###
#### 概念 ####
RTMP（Real Time Messaging Protocol），实时消息传输协议，主要用来在Flash/AIR平台和支持RTMP协议的流媒体/交互服务器之间进行音视频和数据通信，RTMP是Adobe开发的协议，无法在iPhone中兼容。
#### 原理 ####
原理：RTMP协议像一个用来装数据包的容器，以客户端向服务器端发送请求开始，服务器收到请求后进行响应，
经历握手，连接，建立流，最后播放。感兴趣的小伙伴可以在网上查阅具体文档。
### 使用场景 ###
从HLS的概念就可以知道，HLS主要用于移动端播放，而在PC端，Flash对RTMP支持友好，随着HTML5的兴起，最好是都能使用HLS播放更佳，毕竟Flash需要安装插件等（自己对Flash不熟悉）。现在，通过一些插件已经可以解决这些，下面具体总结一下HLS在移动及PC中的使用。
## HLS在HTML5中使用##
###移动端 ###
HLS在移动端具有非常大的优势，可以直接打开播放，HTML5自带的video标签嵌入m3u8视频地址即可，只要有网页浏览器会自己解析，不需要单独下载插件或者APP，在iOS和安卓系统中具有很高的兼容性。

	<video id="video" src="live.m3u8" >
		<p>Your browser does not support the video tag.</p>
	</video>
	

### PC端 ###
按照在移动端相同的写法的话，可以看到，在PC端的大多主流浏览器都无法播放，显示黑屏。多数情况下，肯定还是想要一个地址，兼容PC和移动端，如果再在PC端开发Flash，无疑会增加项目开发周期且冗余，最好是需要通过一些处理，达到我们想要的效果。经过几个项目实践，hls.js可以很好的解决这个问题。
hls.js 是一个依赖HTTP Live Streaming客户端的JavaScript库。详细使用说明可参考官方文档[hls.js](https://github.com/video-dev/hls.js) 。
	
	<video id="video"></video>
	<script>
	  if(Hls.isSupported()) {
	    var video = document.getElementById('video');
	    var hls = new Hls();
	    hls.loadSource('live.m3u8');
	    hls.attachMedia(video);
	    hls.on(Hls.Events.MANIFEST_PARSED,function() {
	      video.play();
	  });
	 }
	</script>
	

注：本文主要是记录直播相关的概念技术理解，HTML5 video的详细开发使用详见另一篇文章。





