# FakeIMEI
Fake IMEI for Free Fire
Good news for Android 10, user apps can no longer get IMEI due to privacy changes https://developer.android.com/about/versions/10/privacy/changes

# How to intergate
To intergate it in the APK file, copy the smali folder to the smali directory of decompiled APK
Open file /smali/com/dts/freefireth/FFAPI.smali
Replace this code:
```.method public static getTelephonyManagerIMEI()Ljava/lang/String;
    .locals 4
    .annotation build Landroidx/annotation/RequiresPermission;
        value = "android.permission.READ_PHONE_STATE"
    .end annotation

    sget-object v2, Lcom/dts/freefireth/FFAPI;->MainActivity:Lcom/dts/freefireth/FFMainActivity;

    const-string/jumbo v3, "phone"

    invoke-virtual {v2, v3}, Lcom/dts/freefireth/FFMainActivity;->getSystemService(Ljava/lang/String;)Ljava/lang/Object;

    move-result-object v1

    check-cast v1, Landroid/telephony/TelephonyManager;

    :try_start_0
    sget v2, Landroid/os/Build$VERSION;->SDK_INT:I

    const/16 v3, 0x19

    if-le v2, v3, :cond_0

    invoke-virtual {v1}, Landroid/telephony/TelephonyManager;->getImei()Ljava/lang/String;

    move-result-object v2

    :goto_0
    return-object v2

    :cond_0
    invoke-virtual {v1}, Landroid/telephony/TelephonyManager;->getDeviceId()Ljava/lang/String;
    :try_end_0
    .catch Ljava/lang/SecurityException; {:try_start_0 .. :try_end_0} :catch_0

    move-result-object v2

    goto :goto_0

    :catch_0
    move-exception v0

    const-string/jumbo v2, ""

    goto :goto_0
.end method
```

To this code:
```.method public static getTelephonyManagerIMEI()Ljava/lang/String;
    .locals 6

    sget-object v2, Lcom/dts/freefireth/FFAPI;->MainActivity:Lcom/dts/freefireth/FFMainActivity;

    invoke-static {v2}, Luk/lglteam/FakeIMEI;->GetIMEI(Landroid/content/Context;)Ljava/lang/String;

    move-result-object v1

    return-object v1
.end method
```

Do the same on getTelephonyManagerMEID

