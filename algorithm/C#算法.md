### 找质数

 在1~10000的整数中，找出同时符合以下条件的数：a.必须是质数。b.该数字各位数字之和为偶数，如数字12345，各位数字之和为1+2+3+4+5=15，不是偶数。

```C#
// See https://aka.ms/new-console-template for more information
using System;
using System.Collections;
using System.Dynamic;

const int N = 1000000;
int n, cnt;

//n = int.Parse(Console.ReadLine());
var res = GetPrimes(10000);
foreach (var r in res)
{
    if(SumIsTwo(r)) Console.Write(r+" ");
}

static List<int> GetPrimes(int n)
{
    var list = new List<int>(); 
    bool[] st = new bool[N];
    int[] primes = new int[N];
    int cnt = 0;
    for (int i = 2; i <= n; i++)
    {
        if (!st[i])
        {
            primes[cnt++] = i;
            list.Add(i);
        }
        for (int j = i * i; j <= n; j += i)
        {
            st[j] = true;
        }
    }
    return list;
}

static bool SumIsTwo(int x)
{
    int sum = 0, i = 1;
    while (x > 0)
    {
        sum += x % 10;
        x /= 10;
    }

    if (sum % 2 == 0) return true;
    else return false;
}
```

### 找出问号代表的数字

一个6位数乘以一个3位数，得到一个结果。但不清楚6位数的两个数字是什么，而且结果中有一位数字也不清楚，请编程找出问号代表的数字，答案可能有多个。

12?56?*123 = 154?4987

```C#
for (int i = 0; i < 10; i++)
{
    for (int j = 0; j < 10; j++)
    {
        for (int k = 0; k < 10; k++)
        {
            if ((120560 + i * 1000 + j) * 123 == 15404987 + k * 10000)
            {
                Console.WriteLine($"12{i}56{j} * 123 = 154{k}4987");
            }
        }
    }
}

```

### 将1-100随机插入

```C#
HashSet<int> list = new HashSet<int>();
Random rand = new Random();
while (list.Count() < 100)
{
    list.Add(rand.Next(1, 101));
}

foreach (var i in list)
{
    Console.Write(i+" ");
}
```

### 不使用第三方变量来交换两个变量的值

```C#
int a = 10,b = 20;
string[] input = Console.ReadLine().Split();
a = int.Parse(input[0]);
b = int.Parse(input[1]);


Console.WriteLine($"交换前{a} {b}");
if (b > a)
{
    a=  b - a;
    b = b - a;
    a = b + a;
}
else
{
    b = a - b;
    a = a - b;
    b = b + a;
}

Console.WriteLine($"交换后{a} {b}");
```

### 判断字符串是否为回文字符串

```C#
var str = Console.ReadLine();
Console.WriteLine(IsPalindrome(str));

bool IsPalindrome(string str)
{
    str = str.Replace(" ", "").ToLower();
    char[] charArray = str.ToCharArray();
    var n = charArray.Length;
    for (int i = 0,j=n-1; i <n/2; i++,j--)
    {
        if (charArray[i] != charArray[j])
        {
            return false;
        }
    }
    return true;
}
```

### 排序

两个数组 a大小为n 和 b 大小为m n>m a的数字无序排列第，b数组为空，取出a数组的最小值放到b数组中第一个位置, 依次类推. 不能改变a数组，不能对之进行排序，也不可以倒到别的数组中

解法：使用st标记元素是否被用过

```C#
int[] a = { -20, 9, 7, 37, 38, 69, 89, -1, 59, 29, 0, -25, 39, 900, 22, 13, 55 };
bool[] st = new bool[a.Length];
int[] b = new int[a.Length];
int bi = 0;
while (bi < a.Length)
{
    int minIndex = FindMinIndex(a, st);
    b[bi++] = a[minIndex];
}
for (int i = 0; i < bi; i++)
{
    Console.Write(b[i] + " ");
}

//找当前可用的最小值的索引下标
int FindMinIndex(int[] a, bool[] st)
{
    int minIndex = -1;
    for (int i = 0; i < a.Length; i++) //找到第一个合法的最小初始值
    {
        if (!st[i])
        {
            minIndex = i; break;
        }
    }
    if (minIndex < 0) //如果最小初始值不存在，则每个数都被用过，填充完成
    {
        return -1;
    }
    else
    {
        for (int i = 0; i < a.Length; i++) //获取最小数的下标
        {
            if (!st[i] && a[i] < a[minIndex])
            {
                minIndex = i;
            }
        }
        st[minIndex] = true;
        return minIndex;
    }
}
```

### 两个线程交替打印0~100的奇偶数

一个共享的计数器变量 `counter` 和一个锁对象 `lockObject`,使用 `Monitor.Pulse` 方法通知另一个线程继续执行，并在当前线程上调用 `Monitor.Wait` 方法来释放锁并等待通知

```C#
int counter = 0;
object lockObject = new object();
Task oddTask = Task.Factory.StartNew(PrintOddNumbers);
Task evenTask = Task.Factory.StartNew(PrintEvenNumbers);

Task.WaitAll(oddTask, evenTask);

void PrintOddNumbers()
{
    while (counter <= 100)
    {
        lock (lockObject)
        {
            if (counter % 2 != 0)
            {
                Console.WriteLine("Odd: " + counter);
                counter++;
                Monitor.Pulse(lockObject);
            }
            else
            {
                Monitor.Wait(lockObject);
            }
        }
    }
}

void PrintEvenNumbers()
{
    while (counter <= 100)
    {
        lock (lockObject)
        {
            if (counter % 2 == 0)
            {
                Console.WriteLine("Even: " + counter);
                counter++;
                Monitor.Pulse(lockObject); //通知一个等待在 lockObject 上的线程可以继续执行
            }
            else
            {
                Monitor.Wait(lockObject);//使当前线程进入等待状态，并释放 lockObject 上的锁
            }
        }
    }
}
```

**需要实现对一个字符串的处理,****首先将该字符串首尾的空格去掉,如果字符串中间还有连续空格的话,仅保留一个空格,即允许字符串中间有多个空格,但连续的空格数不可超过一个.**

```C#
string inputStr=" xx  xx ";

inputStr=Regex.Replace(inputStr.Trim()," *"," ");
```



## 搜索

### DFS

```C#
const int N = 10000000;
int n;
int[] st = new int[N];
int[] path = new int[N];

n = int.Parse(Console.ReadLine());
DFS(0);
void DFS(int u)
{
    if (u == n)
    {
        for (int i = 0; i < n; i++)
            Console.Write($"{path[i]} ");
        Console.WriteLine();
    }
    for (int i = 1; i <= n; i++)
    {
        if (st[i] == 0)
        {
            path[u] = i;
            st[i] = 1;
            DFS(u + 1);
            st[i] = 0;
        }
    }
}
```

