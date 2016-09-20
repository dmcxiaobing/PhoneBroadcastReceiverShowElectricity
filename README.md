# PhoneBroadcastReceiverShowElectricity
Android开发点击查看手机电量的小功能。学习广播的一个小技能小Demo

作者：程序员小冰，GitHub主页：https://github.com/QQ986945193

微博：http://weibo.com/mcxiaobing

首先给大家看一下效果图：

![这里写图片描述](http://img.blog.csdn.net/20160904160522824)

先写一个广播类：

```
package david.qq986945193.com.davidphonebroadcastreceivershowelectricity;

import android.app.AlertDialog;
import android.app.Dialog;
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.DialogInterface;
import android.content.Intent;

/**
 * @author ：程序员小冰
 * @新浪微博 ：http://weibo.com/mcxiaobing
 * @GitHub:https://github.com/QQ986945193
 * @CSDN博客: http://blog.csdn.net/qq_21376985
 * @交流Qq ：986945193
 */
public class BatteryInfoBroadcastReceiver extends BroadcastReceiver {
    @Override
    public void onReceive(Context context, Intent intent) {
        if (Intent.ACTION_BATTERY_CHANGED.equals(intent.getAction())) {

            int level = intent.getIntExtra("level", 0);
            //默认总电量 数值范围
            int scale = intent.getIntExtra("scale", 100);

            Dialog dialog = new AlertDialog.Builder(context).setTitle(
                    "电池电量"
            ).setMessage("电池电量为：" + String.valueOf(level * 100 / scale) + "%").setNegativeButton(
                    "关闭", new DialogInterface.OnClickListener() {

                        @Override
                        public void onClick(DialogInterface dialog, int which) {

                        }
                    }
            ).create();
            dialog.show();
        }
    }
}


```

然后再用一个主类进行动态注册广播调用即可：

```
 /**
         * 动态注册广播
         */
        BatteryInfoBroadcastReceiver receiver = new BatteryInfoBroadcastReceiver();
        IntentFilter filter = new IntentFilter(Intent.ACTION_BATTERY_CHANGED);
        registerReceiver(receiver, filter);
```

如果对您有帮助，欢迎star，fork。。。
