# learing

>Dialog使用起来要更为简单，但是Google则是推荐尽量使用DialogFragment（对于Android 3.0以下的版本，可以结合使用support包中提供的DialogFragment以及FragmentActivity）。今天试着用这两种方式来创建对话框，发现DialogFragment果然有一个非常好的特性（在手机配置变化，导致Activity需要重新创建时，例如旋屏，基于DialogFragment的对话框将会由FragmentManager自动重建，然而基于Dialog实现的对话框则没有这样的能力）。

###*dialog*
```
public class MainActivity extends Activity {
    private Button clk;
    private Dialog dialog;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
         
        clk = (Button) findViewById(R.id.clk);
        dialog = new Dialog(this);
        dialog.setContentView(R.layout.dialog);
        clk.setOnClickListener(new OnClickListener() {
             
            @Override
            public void onClick(View v) {
                dialog.show();
            }
        });
 
        //用户恢复对话框的状态
        if(savedInstanceState != null && savedInstanceState.getBoolean("dialog_show"))
            clk.performClick();
    }
 
    /**
     * 用于保存对话框的状态以便恢复
     */
    @Override
    protected void onSaveInstanceState(Bundle outState) {
        super.onSaveInstanceState(outState);
        if(dialog != null && dialog.isShowing())
            outState.putBoolean("dialog_show", true);
        else
            outState.putBoolean("dialog_show", false);
    }
 
    /**
     * 在Activity销毁之前，确保对话框以关闭
     */
    @Override
    protected void onDestroy() {
        super.onDestroy();
        if(dialog != null && dialog.isShowing())
            dialog.dismiss();
    }
}
```
###*dialogfragment*
```
MyDialogFragment mdf = new MyDialogFragment();
                FragmentTransaction ft = getSupportFragmentManager().beginTransaction();
                ft.setTransition(FragmentTransaction.TRANSIT_FRAGMENT_FADE);
                mdf.show(ft, "df");
            }
```

```
public class MyDialogFragment extends DialogFragment {
    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
            Bundle savedInstanceState) {
        View v = inflater.inflate(R.layout.dialog, container, false);
        return v;
    }
}
```
###*移除 dialogfragment* 
```
 Fragment prev = getSupportFragmentManager().findFragmentByTag("fragment_dialog");
    if (prev != null) {
        DialogFragment df = (DialogFragment) prev;
        df.dismiss();
    }
```
>过默认对话框有个讨厌的标题，我们怎么去掉呢：可以在onCreateView中调用getDialog().requestWindowFeature(Window.FEATURE_NO_TITLE);即可去掉
