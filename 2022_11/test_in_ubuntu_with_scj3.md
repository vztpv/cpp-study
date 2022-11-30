
sprintf vs sprintf_s vs snprintf vs snprintf_s

https://en.cppreference.com/w/c/io/fprintf  


```c++
char buf[] = "\\uDDDD";
snprintf(buf + 2, 5, "%04X", code);
stream << buf;
```

