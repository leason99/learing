Layout檔

##textview
手機螢幕部分只要眼睛看的見的幾乎都是控制項，叫做**View**

有以下屬性

    android:layout_width  為控制項的寬度

    android:layout_height  為控制項的高度

單位可以填dip，也是最常用的，就是單位螢幕點(相對長度)，依解析度和螢幕尺寸不同而會有不同

也可以填像素px啦 (**這樣會失去自動調整的能力**，官方不建議)

也可以填以下屬性：

    "fill_parent"    代表填滿父控制項，在這裡通常是指撐滿螢幕(寬度或是高度)

    "wrap_content"    就是指依照你內容有多少就給你多少(寬度或是高度)


android:text  就是要顯示的文字拉


"@string/hello" 這樣就是在指，去string.xml找到名為hello的字串，當然也可以直接打上去拉，只是不建議這樣做，以後有關多國語言會提到


這裡是string.xml，路徑在res/value/string.xml

    <?xml version="1.0" encoding="utf-8"?>
    <resources> 
       <string name="hello">Hello World, main!</string>

       <string name="app_name">Hello World test</string>
    </resources> 

 

之後會提到android:id的部分，這裡先不提
-----------------------------------------------------------

再來講

LinearLayout 

這種Layout的家族統稱稱為ViewGroup

ViewGroup可以想成各種View的群組，有以下幾種

AbsoluteLayout
RelativeLayout
FrameLayout
LinearLayout
通常也最常用的就是LinearLayout，原因無他，只是方便好用

LinearLayout只會做一件事，指定一個方向(垂直或是水平)

然後不管控制項有多大，全部照樣往下(或往右)排排站

 

在這裡LinearLayout有以下屬性

xmlns:android="http://schemas.android.com/apk/res/android"   這句話絕對不能省略，放在最外層的那控制項即可

依據XML的特性，要去指定一些標籤的定義，就像法條才會有憑有據

android:orientation="vertical"   就是排列方向為垂直(由上而下)

android:orientation="horizontal"   就是排列方向為水平(由左而右)

 

-----------------------------------------------------------

講一下

RelativeLayout 

好了

在Layout檔看起來如下：

 

<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android" 

    android:layout_width="fill_parent"

    android:layout_height="fill_parent"

    >

 

</RelativeLayout>

看起來跟LinearLayout沒啥不同

但多的特性就多了

首先，他沒有android:orientation可以用，因為他是用控制項的相對位置去編排的

如果控制項沒有設定那些多出來的參數，很有可能會發生二控制項重疊

裡面的控制項屬性會多出二種類型的屬性

邊框位置
跟另一個控制項的相對位置
屬性有以下：

 

android:layout_alignLeft 

android:layout_toRightOf 

android:layout_below 

android:layout_above 

android:layout_alignParentLeft 

android:layout_alignParentTop 

android:layout_alignParentRight 

android:layout_alignParentBottom 

android:layout_centerInParent 

 

 

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

android:layout_toRightOf        這在(等下要寫的控制項的名)的右邊

android:layout_below        這在(等下要寫的控制項名)的下面

android:layout_above       這在(等下要寫的控制項名)的上面

 

這個等下要寫控制項的名稱，很重要

控制項的順序也很重要

基本上，這個名子一定要再你的Layout上有提及

還有這個控制項名稱要在XML敘述上比現在這個控制項還要早出現

XML的Layout檔上基本上可以先寫靠左或靠右對齊的控制項敘述

才寫這種相對敘述

 

控制項在XML裡寫的順序很重要

-----------------------------------------------------

 

 

補充：FrameLayout 

 

FrameLayout可以想成是RelativeLayout的功能閹割版

 

RelativeLayout的部份

 

1. 能對齊View的框邊

例如:

android:layout_alignParentLeft  靠左對齊，(吸附邊框左邊)

或是

2. 設定二格View之間的排列關係

例如:

android:layout_toLeftOf       這在(等下要寫的控制項的名)的左邊

上面都提過了

 

 

而FrameLayout只剩下

 

對齊View的框邊的功能

用android:layout_gravity  來指定

如果在其中的View有二個設定成一樣的話呢

就會「依序」重疊上去

 

注意一點，只有RelativeLayout和FrameLayout 

才會發生控制項有重疊的現象

如果版面看似調不出來，可以檢查一下是否為二個控制項重疊

或是版面出界了

 

版面出界的狀況在初期很容易發生

 

像是LinearLayout 裡面有二個控制項

而

第一個控制項是  android:layout_width="fill_parent"    android:layout_height="fill_parent"

填滿全螢幕

第二個  android:layout_width="wrap_content"    android:layout_height="wrap_content"

這樣第二個一定出界的

 

設定上要小心

 

-----------------------------------------------------

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

 

-----------------------------------------------------

底下寫一個LinearLayout的範例，改用RelativeLayout會怎麼寫

 

現在用LinearLayout來撰寫Layout

 

<?xml version="1.0" encoding="utf-8"?>

<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"

    android:orientation="vertical"

    android:layout_width="fill_parent"

    android:layout_height="fill_parent"

    >

<TextView 

    android:id="@+id/tv01"

    android:layout_width="wrap_content"

    android:layout_height="wrap_content"

    android:text="Text01"

    />

    <TextView 

    android:id="@+id/tv02" 

    android:layout_width="wrap_content"

    android:layout_height="wrap_content"

    android:text="Text02"

    />

    <TextView 

    android:id="@+id/tv03"

    android:layout_width="wrap_content"

    android:layout_height="wrap_content"

    android:text="Text03"

    />

    <TextView 

    android:id="@+id/tv04"

    android:layout_width="wrap_content"

    android:layout_height="wrap_content"

    android:text="Text04"

    />

    <TextView 

    android:id="@+id/tv05"

    android:layout_width="wrap_content"

    android:layout_height="wrap_content"

    android:text="Text05"

    />

</LinearLayout>

 

 

-----------------------------------------------------

改用RelativeLayout會變成

 

 

<?xml version="1.0" encoding="utf-8"?>

<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"

    android:layout_width="fill_parent"

    android:layout_height="fill_parent"

    >

<TextView 

    android:id="@+id/tv01"

    android:layout_alignParentTop="true"

    android:layout_alignParentLeft="true"

    android:layout_width="wrap_content"

    android:layout_height="wrap_content"

    android:text="Text01"

    />

    <TextView 

    android:id="@+id/tv02" 

    android:layout_below="@id/tv01"

    android:layout_width="wrap_content"

    android:layout_height="wrap_content"

    android:text="Text02"

    />

    <TextView 

    android:id="@+id/tv03"

    android:layout_below="@id/tv02"

    android:layout_width="wrap_content"

    android:layout_height="wrap_content"

    android:text="Text03"

    />

    <TextView 

    android:id="@+id/tv04"

    android:layout_below="@id/tv03"

    android:layout_width="wrap_content"

    android:layout_height="wrap_content"

    android:text="Text04"

    />

    <TextView 

    android:id="@+id/tv05"

    android:layout_below="@id/tv04"

    android:layout_width="wrap_content"

    android:layout_height="wrap_content"

    android:text="Text05"

    />

</RelativeLayout>

 

 

 

 
