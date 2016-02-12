# layout設置
手機螢幕部分只要眼睛看的見的幾乎都是控制項，叫做View
有以下屬性

    android:layout_width  為控制項的寬度

    android:layout_height  為控制項的高度

單位可以填dip，也是最常用的，就是單位螢幕點(相對長度)，依解析度和螢幕尺寸不同而會有不同

也可以填像素px啦 (這樣會失去自動調整的能力，官方不建議)

也可以填以下屬性：

    "fill_parent"    代表填滿父控制項，在這裡通常是指撐滿螢幕(寬度或是高度)

    "wrap_content" 就是指依照你內容有多少就給你多少(寬度或是高度)

##layout
    > xmlns:android="http://schemas.android.com/apk/res/android"   
這句話絕對不能省略，放在最外層的那控制項即可

 
