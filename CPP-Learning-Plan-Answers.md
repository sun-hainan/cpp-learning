# 第1周练习答案

## 练习1
```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string name = "张三";
    int age = 28;
    float height = 172.5f;
    cout << "姓名:" << name << endl;
    cout << "年龄:" << age << endl;
    cout << "身高:" << height << "cm" << endl;
    return 0;
}
```

## 练习2
```cpp
#include <iostream>
using namespace std;

int main() {
    double a, b;
    cout << "输入两个数:";
    cin >> a >> b;
    cout << "加:" << a + b << endl;
    cout << "减:" << a - b << endl;
    cout << "乘:" << a * b << endl;
    cout << "除:" << (b != 0 ? a / b : 0) << endl;
    return 0;
}
```

## 练习3
```cpp
#include <iostream>
using namespace std;

int main() {
    int score;
    cout << "输入成绩:";
    cin >> score;
    if (score >= 90) cout << "A" << endl;
    else if (score >= 80) cout << "B" << endl;
    else if (score >= 70) cout << "C" << endl;
    else if (score >= 60) cout << "D" << endl;
    else cout << "E" << endl;
    return 0;
}
```

## 练习4
```cpp
#include <iostream>
using namespace std;

int main() {
    for (int i = 1; i <= 100; i++) {
        if (i % 2 == 0) cout << i << " ";
    }
    return 0;
}
```

## 练习5
```cpp
#include <iostream>
using namespace std;

int main() {
    int sum = 0;
    int i = 1;
    while (i <= 100) {
        sum += i;
        i++;
    }
    cout << sum << endl;
    return 0;
}
```

## 练习6
```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[5];
    cout << "输入5个整数:";
    for (int i = 0; i < 5; i++) cin >> arr[i];
    int mx = arr[0], mn = arr[0];
    for (int i = 1; i < 5; i++) {
        if (arr[i] > mx) mx = arr[i];
        if (arr[i] < mn) mn = arr[i];
    }
    cout << "最大值:" << mx << " 最小值:" << mn << endl;
    return 0;
}
```

## 练习7
```cpp
#include <iostream>
using namespace std;

bool isPrime(int n) {
    if (n < 2) return false;
    for (int i = 2; i * i <= n; i++) {
        if (n % i == 0) return false;
    }
    return true;
}

int main() {
    int count = 0;
    for (int i = 1; i <= 100; i++) {
        if (isPrime(i)) {
            cout << i << " ";
            count++;
        }
    }
    cout << endl << "共" << count << "个" << endl;
    return 0;
}
```

## 练习8
```cpp
#include <iostream>
using namespace std;

void swap(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int main() {
    int a = 3, b = 5;
    cout << "交换前: a=" << a << " b=" << b << endl;
    swap(&a, &b);
    cout << "交换后: a=" << a << " b=" << b << endl;
    return 0;
}
```

## 练习9
```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string s;
    cout << "输入字符串:";
    getline(cin, s);
    int letters = 0, digits = 0, spaces = 0;
    for (char c : s) {
        if (c == ' ') spaces++;
        else if (c >= '0' && c <= '9') digits++;
        else if ((c >= 'a' && c <= 'z') || (c >= 'A' && c <= 'Z')) letters++;
    }
    cout << "字母:" << letters << " 数字:" << digits << " 空格:" << spaces << endl;
    return 0;
}
```
