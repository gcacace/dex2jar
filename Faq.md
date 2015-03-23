# FAQ #

  1. [Is dex2jar a dex decompiler](#Is_dex2jar_a_dex_decompiler.md)
  1. [How to decompile a dex file](#How_to_decompile_a_dex_file.md)
  1. [Got OutOfMemoryError: Java heap space](#Got_OutOfMemoryError_%3A_Java_heap_space.md)
  1. [Want to modify a apk/dex file](#Want_to_modify_a_apk/dex_file.md)
  1. [Want to read dex file using dex2jar](#Want_to_read_dex_file_using_dex2jar.md)
  1. [Build dex2jar from source](#Build_dex2jar_from_source.md)
  1. [java.lang.UnsupportedClassVersionError: Bad version n](#Got_UnsupportedClassVersionError_%3A_Bad_version_n.md)
  1. [How can I get the nightly build of dex2jar](#How_can_I_get_the_nightly_build_of_dex2jar.md)

### Is dex2jar a dex decompiler ###
No, dex2jar is a tool for converting Android's .dex format to Java's .class format. just one binary format to another binary format, not to source.

### How to decompile a dex file ###
See the [User Guide](UserGuide.md)


### Got OutOfMemoryError: Java heap space ###
In version 0.0.7.8 and before, dex2jar use the default memory size of JVM. To translate A dex file that contains very large instruction size will cause the Error.
try to add **-Xms512m -Xmx1024m** to dex2jar.bat or dex2jar.sh
```
java -Xms512m -Xmx1024m -cp "%CLASSPATH%" pxb.android.dex2jar.v3.Main %*
```

### Want to modify a apk/dex file ###
dex2jar currently not support modify a apk/dex file directly, dex2jar is desigened to modify a dex/apk file after it convert to .class file. Here is an Example [how to modify a apk file with dex-tools](ModifyApkWithDexTool.md).
alternatives:[smali/baksmali](http://code.google.com/p/smali/),[asmdex](http://asm.ow2.org/asmdex-index.html),[dexmaker](http://code.google.com/p/dexmaker/), they are excellent tools work with dex/odex directly, you should give it a try.

### Want to read dex file using dex2jar ###
dex2jar use an api similar with [asm](http://asm.ow2.org/),refer to http://code.google.com/p/dex2jar/source/browse/src/main/java/pxb/android/dex2jar/dump/Dump.java?r=cb85fc62c81871c3054493b036094a8aeebd08d4

### Build dex2jar from source ###
See the [How to buid dex2jar from source](BuildFromSource.md)

### Got Bad version n UnsupportedClassVersionError: Bad version n ###
please check the version of jdk, dex2jar require jdk6+

### How can I get the nightly build of dex2jar ###
dex2jar host an CI server on [cloudbees](http://www.cloudbees.com), you can get the nightly here:
https://dex2jar.ci.cloudbees.com/job/dex2jar-0.0.9.x/lastStableBuild/com.googlecode.dex2jar$dex-tools/
