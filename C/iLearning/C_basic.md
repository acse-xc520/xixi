[TOC]
# 第二章 变量

## 1 基本数据类型

### 数据类型分类
- 基本类型
  1. 整型
  2. 浮点型
        - 单精度
        - 双精度
  3. 字符型
- 指针类型
- 空类型（void）
- 复合类型
  1. 数组
  2. 结构体
  3. 共用体
  4. 枚举
 
### 基本数据类型的大小
- 32位系统常用ILP32数据模型
- 64位系统，类Unix系统（eg. Linux, MacOSx）采用LP64，而Windows采用LLP64
> ILP：int long pointer
> ILP32：表示在这种数据模型下，int long pointer的大小都是32位，4字节

## 2 逻辑控制语句

## 3 函数声明与实现

## 4 运算符优先级

int a = 3
a += a -= a * a ？

根据优先级
a = a - a * a;
a = 3 - 9 = -6
a = a + a = -12
a = -12

# 第九章 数组和指针

## 9.1 数组和指针的基本形态 

指针用法
```c
char ch = 'c';
char *pch = &ch;    // 指向char地址
char *pStr = "abc"; // 指向字符串起始地址

int m;
int *pm = &m;      // 整数指针

struct Test stTest;
struct Test *pst = &stTest; // 结构体指针

extern void TestFunc(int m);
void (*pf)(int) = TestFunc // 函数指针pf指向同类型函数TestFunc
```

数组用法
```c
char m1[10];
char m2[] = "123"; // 空间是4，包括换行符
char m3[] = {'1', '2'}; // 空间是2
int m4[3][2]; 
int *m5[10] // 长度是10，数组中存放指向整型的指针
```

数组访问
```c
int Test1(){
    char *test = "12345";
    int m = test[1];
    return m;
}
```
获取test[1]的步骤：
1. test表示数组起始地址，先获取地址。
2. test地址加上偏移，获取具体值。

