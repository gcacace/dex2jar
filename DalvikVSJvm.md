## Class Level ##
  1. AccessFlags: Dalvik remove `ACC_SUPER`, in a non interface class `ACC_SUPER` should been added.
  1. Signature: Dalvik use a `Ldalvik/annotation/Signature;` annotation to store signature.
  1. MemberClasses: Dalvik use a `Ldalvik/annotation/MemberClasses;` annotation, and `*$1,*$2...*$n` not included.
  1. `Ldalvik/annotation/InnerClass;` TODO
  1. `Ldalvik/annotation/EnclosingClass;` TODO
  1. `Ldalvik/annotation/EnclosingMethod;` TODO

## Field Level ##
  1. Signature: Dalvik use a `Ldalvik/annotation/Signature;` annotation to store signature.

## Method Level ##
  1. Signature: Dalvik use a `Ldalvik/annotation/Signature;` annotation to store signature.
  1. Throws: Dalvik use a `Ldalvik/annotation/Throws;` annotation to declare method throws.

## Code Level ##
  1. Register: Dalvik code is register-based, and put 'this' and parameters to the tail of the register array. e.g. a virtual davlik method which has 2 locals and 2 parameters, the register array is `[local1,local2,this,param1,param2]`, but same method in jvm local array is `[this,param1,param2,local1,local2]`
  1. Instruction: Dalvik use a [3-address code](http://en.wikipedia.org/wiki/Three_address_code) jvm use stack-based bytecode, more `xLoad` instruction should added. e.g. to call a virtual method `ResourceBundle.getString(String)` dalvik use `[invoke-virtual {v2, v3};]`, and jvm use `[aload 2; aload 3; invokevirtual;]`
  1. Zero and Null: Dalvik treat them as same