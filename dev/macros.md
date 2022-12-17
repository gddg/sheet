
# 宏问题

<https://gcc.gnu.org/onlinedocs/cpp/Variadic-Macros.html>


# Variadic Macros

```cpp

c风格
#define eprintf(...) fprintf (stderr, __VA_ARGS__)

cpp风格

#define eprintf(args...) fprintf(stderr, args)
不可以__VA_ARGS__一起用.


#define eprintf(format, ...) fprintf (stderr, format, __VA_ARGS__)
这个公式看起来更具描述性，但从历史上看它不太灵活,必须有format.
如果将变量参数留空，则会出现语法错误，因为格式字符串后会有一个额外的逗号。

eprintf("成功！\n", ); 
→ fprintf(stderr, "成功！\n", ); // error C20一下出错 , 

C++20可以..


```

## 历史 GNU CPP '##'
'##' 标记粘贴运算符放在逗号和变量参数之间时具有特殊含义.

> #define eprintf(格式, ...) fprintf (标准错误, 格式, ## __VA_ARGS__)

前面的标记也不会 发生##' 不是逗号。

### C++20 __VA_OPT__

```c
#define eprintf(format, ...) \
  fprintf (stderr, format __VA_OPT__(,) __VA_ARGS__) 
```

唯一的宏参数是可变参数参数的情况是模棱两可的.
C标准建议避免使用 __VA_ARGS__.
C++ 禁止__VA_OPT__在可变参数宏的替换列表之外的任何地方。


最后

```c
#define DEBUG_MSG(fmt,...) g_log_file.WriteLogEx( LOG_LEVEL_DEBUG, "(File:%s Line:%d)" fmt, __FILE__, __LINE__, ##__VA_ARGS__)

```



# do---while() ?

