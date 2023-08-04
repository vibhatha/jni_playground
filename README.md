# jni_playground

## Simple Programme

Write a simple HelloWorld class as shown below

```java
class HelloWorld {
    private native void print();
    public static void main(String[] args) {
        new HelloWorld().print();
    }

    static {
        System.loadLibrary("HelloWorld");
    }	
}
```

Note that the `HelloWorld.so` is required to be loaded before calling the native method. 
The native method contains the `native` keyword and no definition, but the declaration. 
The definition is in a native library. 

Steps to compile

1. `javac -h HelloWorld.java`, this would generate the class file and the header `HelloWorld.h`
2. Compile and link

```bash
gcc -shared -I${JAVA_HOME}/include -I${JAVA_HOME}/include/linux HelloWorld.c -o libHelloWorld.so
```

3. Run programme
    Include the shared library for execution include it in `LD_LIBRARY_PATH`

    ```
    export LD_LIBRARY_PATH=$PWD${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
    ```
    and `java HelloWorld` 

    Or, 

    run as `java -Djava.library.path=. HelloWorld`.