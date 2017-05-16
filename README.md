
# [ GDB ] 偵錯器
###### tags: `GDB`
## GNU Debuger
免費的偵錯器
**compile** 程式的時候要加上 `-g` 的選項
以下使用hello world 程式作範例


```=
#include <stdio.h>

int main()
{
        printf("Hello World.\n");
        return 0;
}
```

將可在GDB進行偵錯
```
$ g++  -g  hello_world.cpp -o hello_world
        ↑ 加上這個  
```




# 使用GDB方式

---
* 將要偵錯的程式用GDB開啟
  如剛剛所編出來的hello world
```
$ gdb hello_world
```

* 將會進入一下的畫面
```
GNU gdb (Ubuntu 7.7.1-0ubuntu5~14.04.2) 7.7.1
Copyright (C) 2014 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
<http://www.gnu.org/software/gdb/documentation/>.
For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from hello_world...done.
(gdb) 
```
* 使用 **`break`**  指令來設定中斷點
  如使用main這個function做中斷點 也可以使用行數
```
(gdb) break main
Breakpoint 1 at 0x400531: file hello_world.cpp, line 5.
```
* 或 **`b`**
```
(gdb) b main
Breakpoint 1 at 0x400531: file hello_world.cpp, line 5.
```


* 使用 **`run`** 或 **`r`**  指令來開始執行程式
```
(gdb) run
Starting program: /home/ubuntu/C_C++Code/TestGDB/hello_world 

Breakpoint 1, main () at hello_world.cpp:5
5               printf("Hello World.\n");

```
他會停在即將執行的那行 目前是第五行 的 `printf("Hello World.\n");`

* 使用 **`next`** 或 **`n`** 指令來步進執行該行
```
(gdb) n
Hello World.
6               return 0;
```

* 使用 **`print`** 或 **`p`** 指令來顯示目前想要知道數的值

```=
#include <stdio.h>
int a = 0;
int main()
{
        printf("Hello World.\n");
        a++;
        a--;
        ++a;
        --a;
        return 0;
}
```
如現在我們要知道 **`a`** 目前的值
```
5                       printf("Hello World.\n");
(gdb) p a
$1 = 0
(gdb) n
Hello World.
6                                       a++;
(gdb) p a
$2 = 0
(gdb) n  
7                                                       a--;
(gdb) p a
$3 = 1

```

* 使用 **`quit`** 或 **`q`**  指令來跳出gdb
```
(gdb) q
```

### 待續...

---
# 參考資料
[GDB: The GNU Project Debugger 官方網站](http://www.gnu.org/software/gdb/documentation/)
