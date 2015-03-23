# Introduction #

dex-tool-0.0.9.12 add support to Decrypt Strings in a jar

# Details #

in java we usually use the following code to use constant strings.
```
ldc "hello" // load the string to stack
invoke-virtual Lj/l/String;->toString() //use the string
```
and to prevent from reverse engineering, we encrypt the string and add add a static method to decrypt the string at runtime.
```
ldc "olleh"
invoke-static Ltest/Decrypt;->reverse(Lj/l/String;)Lj/l/String; // decrypt the string
invoke-virtual Lj/l/String;->toString()
```

now if we can figure out which method is the decrypt-method we can call
```
d2j-decrypt-string.sh -mo test.Decrypt -mn reverse path/to/the.jar
```

d2j-decrpyt-string.sh will invoke the decrypt-method by reflection and replace the encrypted string with the original string.

NOTICE: the decrypt-method must be static and takes only one string argument and return string ( signature like `public static String xxx(String a)` ).

## before ##

![http://wiki.dex2jar.googlecode.com/hg/images/decrypt-string-before.png](http://wiki.dex2jar.googlecode.com/hg/images/decrypt-string-before.png)

## after ##

![http://wiki.dex2jar.googlecode.com/hg/images/decrypt-string-after.png](http://wiki.dex2jar.googlecode.com/hg/images/decrypt-string-after.png)