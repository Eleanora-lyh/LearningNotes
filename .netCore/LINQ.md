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

=> 读作 goes to，delegate委托实例的声明可以转为lambda表达式

（1）delegate变=>；（2）无返回值，且方法体只有一行，省略 { } （3）有返回值，方法体中只有一行代码，省略 { } 以及return；（4）如果只有一个参数，参数的()可以省略

```C#
namespace ConsoleApp1
{
    delegate void D1(); //1、声明一个返回类型为void，参数为空的委托类型，D1
    public class DelegateTest
    {
        /// <summary>
        /// 【三】测试lambda表达式
        /// </summary>
        public void LambdaFunc()
        {
            Action a1 = delegate () 
            {
                Console.WriteLine("this is an anonymous function without parameters and return value");
            };
            //delegate变=>,省略{}
            Action a11 = () => Console.WriteLine("this is an anonymous function without parameters and return value");
            
            Action<int, string> a2 = (int a, string b) =>//delegate变=>
                Console.WriteLine("this is an anonymous function with int and string parameters and no return value" + a + b);
            Action<int, string> a22 = (a, b) =>//delegate变=>,参数的类型可省略
                Console.WriteLine("this is an anonymous function with int and string parameters and no return value" + a + b);
            
            //delegate变=>,参数的类型可省略{} return
            Func<int, int, string> f1 = (a, b) => (a + b).ToString();
            f1(1,2);
        }
    }
}
```

## 4、委托-》匿名方法-》lambda表达式

```C#
namespace ConsoleApp1
{
    delegate string D2(int i, int j); 
    public class DelegateTest
    {
         public string Func2(int i, int j)
        {
            return (i + j).ToString();
        }
        /// <summary>
        /// 【四】总结
        /// </summary>
        public void Sumary()
        {
            //委托
            D2 f1 = Func2;
            Console.WriteLine(f1(1, 2));

            //匿名函数
            Func<int, int, string> f2 = delegate (int a, int b)
            {
                return (a + b).ToString();
            };
            Console.WriteLine(f2(1, 2));

            //lambda表达式
            Func<int, int, string> f3 = (a, b) => (a + b).ToString();
            Console.WriteLine(f3(1, 2));
        }
    }
}

//new DelegateTest().Sumary();
```

## 5、Linq

### 5.1 手动实现Linq

Where方法会遍历集合中每个元素，对于每个元素都调用lambda表达式，判断是否为true，如果为true则将次元度放到返回的集合中。

```C#
namespace ConsoleApp1
{
    public class _02Linq
    {
        public void LinqSimulation()
        {
            int[] nums = new int[] { 1,5,44,81,4,45};//数组本身是没有Where方法的，使用System.Linq的拓展方法
            //IEnumerable<int> res = nums.Where(x => x > 10);
            //var res = MyWhere1(nums, i => i > 10);
            var res = MyWhere2(nums, i => i > 10);
            foreach (int x in res)
            {
                Console.WriteLine(x);
            }
        }
        /// <summary>
        /// 手动实现where方法
        /// </summary>
        /// <param name="items">待处理的数组</param>
        /// <param name="f">过滤函数</param>
        /// <returns>对数组中每个元素都执行过滤函数，为true则计入结果</returns>
        static IEnumerable<int> MyWhere1(IEnumerable<int> items,Func<int,bool>f)
        {
            var res = new List<int>();
            foreach (int i in items)
            {
                if (f(i))
                {
                    res.Add(i);
                }
            }
            return res;
        }
        /// <summary>
        /// 手动实现where方法2
        /// </summary>
        /// <param name="items">待处理的数组</param>
        /// <param name="f">过滤函数</param>
        /// <returns>对数组中每个元素都执行过滤函数，为true则计入结果</returns>
        static IEnumerable<int> MyWhere2(IEnumerable<int> items, Func<int, bool> f)
        {
            foreach (int i in items)
            {
                if (f(i))
                {
                    Console.WriteLine("Where2 " + i);
                    yield return i; //边处理边输出，效率更高
                }
            }
        }
    }
}
```

### 5.2 Any()、Count()

与JavaScript中的var不同，JavaScript中var是动态类型，可以 ```var i= 5; i=“abc”```，但在C#中不可以。编译后会将var变成相应的类型。匿名类型+var 是var发挥作用的地方

```C#
namespace ConsoleApp1
{
    public class _02Linq
    {
        public void LinqTest()
        {
            List<Employee> list = new List<Employee>();
            list.Add(new Employee { id = 1, Name = "jerry", Age = 28, Gender = true, Salary = 5000 });
            list.Add(new Employee { id = 2, Name = "jim", Age = 33, Gender = true, Salary = 3000 });
            list.Add(new Employee { id = 3, Name = "lily", Age = 35, Gender = false, Salary = 9000 });
            list.Add(new Employee { id = 4, Name = "lucy", Age = 16, Gender = false, Salary = 2000 });
            list.Add(new Employee { id = 5, Name = "kimi", Age = 25, Gender = true, Salary = 1000 });
            list.Add(new Employee { id = 6, Name = "nancy", Age = 35, Gender = false, Salary = 8000 });
            list.Add(new Employee { id = 7, Name = "zack", Age = 35, Gender = true, Salary = 8500 });
            list.Add(new Employee { id = 8, Name = "jack", Age = 33, Gender = true, Salary = 8000 });
            list.Where(x => x.Age > 30);
            Console.WriteLine(list.Count());//集合的条数
            Console.WriteLine(list.Count(e => e.Age > 20 && e.Salary > 8000));//集合内符合条件的条数
            Console.WriteLine(list.Any()); //集合中是否有数据
            Console.WriteLine(list.Any(e => e.Salary < 8000));//集合中是否至少有一条满足条件
            //count和any都能判断集合中是否存在满足条件的数据，但是Any效率高
        }

        public class Employee
        {
            public long id { get; set; }
            public string Name { get; set; }//姓名
            public int Age { get; set; }//年龄
            public bool Gender { get; set; }//性别
            public int Salary { get; set; }//月薪
            public override string ToString()
            {
                return $"id={id},Name={Name},Age={Age},Gender={Gender},Salary={Salary}";
            }
        }

    }
}
```

### 5.3 Single()、First()

Single:有且只有一条满足要求的数据; 若不存在则报错【选择合适的方法，“防御性编程”】

SingleOrDefault :最多只有一条满足要求的数据;若多条都满足则报错，若没有则返回null

First :至少有一条，返回第一条; 若不存在则报错

FirstOrDefault :返回第一条或者默认值;

```C#
Console.WriteLine(list.SingleOrDefault(x => x.Age > 30)); //System.InvalidOperationException:“Sequence contains more than one matching element”
Console.WriteLine(list.FirstOrDefault(x => x.Age > 30)); //id=2,Name=jim,Age=33,Gender=True,Salary=3000
```

### 5.4 OrderBy()、OrderByDescending()

```C#
var res = list.OrderByDescending(x => x.Age).ThenByDescending(x=>x.Salary);
//生成一个随机数并排序
var res2 = list.OrderByDescending(x => Guid.NewGuid());
Random random = new Random();
var res22 = list.OrderByDescending(x => random.Next());
foreach (var r in res2)
{
    Console.WriteLine(r.ToString());
}
```

### 5.5 分页 Skip()、Take()

```C#
var res3 = list.Skip(1).Take(10);
foreach (var r in res3)
{
    Console.WriteLine(r.ToString());
}
```

### 5.6 聚合函数 Max、Min、Average、Sum、Count

```C#
Console.WriteLine(list.Max(x => x.Name)); //zack
Console.WriteLine(list.Where(x => x.Age >= 30).Average(x => x.Salary)); //7300
```

### 5.7 GroupBy()

GroupBy()方法参数是分组条件表达式，返回值为lGrouping<TKey,TSource>类型的泛型lEnumerable，也就是每一组以一个IGrouping对象的形式返回。lGrouping是一个继承自lEnumerable的接口，IGrouping中Key属性表示这一组的分组数据的值。

```C#
//按照年龄分组,并倒序
IEnumerable<IGrouping<int,Employee>> res4 = list.GroupBy(x => x.Age).OrderByDescending(x=>x.Key);
            foreach( var group in res4)
            {
                Console.WriteLine($@"年龄：{group.Key},人数：{group.Count()},最大工资：{group.Max(x => x.Salary)},最大工资：{group.Average(x => x.Salary)}");
                foreach(var g in group)
                {
                    Console.WriteLine(g);
                }
                Console.WriteLine();
            }
```

输出：

```C#
年龄：35,人数：3,最大工资：9000,最大工资：8500
id=3,Name=lily,Age=35,Gender=False,Salary=9000
id=6,Name=nancy,Age=35,Gender=False,Salary=8000
id=7,Name=zack,Age=35,Gender=True,Salary=8500

年龄：33,人数：2,最大工资：8000,最大工资：5500
id=2,Name=jim,Age=33,Gender=True,Salary=3000
id=8,Name=jack,Age=33,Gender=True,Salary=8000

年龄：28,人数：1,最大工资：5000,最大工资：5000
id=1,Name=jerry,Age=28,Gender=True,Salary=5000

年龄：25,人数：1,最大工资：1000,最大工资：1000
id=5,Name=kimi,Age=25,Gender=True,Salary=1000

年龄：16,人数：1,最大工资：2000,最大工资：2000
id=4,Name=lucy,Age=16,Gender=False,Salary=2000
```

### 5.8 投影Select()

```C#
//1、投影结果
var res = list.Select(x => x.Name + "," + x.Age).ToList();
foreach (var r in res) Console.WriteLine(r);
//2、匿名类型，编译器进行类型的推断
var res2 = list.Select(x => new { Name = x.Name ,Age=x.Age }).ToList();
foreach (var r in res2) Console.WriteLine(r);
//3、例子:根据年龄分组，获取每组人数、最高工资、平均工资
var res3 = list.GroupBy(x => x.Age)
    .Select(x => new { Age = x.Key,Num=x.Count(),MaxSalary=x.Max(y=>y.Salary),AvgSalary=x.Average(y=>y.Salary) });
//4、获取ld>2的数据，然后按照Age分组，并且把分组按照Age排序然后取出前3条，最后再投影取得年龄人数、平均工资
var res = list.Where(x => x.id > 2)
    .GroupBy(x => x.Age)
    .OrderBy(x => x.Key)
    .Take(3)
    .Select(x => new { Age = x.Key, Num = x.Count(), Avg = x.Average(y => y.Salary) });
foreach (var r in res) Console.WriteLine(r); 
```

输出

```
jerry,28
jim,33
lily,35
lucy,16
kimi,25
nancy,35
zack,35
jack,33

{ Name = jerry, Age = 28 }
{ Name = jim, Age = 33 }
{ Name = lily, Age = 35 }
{ Name = lucy, Age = 16 }
{ Name = kimi, Age = 25 }
{ Name = nancy, Age = 35 }
{ Name = zack, Age = 35 }
{ Name = jack, Age = 33 }

{ Age = 28, Num = 1, MaxSalary = 5000, AvgSalary = 5000 }
{ Age = 33, Num = 2, MaxSalary = 8000, AvgSalary = 5500 }
{ Age = 35, Num = 3, MaxSalary = 9000, AvgSalary = 8500 }
{ Age = 16, Num = 1, MaxSalary = 2000, AvgSalary = 2000 }
{ Age = 25, Num = 1, MaxSalary = 1000, AvgSalary = 1000 }

{ Age = 16, Num = 1, Avg = 2000 }
{ Age = 25, Num = 1, Avg = 1000 }
{ Age = 33, Num = 1, Avg = 8000 }
```

### 5.9 ToList()、ToArray()

### 5.10 查询语法

之前写的叫做【LINQ方法语法 Method Syntax】，还有一种叫做【查询语法 Query Syntax】。【LINQ方法语法】在编译的过程中会被编译成【查询语法】

```C#
var res2 = from l in list
    where l.Salary > 5000
    select new { l.Age, l.Name, XB = l.Gender ? "男" : "女" };
```

