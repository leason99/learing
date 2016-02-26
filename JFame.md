### Jframe
  
  ```
  public void setWindow(String Title, String image, int SizeX, int SizeY) {
  
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); //退出方式
        setTitle(Title); //標題名稱
        
        ImageIcon ico = new ImageIcon(image); //圖標創建("當前程式目錄下儲存圖片的檔案名/圖片名.gif或.jpg")//"image/Title.gif"
        
        setIconImage(ico.getImage()); //圖標設定
        
        setSize(SizeX, SizeY); //設定視窗大小
        
        setLocationRelativeTo(this); //設定視窗初始位置在螢幕中心
        
        setResizable(true); //設定視窗大小可變
        
        setExtendedState(JFrame.MAXIMIZED_BOTH); //設定最大化顯示
        
        setVisible(true); //設定視窗可見
}
