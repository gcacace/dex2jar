To get a source file you need to go through the following five steps:
  1. [Source](#Source.md)
  1. [Compile by javac](#Compile_by_javac.md)
  1. [Translate by dx](#Translate_by_dx.md)
  1. [Translate by dex2jar](#Translate_by_dex2jar.md)
  1. [Source decompile by jd-gui](#Source_decompile_by_jd-gui.md)

## Source ##
(.java/editplus)
```
public String getInitParameter(String name) {
        ServletConfig sc = getServletConfig();
        if (sc == null) {
            throw new IllegalStateException(
                lStrings.getString("err.servlet_config_not_initialized"));
        }
        return sc.getInitParameter(name);
    }
```

## Compile by javac ##
(.class/jclasslib)
```
 0 aload_0
 1 invokevirtual #2 <javax/servlet/GenericServlet.getServletConfig>
 4 astore_2
 5 aload_2
 6 ifnonnull 25 (+19)
 9 new #3 <java/lang/IllegalStateException>
12 dup
13 getstatic #4 <javax/servlet/GenericServlet.lStrings>
16 ldc #5 <err.servlet_config_not_initialized>
18 invokevirtual #6 <java/util/ResourceBundle.getString>
21 invokespecial #7 <java/lang/IllegalStateException.<init>>
24 athrow
25 aload_2
26 aload_1
27 invokeinterface #8 <javax/servlet/ServletConfig.getInitParameter> count 2
32 areturn
```

## Translate by dx ##
(.dex/dexdump)
```
022644:                  |[022644] javax.servlet.GenericServlet.getInitParameter:(Ljava/lang/String;)Ljava/lang/String;
022654: 6e10 d703 0400   |0000: invoke-virtual {v4}, Ljavax/servlet/GenericServlet;.getServletConfig:()Ljavax/servlet/ServletConfig; // method@03d7
02265a: 0c00             |0003: move-result-object v0
02265c: 3900 1000        |0004: if-nez v0, 0014 // +0010
022660: 2201 7800        |0006: new-instance v1, Ljava/lang/IllegalStateException; // class@0078
022664: 6202 2f00        |0008: sget-object v2, Ljavax/servlet/GenericServlet;.lStrings:Ljava/util/ResourceBundle; // field@002f
022668: 1a03 2914        |000a: const-string v3, "err.servlet_config_not_initialized" // string@1429
02266c: 6e20 5103 3200   |000c: invoke-virtual {v2, v3}, Ljava/util/ResourceBundle;.getString:(Ljava/lang/String;)Ljava/lang/String; // method@0351
022672: 0c02             |000f: move-result-object v2
022674: 7020 3b01 2100   |0010: invoke-direct {v1, v2}, Ljava/lang/IllegalStateException;.<init>:(Ljava/lang/String;)V // method@013b
02267a: 2701             |0013: throw v1
02267c: 7220 e703 5000   |0014: invoke-interface {v0, v5}, Ljavax/servlet/ServletConfig;.getInitParameter:(Ljava/lang/String;)Ljava/lang/String; // method@03e7
022682: 0c01             |0017: move-result-object v1
022684: 1101             |0018: return-object v1
```

## Translate by dex2jar ##
(.class/jclasslib)
```
 0 aload_0
 1 invokevirtual #49 <javax/servlet/GenericServlet.getServletConfig>
 4 astore_2
 5 aload_2
 6 ifnonnull 27 (+21)
 9 getstatic #37 <javax/servlet/GenericServlet.lStrings>
12 ldc #51 <err.servlet_config_not_initialized>
14 invokevirtual #56 <java/util/ResourceBundle.getString>
17 astore_3
18 new #58 <java/lang/IllegalStateException>
21 dup
22 aload_3
23 invokespecial #61 <java/lang/IllegalStateException.<init>>
26 athrow
27 aload_2
28 aload_1
29 invokeinterface #63 <javax/servlet/ServletConfig.getInitParameter> count 2
34 areturn
```

## Source decompile by jd-gui ##
(.java/jd-gui)
```
public String getInitParameter(String paramString)
  {
    ServletConfig localServletConfig = getServletConfig();
    if (localServletConfig == null)
    {
      String str = lStrings.getString("err.servlet_config_not_initialized");
      throw new IllegalStateException(str);
    }
    return localServletConfig.getInitParameter(paramString);
  }
```