# Introduction #

dex-tool-0.0.9.8 add support to DeObfuscate a jar


# Details #

## The Problem ##

for a Obfuscated jar like [this](http://wiki.dex2jar.googlecode.com/hg/resources/a.jar)
```
package a;
public class a
{
  static String a = "Hello";
  static void a() {
    System.out.println(a);
  }
  public static void main(String[] args) {
    a();
  }
}
```
all package,class,field,method names are 'a', which is difficult to read.

## DeObfuscate It ##

run the following command
```
#generate a 'suggest' config for rename
d2j-init-deobf -f -o init.txt a.jar
```
we got a init.txt
```
p a=pa
c a/a=C000_a
m a/a.a()=Ma
m a/a.a=Fa
```
which means
```
#rename package a to pa
p a=pa
#rename class a to C000_a
c a/a=C000_a
#rename method a to Ma
m a/a.a()=Ma
#rename field a to Fa
m a/a.a=Fa
```

modify init.txt to
```
#rename package a to hello
p a=hello
#rename class a to World
c a/a=World
#rename method a to say
m a/a.a()=say
#rename field a to message
m a/a.a=message
```
and run
```
d2j-jar-remap -f -c init.txt -o a-deobf.jar a.jar
```
now we get the comfortable source
```
package hello;

import java.io.PrintStream;

public class World
{
  static String message = "Hello";

  static void say() {
    System.out.println(message);
  }

  public static void main(String[] args) {
    say();
  }
}
```
or run the program with
```
java -cp a-deobf.jar hello.World
```