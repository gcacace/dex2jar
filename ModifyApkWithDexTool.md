# Introduction #

Dex2jar have the ability to modify the code of an apk.


  1. It first translate the code from dex to jar.
  1. modify .class files in the jar.
  1. It translate jar back to dex and put into apk
  1. sign the apk, and we done the modification.

for demo, we will modify a apk to let it showing a message when it start.

and you need following components in you PATH.
android-sdk,ant,dex2jar,jdk6


# Details #

## got an apk ##

you need an apk, which you didn't have the source.
Just for demo, we build a simple hello-world apk by running the following command
```
android create project --name test_apk --path test_apk --package a.b --activity Main --target 1
cd test_apk
ant debug
cd bin
```
now we got test\_apk/bin/test\_apk-debug.apk. we can check it by running the apk inside an emulator.

![http://wiki.dex2jar.googlecode.com/hg/images/modifyApkDemo-0.png](http://wiki.dex2jar.googlecode.com/hg/images/modifyApkDemo-0.png)

## work with dex-tools ##

Now we got the apk, and It's time to modify it.

  * Convert the code to a modifiable format.

we can't modify dex or jar(.class) file directly. dex2jar support to assemble/disassemble .class file from/to jasmin file. so we convert the apk to jar and disassemble it.
```
# convert classes.dex in test_apk-debug.apk to test_apk-debug_dex2jar.jar
d2j-dex2jar.sh -f -o test_apk-debug_dex2jar.jar test_apk-debug.apk
# verify jar
d2j-asm-verify.sh test_apk-debug_dex2jar.jar
# convert to jasmin format
d2j-jar2jasmin.sh -f -o test_apk_jasmin test_apk-debug_dex2jar.jar
```

  * edit test\_apk\_jasmin/a/b/Main.j to show a toast

```
.method public onCreate(Landroid/os/Bundle;)V
aload 0
aload 1
invokespecial android/app/Activity/onCreate(Landroid/os/Bundle;)V
aload 0
ldc_w 2130837504
invokevirtual a/b/Main/setContentView(I)V

; Toast.makeText(this.getApplicationContext(), "hi", Toast.LENGTH_LONG).show();
aload 0
invokevirtual android/app/Activity/getApplicationContext()Landroid/content/Context;
ldc "hi"
ldc_w 1
invokestatic android/widget/Toast/makeText(Landroid/content/Context;Ljava/lang/CharSequence;I)Landroid/widget/Toast;
invokevirtual android/widget/Toast/show()V

return
.limit locals 2
.limit stack 3
.end method
```

  * repack apk

```
# build jar
d2j-jasmin2jar.sh -f  -o test_apk_jasmin.jar  test_apk_jasmin/ 
# verify jar
d2j-asm-verify.sh test_apk_jasmin.jar
# convert to dex
d2j-jar2dex.sh  -f -o classes.dex test_apk_jasmin.jar
# make a copy
cp test_apk-debug.apk test_apk-debug-toast.apk
# replace classes.dex in test_apk-debug-toast.apk
zip -r test_apk-debug-toast.apk classes.dex
# sign the apk
d2j-apk-sign.sh -f -o test_apk-debug-toast-signed.apk test_apk-debug-toast.apk
```

  * run the apk

```
# uninstall previously apk
adb uninstall a.b
# install
adb install test_apk-debug-toast-signed.apk
# start main activity
adb shell am start -n a.b/.Main
```

![http://wiki.dex2jar.googlecode.com/hg/images/modifyApkDemo-1.png](http://wiki.dex2jar.googlecode.com/hg/images/modifyApkDemo-1.png)


## NOTICE ##

all the above command is for `*`unix, for windows users, please replace the suffix from .sh to .bat.

and for the zip command, just open the test\_apk-debug-toast.apk with winRAR,winZIP or 7z, then drag the classes.dex into it.