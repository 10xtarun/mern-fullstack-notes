# How to handle media in HTML?

In HTML, images, videos, and audios can be handled using specific elements and attributes to embed them into web pages. Here are examples of how to handle each of them:

### Images:

Images can be displayed on a webpage using the `<img>` element. The src attribute specifies the URL of the image, and the alt attribute provides alternative text for screen readers and in case the image cannot be displayed.

Example:
```html
<img src="image.jpg" alt="Description of image">
```

### Videos:

Videos can be embedded in a webpage using the `<video>` element. The src attribute specifies the URL of the video file, and the `<source>` element allows specifying multiple video formats for better browser compatibility. Additional attributes such as controls enable the default playback controls, and autoplay enables automatic playback.

Example:
```html
<video width="320" height="240" controls autoplay>
    <source src="video.mp4" type="video/mp4">
    <source src="video.webm" type="video/webm">
    Your browser does not support the video tag.
</video>
```

### Audios:

Audio files can be included in a webpage using the `<audio>` element. Similar to videos, the src attribute specifies the URL of the audio file, and the `<source>` element allows specifying multiple audio formats. Additional attributes such as controls enable the default playback controls, and autoplay enables automatic playback.

Example:
```html
<audio controls autoplay>
    <source src="audio.mp3" type="audio/mpeg">
    <source src="audio.ogg" type="audio/ogg">
    Your browser does not support the audio tag.
</audio>
```

### Responsive Images:

To ensure that images scale properly on different devices and screen sizes, you can use the srcset attribute along with the sizes attribute to specify different image sources and their corresponding sizes. This helps in serving the most appropriate image based on the device's pixel density and screen size.

Example:
```html
<img srcset="image-320w.jpg 320w,
             image-480w.jpg 480w,
             image-800w.jpg 800w"
     sizes="(max-width: 320px) 280px,
            (max-width: 480px) 440px,
            800px"
     src="image-800w.jpg" alt="Description of image">
```

> By using these HTML elements and attributes, you can effectively handle and display images, videos, and audios on your web pages.
