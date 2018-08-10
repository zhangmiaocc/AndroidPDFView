# AndroidPDFView
#### My Blog：[`zhangmiao.cc`](zhangmiao.cc)
参考自:https://github.com/barteksc/AndroidPdfViewer
安装

添加到build.gradle：

compile 'com.github.barteksc:android-pdf-viewer:3.1.0-beta.1'

或者如果你想使用更稳定的版本：

compile 'com.github.barteksc:android-pdf-viewer:2.8.2'

库在jcenter存储库中可用，可能它很快就会在Maven Central中。

ProGuard的

如果您使用的是ProGuard，请将以下规则添加到proguard配置文件中：

    -keep class com.shockwave.**

在布局中包含PDFView

    <com.github.barteksc.pdfviewer.PDFView
            android:id="@+id/pdfView"
            android:layout_width="match_parent"
            android:layout_height="match_parent"/>

加载PDF文件

所有可用选项都带有默认值：

    pdfView.fromUri（Uri）
    
    pdfView.fromFile（文件）
    
    pdfView.fromBytes（byte []）
    
    pdfView.fromStream（InputStream）//将流写入bytearray  - 本机代码不能使用Java Streams
    
    pdfView.fromSource（DocumentSource）
    
    pdfView.fromAsset（String）
        .PAGES（0，2，1，3，3，3）//所有页面默认显示 
        .enableSwipe（真）//允许阻止改变使用滑动页 
        .swipeHorizontal（假）
        .enableDoubletap（true）
        .defaultPage（0）
         //允许在当前页面上绘制一些东西，通常在屏幕中间可见
        .onDraw（onDrawListener）
        //允许在所有页面上绘制内容，分别为每个页面绘制。仅针对可见页面调用
        .onDrawAll（onDrawListener）
        .onLoad（onLoadCompleteListener）//在加载文档并开始渲染后调用
        .onPageChange（onPageChangeListener）
        .onPageScroll（onPageScrollListener）
        .onError（onErrorListener）
        .onPageError（onPageErrorListener）
        .onRender（onRenderListener）//在第一次呈现文档后调用
        //单击时调用，如果处理则返回true，false以切换滚动句柄可见性
        .onTap（onTapListener）
        .onLongPress（onLongPressListener）
        .enableAnnotationRendering（false）//呈现注释（例如注释，颜色或表单） 
        .password（null）
        .scrollHandle（null）
        .enableAntialiasing（true）//在低分辨率屏幕上改进渲染一点
        //在dp中页面之间的间距。要定义间距颜色，请设置视图背景 
        .spacing（0）
        .autoSpacing（false）//在屏幕上添加动态间距以适应每个页面 
        .linkHandler（DefaultLinkHandler）
        .pageFitPolicy（FitPolicy 。 WIDTH）
        .pageSnap（true）//将页面捕捉到屏幕边界 
        .pageFling（false）//仅对像ViewPager 
        这样的单页进行一次更改 .nightMode（false）//切换夜间模式 
        .load（）;

<span style="color:red">注意</span>

pages 是可选的，它允许您根据需要过滤和排序PDF页面
