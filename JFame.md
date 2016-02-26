# Jframe
  
  public class sendUI extends JFrame {
  
  
  ```
  public void myframe (String Title, String image, int SizeX, int SizeY) extends JFrame {
  
          //constructor
       public myframe(){
          
          //inition something here
       
       }
       //own method
       }
```
 
##Set
 
###setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); //退出方式
  
  + DO_NOTHING_ON_CLOSE：不執行任何操作
  + HIDE_ON_CLOSE：自動隱藏該表單。
  + DISPOSE_ON_CLOSE：自動隱藏並釋放該表單
  + EXIT_ON_CLOSE：使用 System exit 方法退出應用程式。僅在應用程式中使用。
  + 預設情況下，該值被設置為 HIDE_ON_CLOSE。*/
        
        
        
###setTitle(Title); //標題名稱
        
###ImageIcon ico = new ImageIcon(image); //圖標創建("當前程式目錄下儲存圖片的檔案名/圖片名.gif或.jpg")//"image/Title.gif"
        
###setIconImage(ico.getImage()); //圖標設定
        
###setSize(SizeX, SizeY); //設定視窗大小
        
###setLocationRelativeTo(this); //設定視窗初始位置在螢幕中心
        
###setResizable(true); //設定視窗大小可變
        
###setExtendedState(JFrame.MAXIMIZED_BOTH); //設定最大化顯示
        
###setVisible(true); //設定視窗可見
-------------------
myframe.disposed(); /釋放該表單
