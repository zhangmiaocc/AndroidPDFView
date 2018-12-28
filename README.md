# AndroidPDFView
#### My Blog：[zhangmiao.cc](https://zhangmiao.cc/posts/44884a58.html)
参考自：https://github.com/barteksc/AndroidPdfViewer

## 安装

添加到*build.gradle*：

`compile 'com.github.barteksc:android-pdf-viewer:3.1.0-beta.1'`

或者如果你想使用更稳定的版本：

`compile 'com.github.barteksc:android-pdf-viewer:2.8.2'`

库在jcenter存储库中可用，可能它很快就会在Maven Central中。

## ProGuard的

如果您使用的是ProGuard，请将以下规则添加到proguard配置文件中：

```java
-keep class com.shockwave.**
```

## 在布局中包含PDFView

```
<com.github.barteksc.pdfviewer.PDFView
        android:id="@+id/pdfView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
```

## 加载PDF文件

所有可用选项都带有默认值：

```java
pdfView.fromUri(Uri)
or
pdfView.fromFile(File)
or
pdfView.fromBytes(byte[])
or
pdfView.fromStream(InputStream) // stream is written to bytearray - native code cannot use Java Streams
or
pdfView.fromSource(DocumentSource)
or
pdfView.fromAsset(String)
    .pages(0, 2, 1, 3, 3, 3) // all pages are displayed by default
    .enableSwipe(true) // allows to block changing pages using swipe
    .swipeHorizontal(false)
    .enableDoubletap(true)
    .defaultPage(0)
    // allows to draw something on the current page, usually visible in the middle of the screen
    .onDraw(onDrawListener)
    // allows to draw something on all pages, separately for every page. Called only for visible pages
    .onDrawAll(onDrawListener)
    .onLoad(onLoadCompleteListener) // called after document is loaded and starts to be rendered
    .onPageChange(onPageChangeListener)
    .onPageScroll(onPageScrollListener)
    .onError(onErrorListener)
    .onPageError(onPageErrorListener)
    .onRender(onRenderListener) // called after document is rendered for the first time
    // called on single tap, return true if handled, false to toggle scroll handle visibility
    .onTap(onTapListener)
    .onLongPress(onLongPressListener)
    .enableAnnotationRendering(false) // render annotations (such as comments, colors or forms)
    .password(null)
    .scrollHandle(null)
    .enableAntialiasing(true) // improve rendering a little bit on low-res screens
    // spacing between pages in dp. To define spacing color, set view background
    .spacing(0)
    .autoSpacing(false) // add dynamic spacing to fit each page on its own on the screen
    .linkHandler(DefaultLinkHandler)
    .pageFitPolicy(FitPolicy.WIDTH)
    .pageSnap(true) // snap pages to screen boundaries
    .pageFling(false) // make a fling change only a single page like ViewPager
    .nightMode(false) // toggle night mode
    .load();
```

####  <span style="color:red">注意</span>

`pages` 是可选的，它允许您根据需要过滤和排序PDF页面
