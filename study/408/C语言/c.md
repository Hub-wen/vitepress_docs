---
lang: zh-CN
title: C语言基础
titleTemplate: 数据结构需要掌握的C语言基础
description: 学好C语言，走遍天下都不怕
aside: left
lastUpdated: true
sidebar: false
footer: false
prev:
  text: '前言'
  link: '/study/index'
next:
  text: '第一篇|绪论'
  link: '/study/408/Data_Structure/绪论'  
---

# 数据结构需要掌握的C语言基础

<!-- * <Badge type="danger" text="重要" />
* <Badge type="warning" text="难点" />
* <Badge type="tip" text="掌握" />
* <Badge type="info" text="理解" />
* <Badge type="danger">重要</Badge>
* <Badge type="warning">难点</Badge>
* <Badge type="tip">掌握</Badge>
* <Badge type="info">理解</Badge> -->
* 数据类型、变量和常用算数运算 <Badge type="tip" text="掌握" />
* if判断语句和常用算术运算 <Badge type="tip" text="掌握" />
* for循环和while循环语句 <Badge type="tip" text="掌握" />
* 组和字符串 <Badge type="tip" text="掌握" />
* 指针和动态分配空间 <Badge type="warning" text="难点" />
* 结构体和typedef的用法 <Badge type="danger" text="重点" />
* 函数、值传递和指针传递 <Badge type="warning" text="难点" />

---

## 1. 数据类型、变量和常用算术运算

### 数据类型及变量定义与输入输出

```c
int a; //a = 25;
float b = 3.14;
char c = 'Y';
bool d = true; //bool d = false;

// 单个变量输入
scanf("%d", &a);
scanf("%d", &d);

//多个变量连续输入
scanf("%f % c", &b, &c);

// 多个变量连续输出
printf("%d %f %c %d", a, b, c, d);
```

### 常用算术运算

```c
int a = 10, b = 6;
printf("%d", a + b);    // 16
printf("%d", a - b);    // 4
printf("%d", a * b);    // 60
printf("%d", a / b);    
// 1（自动向下取整，不是四舍五入。）int a = 3.9; 打印a就是3
printf("%d", a % b);    
// 4 如果想得到小数（双斜线表示代码注释，关键代码尽量加注释便于老师阅卷理解）
printf("%f", a * 1.0 / b); // 1.666667
```

---

## 2. 判断语句与逻辑运算

### if-else 结构

```c
if(条件1){
  xxxx(满足条件1执行的语句)
}  
else if(条件2){
  xxxx(满足条件2执行的语句)
}
....
else{
  xxxx(上面条件都不满足执行的语句)
}
```                        
> 如果整数变量a = 10， 则将自增10。否则，a>=5，则将其自增5后并打印a。如果上述条件都不满足，则自增1。

```c
int a = 10;
if (a == 10) { //括号可省略          
    a += 10;   //缩进两个字符         
} else if (a >= 5) {    
    a += 5;             
    printf("%d", a);   
} else {                
    a += 1;             
}  
```
```c
int a = 5;
if(a)
  printf("a不是0");
else
  printf("a一定为0");

bool b = true;
if(b)
  printf("b是%d", b);
else
  printf("b是%d", b);
```

### 逻辑运算符

- `&&`：与
- `||`：或
- `!`：非

```c
int a = 3, b = 10;
if (a > 5 && b > 5)   // 两个条件都满足
if (a > 5 || b > 5)   // 至少一个满足
if (a != 5 || b > 10) // a!=5或b>10
if (!a)               // a 为 0 时成立
```

---

## 3. 循环语句

### for 循环

```c
for (int i = 0; i < 10; i++) {
    printf("hello %d\n", i);
} //从0到9执行10次
```
#### 补充知识点： i++和++i的区别
```c
int a = 5;
int b = a++; //b=5
int c = ++b; //c=6
int d = c--; //d=6
```
> for循环()里的i++和++i没有区别，怎么写都行 

#### 局部变量和全局变量
```c
int i = 0;
for( ; i < 10; i++);
printf("%d", i);
```

### while 循环

```c
int i = 0;//初始化在外面
while (i < 10) {
    printf("hello %d\n", i);//这里写i++,下面不写也可以
    i++;//++i也没问题
}
```
> for和while循环几乎可以互换使用， for的优势在于初始化和循环变量修改比较直观。但是如果有很多给=个循环变量，for循环就变得很庞大了，while的优势就体现出来了。

```c
for(int i = 0, j = i + 1, k = j * 2; i < 100||j < 50||k < 500; i *= 2, j += 3, k %= 2)

int i = 0, j = i + 1, k = j * 2;
while(i < 100||j < 50||k < 500){
    i *= 2;
    j += 3; 
    k %= 2;
}
```

### 循环控制

- `continue`：跳过本次循环剩余部分
- `break`：跳出整个循环

---

## 4. 数组和字符串

### 数组定义与初始化

```c
int A[5] = {9, 5, 3, 7, 5};
int B[10];          // 未初始化
int C[10] = {0};    // 全0初始化
int D[10] = {1};    // 第一个为1，其余为0
```

### 字符数组（字符串）

```c
char E[10] = {'a', 'p', 'l', 'e'};
```

---

## 5. 指针与动态内存分配

> 💡指针就是地址、指针就是地址、指针就是tmd地址！！！
### 指针基础

```c
int a = 10;
int *p = &a;
printf("%d", *p); // 10
```

### 动态内存分配

```c
int *p = (int*)malloc(sizeof(int));
*p = 10;
free(p);

// 动态数组
int *arr = (int*)malloc(5 * sizeof(int));
free(arr);
```

> ⚠️ 注意：静态分配在栈上，动态分配在堆上，需手动释放。

---

## 6. 结构体与 typedef

### 结构体定义与使用

```c
struct student {
    float score;
    int age;
};

struct student s1;
s1.age = 18;
s1.score = 95.5;
```

### 使用 typedef 简化

```c
typedef struct student {
    float score;
    int age;
} student, *stu;

student s1;
stu p = (stu)malloc(sizeof(student));
p->age = 18;
```

---

## 7. 函数与参数传递

### 值传递 vs 指针传递

```c
// 值传递（不改变实参）
void swap(int a, int b) {
    int temp = a;
    a = b;
    b = temp;
}

// 指针传递（改变实参）
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}
```

### 全局变量与局部变量

- 局部变量：函数内有效
- 全局变量：整个程序有效

---
