# 第2周：条件判断和循环——程序的两条岔路

---

## 从一个游戏场景开始

你写过传奇脚本，应该写过这样的逻辑：

```lua
-- Lua 版本
if playerLevel >= 10 then
    -- 玩家达到10级，可以转职
    enableTransfer(playerId)
else
    -- 等级不够，提示
    sendMessage(playerId, "等级不足，需要10级")
end
```

这个逻辑在 C++ 里几乎一模一样，只是语法略有不同：

```cpp
// C++ 版本
if (playerLevel >= 10) {
    // 玩家达到10级，可以转职
    enableTransfer(playerId);
} else {
    // 等级不够，提示
    sendMessage(playerId, "等级不足，需要10级");
}
```

**区别只有两个：**
1. C++ 要给条件加括号 `( )`
2. C++ 的代码块要用 `{ }` 包裹，Lua 用 `then ... end`

---

## 条件判断：if / else

### 最简单的 if

```cpp
int hp = 50;

if (hp < 30) {
    cout << "危险！血量过低" << endl;
}
```

**执行原理：**

```
电脑看到 if (hp < 30)
    ↓
计算 hp < 30 的结果 → false（50 不小于 30）
    ↓
结果为 false，跳过整个 if 代码块
    ↓
继续执行后面的代码
```

**等价的 Lua 写法：**
```lua
local hp = 50
if hp < 30 then
    print("危险！血量过低")
end
```

### if + else：二选一

```cpp
int hp = 50;

if (hp < 30) {
    cout << "危险！血量过低" << endl;
} else {
    cout << "状态正常" << endl;
}
```

**流程图：**
```
    hp < 30 ?
   ↙         ↘
  true        false
   ↓           ↓
打印"危险"   打印"正常"
```

### if + else if + else：多选一

```cpp
int score = 85;

if (score >= 90) {
    cout << "评级: S" << endl;
} else if (score >= 80) {
    cout << "评级: A" << endl;
} else if (score >= 60) {
    cout << "评级: B" << endl;
} else {
    cout << "评级: C" << endl;
}
```

**注意：C++ 的 else if 是分开的两个词 `else if`，Lua 里是 `elseif`（一个词）**

### 条件判断的坑：赋值而非比较

**Lua 的坑：**
```lua
if x = 10 then  -- Lua 里 = 是赋值，这个 if 永远为 true
    print("x是10")
end
```

**C++ 的坑：**
```cpp
if (x = 10) {  // 危险！= 是赋值，= 10 把10赋给x，条件永远为true
    cout << "x是10";  // 永远会执行
}
```

```cpp
if (x == 10) {  // 正确：== 才是比较
    cout << "x是10";
}
```

**记忆口诀：**
```
=  是"赋值"（把右边的值放进左边的盒子）
== 是"比较"（问左右两边是不是相等）
```

### 练习1：成绩评级

**题目：** 输入一个成绩（0-100），输出对应评级
- 90-100：A
- 80-89：B
- 60-79：C
- 60以下：D

**参考代码：**
```cpp
#include <iostream>
using namespace std;

int main() {
    int score;
    cout << "输入成绩（0-100）: ";
    cin >> score;

    if (score >= 90) {
        cout << "评级: A" << endl;
    } else if (score >= 80) {
        cout << "评级: B" << endl;
    } else if (score >= 60) {
        cout << "评级: C" << endl;
    } else {
        cout << "评级: D" << endl;
    }

    return 0;
}
```

---

## 循环：让代码重复执行

Lua 和 C++ 都有循环，语法几乎一样。

### for 循环：知道次数的循环

**Lua 的 for：**
```lua
for i = 1, 10, 1 do
    print(i)
end
```

**C++ 的 for：**
```cpp
for (int i = 1; i <= 10; i++) {
    cout << i << " ";
}
```

**逐段解释：**
```cpp
for (                        // for 循环开始
    int i = 1;              // 第1段：初始化（循环开始前执行一次）
    i <= 10;                // 第2段：条件判断（每次循环前检查）
    i++                     // 第3段：步进（每次循环后执行）
) {
    cout << i << " ";       // 循环体：要重复执行的代码
}
```

**i++ 是什么意思？**
```
i++  等价于  i = i + 1  等价于  i += 1
    ↓
先使用 i 的值，然后再加1
```

**执行流程：**
```
i = 1 → 检查 i <= 10 → true → 打印 1 → i++ → i = 2
       → 检查 i <= 10 → true → 打印 2 → i++ → i = 3
       → ...（继续直到 i = 11）
       → 检查 i <= 10 → false → 退出循环
```

### 练习2：打印 1-100 的偶数

**题目：** 用 for 循环打印 1-100 的所有偶数

**思路1：逐个判断**
```cpp
for (int i = 1; i <= 100; i++) {
    if (i % 2 == 0) {  // % 是取模（求余数）
        cout << i << " ";
    }
}
```

**思路2：直接跳着走（更高效）**
```cpp
for (int i = 2; i <= 100; i += 2) {
    cout << i << " ";
}
```

**Lua 版本（对比）：**
```lua
for i = 2, 100, 2 do
    print(i)
end
```

### while 循环：不知道次数，只知道条件

**场景：** 玩家不退出就一直等待，这个循环次数不固定

```lua
-- Lua 版本
while true do
    local cmd = waitCommand()
    if cmd == "quit" then
        break
    end
end
```

```cpp
// C++ 版本
while (true) {
    string cmd = waitCommand();
    if (cmd == "quit") {
        break;
    }
}
```

### 练习3：计算 1+2+3+...+100

**题目：** 用 while 循环计算 1 到 100 的和

```cpp
#include <iostream>
using namespace std;

int main() {
    int sum = 0;    // 累加器，初始为0
    int i = 1;      // 计数器

    while (i <= 100) {
        sum = sum + i;  // 把 i 加到 sum 里
        i++;            // i 增加1
    }

    cout << "1+2+...+100 = " << sum << endl;
    return 0;
}
```

**执行过程（简化版）：**
```
i=1:  sum=0+1=1,   i=2
i=2:  sum=1+2=3,   i=3
i=3:  sum=3+3=6,   i=4
...（继续直到 i=101 退出循环）
结果: sum = 5050
```

### do...while：至少执行一次

**和 while 的区别：**
- `while`：先判断条件，可能一次都不执行
- `do...while`：先执行一次，再判断条件，**至少执行一次**

```cpp
int hp = 50;

while (hp < 30) {  // 条件为 false，循环体一次都不执行
    cout << "治疗中...";
    hp++;
}
// 打印：什么都不输出

// -------- vs --------

do {
    cout << "治疗中...";  // 先执行一次
    hp++;
} while (hp < 30);
// 打印：治疗中...（至少执行一次）
```

**实际用途：** 比如服务器等待客户端连接，至少要检查一次才能知道有没有连接进来。

---

## 循环控制：break 和 continue

| 命令 | 作用 | 类比 |
|------|------|------|
| `break` | 跳出整个循环 | 接到老板电话，立刻停止购物离开 |
| `continue` | 跳过本次循环，继续下一次 | 跳过今天的跑步，明天继续 |

### break 的例子：找到第一个满足条件的数

```cpp
for (int i = 1; i <= 100; i++) {
    if (i * i > 100) {    // i的平方大于100
        cout << "第一个满足条件的数: " << i << endl;
        break;            // 找到就停止，不需要继续找了
    }
}
```

输出：`第一个满足条件的数: 11`（因为 11×11=121 > 100）

### continue 的例子：跳过某些数

```cpp
for (int i = 1; i <= 10; i++) {
    if (i == 5) {
        continue;  // 遇到5就跳过，不打印5
    }
    cout << i << " ";
}
```

输出：`1 2 3 4 6 7 8 9 10`（跳过了5）

---

## 嵌套循环：循环里的循环

**场景：** 打印一个九九乘法表

```cpp
for (int i = 1; i <= 9; i++) {
    for (int j = 1; j <= 9; j++) {
        cout << i << "*" << j << "=" << i*j << "\t";
    }
    cout << endl;  // 每行结束后换行
}
```

**输出：**
```
1*1=1   1*2=2   1*3=3   ... 1*9=9
2*1=2   2*2=4   2*3=6   ... 2*9=18
3*1=3   3*2=6   3*3=9   ... 3*9=27
...
9*1=9   9*2=18  9*3=27  ... 9*9=81
```

**运行原理：**
```
外层 i=1 时，内层 j 从1走到9，完整打印一行
外层 i=2 时，内层 j 从1走到9，完整打印一行
...（共9行）
```

### 练习4：打印直角三角形

```
*
**
***
****
*****
```

```cpp
for (int i = 1; i <= 5; i++) {
    for (int j = 1; j <= i; j++) {
        cout << "*";
    }
    cout << endl;
}
```

---

## switch：多值判断的另一种写法

当判断的是**一个变量的多个离散值**时，switch 比 if/else 更清晰。

```cpp
int day = 3;

switch (day) {
    case 1:
        cout << "周一" << endl;
        break;
    case 2:
        cout << "周二" << endl;
        break;
    case 3:
        cout << "周三" << endl;
        break;
    case 4:
        cout << "周四" << endl;
        break;
    case 5:
        cout << "周五" << endl;
        break;
    default:
        cout << "周末" << endl;
        break;
}
```

**等价于 if/else 的写法：**
```cpp
if (day == 1) cout << "周一" << endl;
else if (day == 2) cout << "周二" << endl;
else if (day == 3) cout << "周三" << endl;
else if (day == 4) cout << "周四" << endl;
else if (day == 5) cout << "周五" << endl;
else cout << "周末" << endl;
```

**switch 的坑：忘了 break**

```cpp
int grade = 2;
switch (grade) {
    case 1:
        cout << "等级1" << endl;   // 会执行
    case 2:
        cout << "等级2" << endl;   // 会执行（没有break！）
    case 3:
        cout << "等级3" << endl;   // 也会执行！
        break;
}
// 输出：等级2 等级3（不是只有"等级2"）
```

**原理：** case 只是"标签"，找到匹配的标签后，会**从那里一直执行下去**直到遇到 break。所以每个 case 后面都要加 `break`。

---

## 阶段练习：菜单选择系统

**这是你用 Lua 写过的典型场景，用 C++ 重写：**

```cpp
#include <iostream>
using namespace std;

int main() {
    int choice;

    while (true) {
        cout << "===== 游戏菜单 =====" << endl;
        cout << "1. 创建角色" << endl;
        cout << "2. 进入副本" << endl;
        cout << "3. 查看背包" << endl;
        cout << "4. 退出游戏" << endl;
        cout << "请选择: ";

        cin >> choice;

        if (choice == 1) {
            cout << "正在创建角色..." << endl;
        } else if (choice == 2) {
            cout << "正在进入副本..." << endl;
        } else if (choice == 3) {
            cout << "背包里有: 药水x3, 金币x1000" << endl;
        } else if (choice == 4) {
            cout << "再见！" << endl;
            break;
        } else {
            cout << "无效选择，请重新输入" << endl;
        }

        cout << endl;  // 空一行，让输出更清晰
    }

    return 0;
}
```

**对比 Lua 版本：**
```lua
while true do
    print("===== 游戏菜单 =====")
    print("1. 创建角色")
    print("2. 进入副本")
    print("3. 查看背包")
    print("4. 退出游戏")
    print("请选择:")
    local choice = io.read()

    if choice == "1" then print("正在创建角色...")
    elseif choice == "2" then print("正在进入副本...")
    elseif choice == "3" then print("背包里有...")
    elseif choice == "4" then print("再见！") break
    else print("无效选择")
    end
end
```

**主要区别：**
- `cin >> choice` 读取输入（Lua 用 `io.read()`）
- C++ 的 `if/else if/else` 在一起写，Lua 用 `elseif`
- 字符串比较：C++ 用 `==`，Lua 也用 `==`

---

## 本周总结

| 概念 | 记住一句话 |
|------|-----------|
| if / else | 二选一，条件写在括号里，用 `{}` 包裹代码块 |
| for 循环 | 知道次数，格式：`for(初始化; 条件; 步进)` |
| while 循环 | 不知道次数，只知道条件 |
| do...while | 至少执行一次的 while |
| break | 跳出整个循环 |
| continue | 跳过本次，继续下一次 |
| switch | 多值判断，比 if/else 更清晰 |
| = vs == | `=` 是赋值，`==` 是比较 |

---

## 下周预告：第3周——数组和函数

下周我们会学：
- 数组：如何存储大量数据（类似 Lua 的 table 数值索引）
- 函数：如何封装和复用代码
- 参数传递：值传递 vs 引用传递（C++ 独有，Lua 里没有）
