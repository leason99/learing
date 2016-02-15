# layout設置

 [Manifest.xml:xmlns](https://sites.google.com/site/givemepassxd999/android/fen-ximanifest-xml)
  
    mlns:android="http://schemas.android.com/apk/res/android"
    xmlns是xml namespace的縮寫,代表著宣告用android:這個變數為"http://schemas.android.com/apk/res/android"這串網址,
    這樣的就可以直接使用網址內那個檔案所提供的屬性。
  
 [TOOLS屬性](http://www.xlgps.com/article/48068.html)
  
   *Tools: context*
   
    這個屬性基本上是設定在 Activity 的 Layout XML 的根元素 (root element) 上
    記錄該 Layout 所屬的 Activity/Activities (一個 Layouy可以被多個 Activity 重複使用)
    藉由記錄該 Layout 所屬的 Activity 這個動作，Android Studio 便能夠取得該 Activity 的佈景主題 
    (theme，每個 Activity 可以有自己所要套用的 theme)，並且在 Preview 視窗中顯示套用套用該主題後的預覽畫面。
    
 [stytle,theme](http://xnfood.com.tw/style-theme/#declare_02)
 [button style](http://ithelp.ithome.com.tw/question/10156770)
 [textsize,單位,像素](https://magiclen.org/android-screen/)
 
   SP(Scale-independent Pixel)
SP常用來當作文字的長度，基本上SP就是DP(在字型大小100%的時候)，但是SP可以再隨著系統的字型大小設定做倍率的縮放。在Android系統中，如果要讓文字大小可以被使用者在系統設定中的字型大小影響，那就使用SP單位指定文字大小吧！
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
  Layout的家族統稱稱為ViewGroup
  *   AbsoluteLayout
  *   RelativeLayout
  *   FrameLayout
  *   LinearLayout

 > xmlns:android="http://schemas.android.com/apk/res/android"
 
   這句話絕對不能省略，放在最外層的那控制項即可
    
    
    android:orientation="vertical"   就是排列方向為垂直(由上而下)

    android:orientation="horizontal"   就是排列方向為水平(由左而右)
###RelativeLayout
他沒有android:orientation可以用，因為他是用控制項的相對位置去編排的

邊框位置

先有一個控制項位置做絕對位置，才能做相對位置的判定嘛

以word的文字編排方式可以很直覺的理解

    android:layout_alignParentLeft  靠左對齊，(吸附邊框左邊)

    android:layout_alignParentTop   靠上對齊，(吸附邊框上方)

    android:layout_alignParentRight   靠右對齊，(吸附邊框右邊)

    android:layout_alignParentBottom   靠下對齊，(吸附邊框下方)

    android:layout_centerInParent    置中，(計算放在正中間)

這類型就是以RelativeLayout的邊框做位置，做對齊
而另一種就是以別人的控制項位置做為自己的控制項位置

    android:layout_toLeftOf       這在(等下要寫的控制項的名)的左邊
    
    android:layout_toRightOf    這在(等下要寫的控制項的名)的右邊
   
    android:layout_below        這在(等下要寫的控制項名)的下面
    
    android:layout_above       這在(等下要寫的控制項名)的上面
###FrameLayout
 FrameLayout可以想成是RelativeLayout的功能閹割版
 只剩下對齊View的框邊的功能
##ID
所有的View和ViewGroup都可能需要android:id這東西

他會在Compile專案時會產生一個R檔，就是gen/你的package名稱/R.java

這個R檔會包含你的所有Layout上的所有id和string.xml上的名稱....等等內容，沒事別去動他

寫法如下

    android:id="@+id/tv01"

這裡的@就是叫程式去R檔裡面找到代稱叫做tv01的id名稱

這裡的+號不能省略，代表的是我需要在R檔裡新增一個id名稱叫做

這個所有的Layout檔都適用，不同Layout裡的控制項id最好是要不一樣

在一個Layout檔中，控制項的id一定要不同

到時候程式可以用findViewById去依照這個id抓取其控制項
[findviewbyid](http://www.2cto.com/kf/201204/127405.html)
