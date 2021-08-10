1. 开启Android10+ 全面屏手势

	```shell
	adb shell cmd overlay enable com.android.internal.systemui.navbar.gestural
	```

2. 获取当前默认启动器
	```shell
	adb shell cmd shortcut get-default-launcher
	```

3. 设置默认启动器
	```shell
	adb shell cmd package set-home-activity "com.bllocosn/com.bllocosn.MainActivity"
	```
	常见启动器包名
	
	|App Name|packageName/activityName|
	|---|---|
	|Ratio|com.bllocosn/com.bllocosn.MainActivity|
	|Omega|com.saggitt.omega/com.saggitt.omega.OmegaLauncher|
	|OpenLauncher|com.benny.openlauncher/com.benny.openlauncher.activity.HomeActivity|