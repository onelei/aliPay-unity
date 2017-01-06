# aliPay-unity
aliPay plugin for unity.

## android function

```

	/**
     * 支付宝支付业务
     *
     */
    public void AliPay(String _orderInfo) {

        final String orderInfo = _orderInfo;

        Runnable payRunnable = new Runnable() {

            @Override
            public void run() {
                PayTask alipay = new PayTask(AliPay.this);
                Map<String, String> result = alipay.payV2(orderInfo, true);
                Log.i("msp", result.toString());

                Message msg = new Message();
                msg.what = SDK_PAY_FLAG;
                msg.obj = result;
                mHandler.sendMessage(msg);
            }
        };

        Thread payThread = new Thread(payRunnable);
        payThread.start();
    }

```

## send message to unity

```
    UnityPlayer.UnitySendMessage("SDKManager","PayCallBack",""+resultStatus);


```

## CSharp

```
   //  aliPay function;
   public void AliPay(string orderInfo)
    {
#if UNITY_ANDROID
        var ja = new AndroidJavaClass ("com.unity3d.player.UnityPlayer");  
		var jo = ja.GetStatic<AndroidJavaObject> ("currentActivity");
		jo.Call ("AliPay",orderInfo);
#endif
    }


    // pay callBack;
    void PayCallBack(string errCode)
    {
         
    }
```
