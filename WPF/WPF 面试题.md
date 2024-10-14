WPF 面试题

https://zhuanlan.zhihu.com/p/669348243







###  3、如何理解WPF体系结构?

答：WPF体系结构由几个关键组件组成，这些组件共同工作以创建和渲染UI：

- PresentationFramework：这是提供WPF应用程序基础的核心程序集。它包括用于UI元素、控件、数据绑定、样式和布局的类。
- XAML：XAML是一种用于以声明方式定义UI元素及其关系的标记语言。它允许开发人员将UI设计与应用程序逻辑分离。
- 可视树：可视树表示WPF应用程序中UI元素的层次结构。每个UI元素由一个可视对象表示，可视树定义了这些对象之间的父子关系。
- 逻辑树：逻辑树表示WPF应用程序中UI元素的逻辑结构。它根据它们的逻辑层次结构（例如窗口包含面板、控件和其他UI元素）定义UI元素之间的关系。
- 依赖属性：依赖属性是WPF中的一个关键概念。它们允许UI元素具有可以设置、获取或绑定到其他属性的属性。依赖属性支持数据绑定、动画和样式等功能。
- 布局系统：WPF提供了一个强大的布局系统，根据属性和可用空间自动排列和调整UI元素的大小。它支持各种布局面板，如StackPanel、Grid和DockPanel，可以嵌套使用以创建复杂的布局。
- 渲染引擎：WPF使用DirectX进行硬件加速渲染，提供平滑的图形和动画效果。渲染引擎将可视树转换为一系列渲染命令，发送到GPU进行显示。
- 输入系统：WPF提供了丰富的输入系统，处理用户交互，如鼠标、键盘、触摸和触控笔输入。它包括事件处理、命令路由和输入手势，用于构建交互式应用程序。

答案有点多。总结一下，它包含PresentationFramework、XAML、可视树、逻辑树、依赖属性、布局系统、渲染引擎和输入系统

###  5、解释什么是依赖属性，它和以前的属性有什么不同?为什么在WPF会使用它?

答：

**依赖属性：**

在WPF中，依赖属性（Dependency Property）是一种特殊类型的属性，用于在UI元素中存储和管理属性值。与传统的属性不同，依赖属性具有更强大的功能和灵活性。它们支持数据绑定、样式、动画、值继承和属性更改通知等特性。

**依赖属性与以前属性的不同之处：**

与以前的属性相比，依赖属性具有以下不同之处：

•值的存储方式：依赖属性的值不是直接存储在对象的字段或属性中，而是由WPF框架负责管理。这使得依赖属性可以支持更多的功能，如数据绑定和样式。

属性元数据：依赖属性具有属性元数据，用于定义属性的行为和特性。属性元数据包括默认值、属性更改回调、验证规则等。这使得开发人员可以更好地控制属性的行为。

•属性系统支持：依赖属性通过WPF的属性系统进行管理和操作。属性系统提供了一套机制，用于处理属性的值、继承、优先级和通知。这使得依赖属性可以在整个应用程序中共享和重用。

•数据绑定支持：依赖属性天生支持数据绑定，可以将属性与数据源进行绑定，实现自动更新和同步。这使得开发人员可以轻松地实现UI元素与数据的交互。

为什么在WPF中使用依赖属性：

•数据绑定和样式：依赖属性天生支持数据绑定和样式，使开发人员可以轻松地实现动态更新和样式化的UI元素。

•值继承和优先级：依赖属性支持值的继承和优先级，使得属性的值可以从父元素传递给子元素，并根据不同的优先级进行覆盖。

•动画和转换：依赖属性可以与动画和值转换器一起使用，实现平滑的动画效果和值的转换。

•属性更改通知：依赖属性提供属性更改通知，使开发人员可以在属性值发生变化时做出相应的响应。

这道题好难啊。

###  6、WPF中什么是样式?

**答：**在WPF中，样式（Style）是一种用于定义和应用一组属性值的机制，以统一和定制UI元素的外观和行为。样式可以应用于单个UI元素或整个应用程序中的多个UI元素，从而实现一致的外观和交互效果。

样式通常使用XAML（可扩展应用程序标记语言）来定义，它可以包含一组属性设置，如背景颜色、字体样式、边框样式等。通过将样式应用于UI元素，可以轻松地更改其外观，而无需在每个元素上重复设置相同的属性。

例如，以下代码定义了一个样式，用于设置button控件的背景色和字体颜色：

```html
<Style TargetType="Button"> 
    <Setter Property="Background" Value="Blue"/> 
    <Setter Property="Foreground" Value="White"/>
</Style>
```

可以将样式应用到控件，使用Style属性。

例如，以下代码将上例中的样式应用到button控件：

```html
<Button Style="{StaticResource MyButtonStyle}"/>
```

当然用C#代码也可以控制。



###  7、阐述WPF中什么是模板？

答：WPF中的模板是一种用于定义控件外观的机制。它可以使用XAML或代码来定义。在XAML中，模板可以定义在`Template`元素中。`Template`元素包含一个`TargetType`属性，用于指定模板适用的控件类型。`Template`元素还包含一个`Content`属性，用于指定模板的内容。

例如，以下代码定义了一个模板，用于设置button控件的外观：

```html
<Template TargetType="Button"> 
    <Setter Property="Background" Value="Blue"/> 
    <Setter Property="Foreground" Value="White"/> 
    <Setter Property="BorderThickness" Value="2"/> 
    <Setter Property="BorderBrush" Value="Black"/> 
    <Content> 
        <TextBlock Text="{Binding Content}"/> 
    </Content>
</Template>
```





将代码应用到button

```
<Button Template="{StaticResource MyButtonTemplate}"/>
```

同样C#也可以配置，这里就不多说了。

**
**

 ###  8、阐述WPF视觉树VS 逻辑树?

答：视觉树是指WPF用户界面在屏幕上呈现的结构。它由一系列的视觉元素组成，例如控件、布局、动画等。视觉树是WPF用户界面的最终表现形式。

逻辑树是指WPF用户界面的逻辑结构。它由一系列的逻辑元素组成，例如控件、数据源、事件等。逻辑树是WPF用户界面的底层结构。

视觉树和逻辑树之间的关系

视觉树和逻辑树是相互关联的。视觉树中的每个元素都有一个对应的逻辑元素。例如，textBlock控件在视觉树中对应TextBlock类，在逻辑树中对应TextBlock对象。





###  9、解释—下WPF中的ResourceDictionary ?

答：WPF中的ResourceDictionary是一种用于存储资源的容器。资源可以是任何类型的值，例如字符串、颜色、图像、样式等。ResourceDictionary可以用于将资源重用到多个位置，从而提高应用程序的可维护性和一致性。

案例：

```
<ResourceDictionary> <ResourceDictionary.Resources><stringx:Key="MyString">欢迎加入DOTNET开发跳槽</string><Colorx:Key="MyColor">red</Color> </ResourceDictionary.Resources></ResourceDictionary>
```

以上代码定义了一个ResourceDictionary，其中包含一个字符串资源和一个颜色资源。



### 10、WPF路由事件的哪三种方式/策略(冒泡 直接 隧道)?

答：直接路由事件（Direct Routed Events）：直接路由事件是在特定元素上引发并处理的事件。当一个元素触发一个直接路由事件时，该事件会沿着元素树向上或向下进行传播，直到找到一个处理该事件的元素。处理直接路由事件的元素可以是触发事件的元素本身，也可以是其父级或子级元素。.

隧道路由事件（Tunneling Routed Events）：隧道路由事件从根元素开始，沿着元素树向下传播，直到触发事件的元素。这种事件传播方式允许在事件到达目标元素之前，对事件进行预处理或拦截。处理隧道路由事件的元素通常是根元素或目标元素的父级元素。.

冒泡路由事件（Bubbling Routed Events）：冒泡路由事件从触发事件的元素开始，沿着元素树向上传播，直到根元素。这种事件传播方式允许在事件到达根元素之前，对事件进行预处理或拦截。处理冒泡路由事件的元素通常是触发事件的元素本身或其父级元素。.

这三种路由事件的传播方式提供了灵活的事件处理机制，使开发人员能够在不同层次的元素上捕获和处理事件，从而实现更加灵活和可扩展的用户界面交互。



### 11、解释Routed Events(路由事件)与Commands(命令)?

答：在 WPF 中，路由事件和命令是两种用于处理用户输入和应用程序行为的常用机制。路由事件是一种事件，可以沿着元素树从一个元素传播到另一个元素。这允许您将事件处理程序附加到元素树中的任何位置，而不仅仅是该元素本身。命令是一种封装了操作的对象。命令可以被路由事件处理程序使用来执行操作。



### 12、C#中的表单界面上，有一个DataGrid控件，如何将SQL数据库里的一个表中的数据显示在这个控件上，请描述一下操作方法及步骤 ？

答：首先，确保已经建立了与SQL数据库的连接。可以使用[http://ADO.NET](https://link.zhihu.com/?target=http%3A//ADO.NET)提供的SQL连接对象（如SqlConnection）来连接到数据库。连接字符串应包含数据库的相关信息，如服务器名称、数据库名称、身份验证方式等。

在XAML文件中，将DataGrid控件添加到表单界面上。可以使用以下代码示例创建一个简单的DataGrid控件：

```
<DataGrid x:Name="myDataGrid" AutoGenerateColumns="True" />
```



这将创建一个名为"myDataGrid"的DataGrid控件，并自动根据数据源生成列。

在C#代码中，编写查询数据库的代码，并将结果绑定到DataGrid控件上。可以使用SQLDataAdapter和DataSet来执行查询并获取结果集。以下是一个简单的示例：



```
using (SqlConnection connection = new SqlConnection(connectionString)){ string query = "SELECT * FROM TableName"; SqlDataAdapter adapter = new SqlDataAdapter(query, connection); DataSet dataSet = new DataSet();adapter.Fill(dataSet,"TableName"); myDataGrid.ItemsSource = dataSet.Tables["TableName"].DefaultView;}
```



在上述代码中，将查询结果填充到DataSet对象中，并将DataSet中的表绑定到DataGrid的ItemsSource属性上。这将使DataGrid显示查询结果中的数据。

运行应用程序，DataGrid控件将显示来自SQL数据库表的数据。

以上代码仅供参考，根据项目的实际情况来调整。



### 13、解释完整的WPF对象层次结构 ？

答：WPF 对象层次结构是 WPF 应用程序的基础。它定义了 WPF 应用程序中的所有对象类型以及它们之间的关系。

WPF 对象层次结构的顶层是 Object 类。所有 WPF 对象都直接或间接继承自 Object 类。

Object 类的下一个子类是 DispatcherObject 类。DispatcherObject 类提供了用于处理和分发消息和事件的功能。

DispatcherObject 类的下一个子类是 DependencyObject 类。DependencyObject 类提供了用于支持依赖属性和样式的功能。

DependencyObject 类的下一个子类是 UIElement 类。UIElement 类是所有可视元素的基类。

UIElement 类的下一个子类是 FrameworkElement 类。FrameworkElement 类是所有框架元素的基类。

FrameworkElement 类的下一个子类是 Control 类。Control 类是所有控件的基类。

以下是 WPF 对象层次结构的简要概述：

```
Object DispatcherObject DependencyObject UIElement FrameworkElement Control
```



### 14、简述WPF会取代DirectX吗 ？

**答：**WPF 不会取代 DirectX。WPF 和 DirectX 是两个不同的技术，它们各有优缺点。

WPF 是一种用于构建用户界面的框架。它提供了强大的功能，用于创建高性能、可扩展的用户界面。但是，WPF 并不擅长处理图形和游戏。DirectX 是一种用于处理图形和游戏的 API。它提供了直接访问硬件的能力，可以实现高性能的图形和游戏。但是，DirectX 的使用比较复杂，不适合构建简单的用户界面。因此，WPF 和 DirectX 可以结合使用，以构建具有高性能图形和用户界面的应用程序。例如，WPF 可以用于构建用户界面，DirectX 可以用于处理图形和游戏。







### 16、简述什么是WPF中的值转换器 ？

答：WPF 中的值转换器 (Value Converter) 是一种用于在数据绑定时在源值和目标值之间进行转换的类。这些转换器可以在绑定数据时改变数据的表示形式，使得数据能够以适合于特定上下文的方式显示。



### 17、简述解释这几个类的作用及关系: Visual, UIElement, FrameworkElement, Control ？

答：在 WPF 中，Visual 类是所有可视元素的基类。UIElement 类是所有可视元素的基类，它添加了布局、大小和位置等功能。FrameworkElement 类是所有框架元素的基类，它添加了资源、命令、模板等功能。Control 类是所有控件的基类，它添加了样式、数据绑定等功能。



###  18、你用过WPF中的触发器吗？触发器有哪几种？

答：触发器可以用于在满足特定条件时自动执行操作。WPF 中的触发器有四种：

- Trigger：最基本的触发器，可以根据依赖属性的值进行触发。
- MultiTrigger：可以根据多个依赖属性的值同时进行触发。
- DataTrigger：可以根据数据绑定的数据进行触发。
- EventTrigger：可以根据事件的发生进行触发。

### 19、在WPF中，什么是DataContext？它的作用是什么？

答：在WPF中，DataContext是一个重要的概念，它表示界面元素的数据上下文。每个WPF控件都有一个DataContext属性，用于绑定数据。通过将数据与界面元素的DataContext绑定，可以实现数据与界面的分离，使界面元素能够自动显示和更新数据的变化。

###  20、WPF中的MVVM模式是什么？它的优势是什么？

答：MVVM（Model-View-ViewModel）是一种在WPF中常用的架构模式。它通过将界面逻辑与业务逻辑分离，使开发者能够更好地组织和测试代码。MVVM模式的优势包括：

可维护性：MVVM模式将界面逻辑、业务逻辑和数据模型分离，使代码更易于维护和修改。

可测试性：MVVM模式使界面逻辑与业务逻辑解耦，使得可以更方便地进行单元测试和自动化测试。

可扩展性：MVVM模式使开发者能够轻松地扩展和修改界面，而不影响其他部分的代码。



###  21、WPF与Windows Forms相比有哪些优势？

答：WPF 和 Windows Forms 都是用于开发 Windows 桌面应用程序的框架。WPF 是比 Windows Forms 更新的框架，它提供了更丰富的图形和用户体验功能。

WPF 与 Windows Forms 相比的优势主要包括：

更丰富的图形功能：WPF 使用 XAML 来描述用户界面，XAML 是一种基于 XML 的语言，它可以用于描述复杂的图形效果。WPF 还提供了各种图形元素和动画效果，可以用于创建丰富而逼真的用户界面。

更灵活的布局：WPF 的布局系统更加灵活，可以用于创建各种布局方式。WPF 还提供了各种布局元素，可以用于实现复杂的布局效果。

更强大的数据绑定：WPF 的数据绑定功能更加强大，可以用于将数据与用户界面元素进行关联。WPF 还提供了各种数据绑定元素，可以用于实现复杂的数据绑定效果。

更高效的性能：WPF 使用 Direct3D 进行图形渲染，可以提供更高效的性能。

https://zhuanlan.zhihu.com/p/462042959

https://www.cnblogs.com/Lennon0925/p/11151132.html

https://blog.csdn.net/weixin_42222865/article/details/106192676

https://blog.csdn.net/Cool2Feel/article/details/117999948

