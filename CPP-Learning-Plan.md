# C++ 学习路线图（每天1小时，适合Lua背景）

> 按顺序做，不要跳。每阶段完成后才进入下一阶段。

---

## 阶段一：C++ 基础语法（第1-4周）

### 第1周：环境 +  Hello World + 变量

**目标：** 跑通第一个程序，理解基本概念

**1.1 安装编译器**
- 下载 MinGW-w64：https://www.mingw-w64.org/ 或直接搜 MinGW-w64 installer
- 安装时选 x86_64架构，路径不要有中文
- 配置环境变量：将 `mingw64/bin` 加入 PATH
- 打开 PowerShell，输入 `g++ --version`，有版本号即成功

**1.2 写第一个程序**
```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Hello, World!" << endl;
    return 0;
}
```
保存为 `main.cpp`，命令行执行：
```
g++ main.cpp -o main.exe
.\main.exe
```

**1.3 变量和数据类型**
```cpp
int age = 28;           // 整数
float height = 172.5;   // 单精度浮点
double score = 99.8;    // 双精度浮点
char grade = 'A';        // 字符
bool isStudent = false;  // 布尔

cout << "年龄:" << age << endl;
cout << "是否学生:" << isStudent << endl;
```

**练习1：**
声明变量存储你的名字、年龄、身高，输出格式：
```
姓名: 张三
年龄: 28
身高: 172.5cm
```

**1.4 输入输出**
```cpp
int a, b;
cout << "输入两个数:";
cin >> a >> b;
cout << "和:" << a + b << endl;
```

**练习2：**
写一个计算器，输入两个数，输出加减乘除结果（除法保留两位小数）。

---

### 第2周：条件判断 + 循环

**2.1 if / else**
```cpp
int score = 85;
if (score >= 90) {
    cout << "优秀" << endl;
} else if (score >= 60) {
    cout << "及格" << endl;
} else {
    cout << "不及格" << endl;
}
```

**练习3：**
输入成绩，输出对应等级（A/B/C/D/E）。

**2.2 switch**
```cpp
int day = 3;
switch(day) {
    case 1: cout << "周一"; break;
    case 2: cout << "周二"; break;
    case 3: cout << "周三"; break;
    default: cout << "其他";
}
```

**2.3 for 循环**
```cpp
// 打印1到10
for (int i = 1; i <= 10; i++) {
    cout << i << " ";
}
```

**练习4：**
用 for 循环打印 1-100 的所有偶数。

**2.4 while 循环**
```cpp
int i = 1;
while (i <= 10) {
    cout << i << " ";
    i++;
}
```

**练习5：**
用 while 循环计算 1+2+3+...+100 的和。

**2.5 break / continue**
```cpp
for (int i = 1; i <= 10; i++) {
    if (i == 5) continue;  // 跳过5
    if (i == 8) break;     // 遇到8停止
    cout << i << " ";
}
// 输出: 1 2 3 4 6 7
```

---

### 第3周：数组 + 函数

**3.1 数组**
```cpp
int arr[5] = {10, 20, 30, 40, 50};
cout << arr[0] << endl;  // 输出10

// 遍历
for (int i = 0; i < 5; i++) {
    cout << arr[i] << " ";
}
```

**练习6：**
输入5个整数，存到数组，输出最大值和最小值。

**3.2 函数基础**
```cpp
int add(int a, int b) {
    return a + b;
}

int main() {
    cout << add(3, 5) << endl;  // 输出8
    return 0;
}
```

**练习7：**
写一个函数 `isPrime(int n)` 判断 n 是否是素数，是返回 true，否返回 false。在 main 里测试 1-100 的素数有多少个。

---

### 第4周：指针 + 字符串

**4.1 指针（重要！与Lua的内存概念相关）**
```cpp
int a = 10;
int* p = &a;        // p存的是a的地址
cout << p << endl;  // 打印地址
cout << *p << endl; // 通过地址取值，输出10

*p = 20;            // 通过指针修改a的值
cout << a << endl; // 输出20
```

**练习8：**
写一个函数 `swap(int* a, int* b)` 交换两个整数的值，体会指针的用法。

**4.2 字符串**
```cpp
#include <string>
string name = "张三";
string s2 = " is ";
string s3 = name + s2 + "student";
cout << s3 << endl;
cout << s3.length() << endl;      // 长度
cout << s3.substr(0, 2) << endl; // 截取
```

**练习9：**
输入一个字符串，统计其中字母、数字、空格分别有多少个。

---

## 阶段二：数据结构（第5-8周）

### 第5周：结构体 + 动态内存

**5.1 结构体**
```cpp
struct GamePlayer {
    string name;
    int level;
    float hp;
};

int main() {
    GamePlayer p1;
    p1.name = "战士";
    p1.level = 10;
    p1.hp = 100.0f;
    cout << p1.name << " 等级 " << p1.level << endl;
    return 0;
}
```

**练习10：**
定义一个技能结构体，包含名称、冷却时间、伤害值。创建3个技能输出信息。

**5.2 new / delete（手动内存管理）**
```cpp
int* p = new int[5];  // 申请内存
p[0] = 10;
p[1] = 20;
delete[] p;           // 释放内存
```

> 这是Lua不会接触到的部分，C++必须掌握。Lua的GC自动回收，C++要手动。

---

### 第6周：标准容器

**6.1 vector（动态数组）**
```cpp
#include <vector>
vector<int> v;
v.push_back(10);
v.push_back(20);
v.push_back(30);

for (int i = 0; i < v.size(); i++) {
    cout << v[i] << " ";
}
```

**练习11：**
用 vector 实现一个动态数组，支持尾插、删除、查找、输出。

**6.2 map（键值对）**
```cpp
#include <map>
map<string, int> player;
player["战士"] = 100;
player["法师"] = 80;

for (auto it = player.begin(); it != player.end(); it++) {
    cout << it->first << ":" << it->second << endl;
}
```

**练习12：**
用 map 存储5个学生的姓名和成绩，查找某个学生的成绩，不存在输出"未找到"。

---

### 第7周：STL算法

**6.3 常用STL函数**
```cpp
#include <algorithm>
vector<int> v = {5, 2, 8, 1, 9};
sort(v.begin(), v.end());              // 排序
int mx = *max_element(v.begin(), v.end());  // 最大值
int mn = *min_element(v.begin(), v.end());   // 最小值
reverse(v.begin(), v.end());           // 反转
```

**练习13：**
生成20个随机整数（1-100），排序后输出，并找出第3大的数。

---

### 第8周：阶段小项目

**项目：简易通讯录**
```
功能：
1. 添加联系人（姓名+电话）
2. 删除联系人
3. 查找联系人
4. 显示所有联系人
5. 退出

用 vector 或 map 存储，循环显示菜单。
```

这是第一个独立完成的项目，不要看答案，自己写。写不出来就回到前面的章节补基础。

---

## 阶段三：进阶 + 计算机基础（第9-16周）

### 第9-10周：面向对象（类和对象）

**类和构造**
```cpp
class Player {
public:
    string name;
    int hp;

    // 构造函数
    Player(string n, int h) {
        name = n;
        hp = h;
    }

    void show() {
        cout << name << " hp:" << hp << endl;
    }
};

int main() {
    Player p1("战士", 100);
    Player p2("法师", 80);
    p1.show();
    p2.show();
    return 0;
}
```

**练习14：**
创建一个装备类，属性包括名称、品质（白/绿/蓝/紫/橙）、等级。实现显示装备信息的方法。

**继承和多态（了解概念即可）**
```cpp
class Character {
protected:
    string name;
    int hp;
public:
    virtual void attack() {
        cout << name << " 普通攻击" << endl;
    }
};

class Mage : public Character {
public:
    void attack() override {
        cout << name << " 释放火球术" << endl;
    }
};
```

---

### 第11-12周：文件操作 + 错误处理

**文件读写**
```cpp
#include <fstream>

// 写入
ofstream out("save.txt");
out << "战士 100 50" << endl;
out.close();

// 读取
ifstream in("save.txt");
string name;
int hp, mp;
in >> name >> hp >> mp;
in.close();
```

**练习15：**
实现一个存档系统，把玩家数据（姓名、等级、金币）写入文件，读取后显示。

---

### 第13-14周：网络编程（与Lua脚本的TCP经验结合）

**socket编程基础（Windows）**
```cpp
#include <winsock2.h>
#pragma comment(lib, "ws2_32.lib")

int main() {
    WSADATA wsa;
    WSAStartup(MAKEWORD(2, 2), &wsa);

    SOCKET clientSocket = socket(AF_INET, SOCK_STREAM, 0);
    sockaddr_in serverAddr;
    serverAddr.sin_family = AF_INET;
    serverAddr.sin_port = htons(8888);
    serverAddr.sin_addr.s_addr = inet_addr("127.0.0.1");

    connect(clientSocket, (sockaddr*)&serverAddr, sizeof(serverAddr));
    cout << "连接成功" << endl;

    closesocket(clientSocket);
    WSACleanup();
    return 0;
}
```

**练习16：**
实现一个TCP客户端，连接本机8888端口，发送"Hello Server"，接收并打印服务器响应。

---

### 第15-16周：数据结构与算法（结合你的算法基础）

**你已经学过算法，这里用C++实现一遍：**
- 练习17：用C++实现快速排序
- 练习18：用C++实现二分搜索
- 练习19：用C++实现链表（插入、删除、遍历）
- 练习20：用C++实现一个简单的栈

---

## 阶段四：项目阶段（第17-24周）

### 项目一：基于Lua热更新的游戏服务器框架（结合你的经验）
```
用C++实现一个简单的游戏服务器：
- TCP监听客户端连接
- 解析协议（参考你写传奇脚本的经验）
- 管理玩家对象（用vector/map）
- 处理登录、退出、聊天消息
- 与Lua脚本层结合（可选）
```

### 项目二：回合制战斗系统
```
用C++实现一个回合制战斗：
- 英雄属性：生命、攻击、防御
- 技能系统：普通攻击、特殊技能
- 战斗流程：回合循环、伤害计算、胜负判定
- 存档功能：战斗结果写入文件
```

---

## 每日执行模板

```
每日前置任务（10分钟）：
- 复习前一天代码
- 理解上一道练习的答案逻辑

每日核心任务（40分钟）：
- 学习新章节内容
- 跟着示例敲代码（不要复制粘贴！手动敲）
- 完成当日练习

每日收尾（10分钟）：
- 运行成功当天代码，截图保存
- 在 GitHub 创建文件夹，当天代码传上去
```

## GitHub 管理方法

```
你的仓库：cpp-learning
结构：
cpp-learning/
  week01/
    exercise01.cpp
    exercise02.cpp
  week02/
    ...
  project01/
    ...
```

每行代码commit一次，commit信息写：`week01: 练习1-5完成`。

---

## 检查点（每4周一次）

```
第4周末检查：
- 能独立完成练习1-9
- 理解指针的概念（能用手指比划出&和*的区别）
- GitHub上有4周的代码记录

第8周末检查：
- 能独立完成通讯录项目
- 理解 vector/map 的使用场景
- 能说清楚 new/delete 和 Lua GC 的区别

第16周末检查：
- 能实现 TCP 客户端
- 能用 C++ 实现常见算法
- 有两个完整项目在 GitHub

第24周末：
- 开始投简历，找 C++ 游戏服务端岗位
```

---

## 遇到问题怎么办

1. **语法不懂**：回到《C++ Primer》对应章节重新看
2. **编译报错**：把错误信息复制到搜索引擎（百度/CSDN），95%的问题别人都遇到过
3. **逻辑卡住**：先放下，睡一觉再想，或者让 AI 工具帮你解释思路（不是帮你写）

---

这个计划按顺序执行，不需要任何外部链接。
