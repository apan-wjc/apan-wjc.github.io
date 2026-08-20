### Controls
For local video, there are a few options for controls:  
```html
<video width="900" controls autoplay muted loop poster="../assets/thumbnail.jpg">
```

|Attribute|Effect|
|-|-|
|autoplay|Starts playing automatically (usually needs muted too, since browsers block unmuted autoplay)|
|muted|Starts silent|
|loop|Repeats when finished|
|poster="..."|Thumbnail image shown before playback starts|

### Local Video
Due to Github file size limitation, `mv assets/4K_Wujiaochang_Shanghai_China360.mp4 /opt/video/` to avoid load video to Github.  
So, this sample is NOT working since the video file cannot be found.
<div style="text-align:center;">
<video width="900" height="600" controls>
  <source src="/opt/video/4K_Wujiaochang_Shanghai_China360.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
</div>

### Video Link Embed
使用HTML的iframe可以嵌入各大平台的视频，例如YouTube：
<div style="text-align:center;">
<iframe width="900" height="600" src="https://www.youtube.com/embed/Xq8ABGnBsdY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encr>
</div>
