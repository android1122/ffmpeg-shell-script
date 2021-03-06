# FFmpeg Shell Script
Bash Script Examples with FFmpeg, 使用FFmpeg批量处理视频文件

## 一些实例

- [Cut videos 批量去片尾，去掉视频末尾3秒](cut.sh)
- [Crop videos 批量裁剪视频，暴力方法去某音上下水印](crop.sh)

## 常见问题

### 剪辑视频
```
ffmpeg -ss 00:03:00 -i video.mp4 -t 60 -c copy cut.mp4
```
-ss后面指定的时间轴，-t后面指定时长单位为秒。为什么要将-ss放在-i前面？因为官方文档推荐这样做，这样做剪辑出来的视频时间轴更精准，并且速度更快。还有一个参数-to放在-i video.mp4后面，作用是指定剪辑时长，例如-to 00:02:00，当-ss放在-i前面的时候，这个-to剪辑出来的是-ss指定的时间轴加上-to指定的时间，比如-ss 00:01:00 -i video.mp4 -to 00:02:00，则剪辑出来的视频，是原视频00:01:00到00:03:00的片段。如果想把片头给去掉则指定了时间轴就不要添加-to和-t参数。

-to参数实例
```
ffmpeg -ss 00:03:00 -i video.mp4 -to 00:02:00 -c copy cut.mp4
```
以上命令代表将原视频文件00:03:00到00:05:00的片段剪辑出来，生成为cut.mp4文件在当前文件夹，并且使用编码为copy复制源视频文件的编码格式。

去除片头
```
ffmpeg -ss 00:03:00 -i video.mp4 -c copy cut.mp4
```
去除片头，就不需要添加-to或者-t参数，那么则是剪辑00:03:00到视频结尾。
