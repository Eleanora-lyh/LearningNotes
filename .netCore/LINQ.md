委托——》lambda——》LINQ

统计一个字符串中每个字母出现的频率(忽略大小写)，然后按照从高到低的顺序输出出现频率高于2次的单词和其出现的频率。

```C#
var items=s.Where(c => char.lsLetter(c))//过滤非字母
    .Select(c =>char.ToLower(c))//大写字母转换为小写
    .GroupBy(c =>c)//根据字母进行分组
    .Where(g=>g.Count()>2)//过滤掉出现次数<=2
    .OrderByDescending(g =>g.Count())//按次数排序
    .Select(g=>new { char=g.Key,Count=g.Count()});
```

## 1、委托

1、委托是可以指向方法的类型，调用委托变量时执行的就是变量指向的方法举例。

2、.NET 中定义了泛型委托Action(无返回值)和Func(有返回值)，所以一般不用自定义委托类型。举例。

```C#
namespace ConsoleApp1
{
    delegate void D1(); //1、声明一个返回类型为void，参数为空的委托类型，D1
    public class DelegateTest
    {
        /// <summary>
        /// 【一】测试委托
        /// </summary>
        public void DelegateFunc()
        {
            D1 d1 = Func1; //3.1、声明一个D1委托类型的委托实例对象d1，d1指向Func1
            d1(); //4.1、调用d1()

            // 无返回值Action，有返回值Func
            Action a = Func1;//3.2、声明一个参数和返回类型为Func1的委托实例，a指向Func1
            a();//4.2、调用a()
            Action<int,string> b = Func11;
            b(1,"2"); //this is func11 res=12

            Func<int, int, string> f = Func2;//3.3、声明一个参数为int,int返回类型为string的委托实例对象f，f指向Func1
            Console.WriteLine(f(1, 2));//4.3、调用f()
        }
        public void Func1()//2、声明一个返回类型为void，参数为空的函数，Func1
        {
            Console.WriteLine("this is func1");
        }
        public void Func11(int i, string s)//2、声明一个返回类型为void，参数为空的函数，Func1
        {
            Console.WriteLine("this is func11 res=" + i + s);
        }
        public string Func2(int i, int j)//2、声明一个返回类型为void，参数为空的函数，Func1
        {
            return (i + j).ToString();
        }
    }
}

//new DelegateTest().DelegateFunc();
```

## 2、匿名方法

```C#
namespace ConsoleApp1
{
    delegate void D1(); //1、声明一个返回类型为void，参数为空的委托类型，D1
    public class DelegateTest
    {
        /// <summary>
        /// 【二】测试匿名方法
        /// </summary>
        public void AnonymousFunc()
        {
            Action a1 = delegate () //声明一个无参数无返回值的委托实例
            {
                //形参parameters 实参argument
                Console.WriteLine("this is an anonymous function without parameters and return value");
            };
            a1();

            Action<int, string> a2 = delegate (int a, string b) //声明一个无参数无返回值的委托实例
            {
                //形参parameters 实参argument
                Console.WriteLine("this is an anonymous function with int and string parameters and no return value" + a + b);
            };
            a2(1,"2");
        }
    }
}

//new DelegateTest().AnonymousFunc();
```





## 3、lambda表达式

