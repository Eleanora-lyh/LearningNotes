## 1、依赖安装

1）安装prism

```bash
NuGet\Install-Package Prism.DryIoc -Version 8.1.97
```

2）删除原来的MainWindow，将MainWindow移到Views文件夹下，MainWindow的页面代码如下：

```xml
<Window x:Class="LoginTest.Views.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:LoginTest.Views"
        xmlns:prism="http://prismlibrary.com/"
        prism:ViewModelLocator.AutoWireViewModel="True"
        mc:Ignorable="d"
        Title="MainWindow" Height="700" Width="1200">
    <Grid>
        <TextBlock Text="这是登录成功后的界面" FontSize="40"></TextBlock>
    </Grid>
</Window>
```

3）引用prism，修改app.xaml

```xml
<prism:PrismApplication x:Class="LoginTest.App" xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
                        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" xmlns:local="clr-namespace:LoginTest"
                        xmlns:materialDesign="http://materialdesigninxaml.net/winfx/xaml/themes" xmlns:prism="http://prismlibrary.com/">
    <Application.Resources>
        <ResourceDictionary>
            <ResourceDictionary.MergedDictionaries>
                <materialDesign:BundledTheme BaseTheme="Dark" PrimaryColor="DeepPurple"
                                             SecondaryColor="Lime" />
                <ResourceDictionary Source="pack://application:,,,/MaterialDesignThemes.Wpf;component/Themes/MaterialDesign3.Defaults.xaml" />
            </ResourceDictionary.MergedDictionaries>
        </ResourceDictionary>
    </Application.Resources>
</prism:PrismApplication>
```

4）修改app.xmal.cs

```c#
using System.Configuration;
using System.Data;
using System.Windows;
using LoginTest.ViewModels;
using LoginTest.Views;
using Prism.DryIoc;
using Prism.Ioc;
using Prism.Services.Dialogs;

namespace LoginTest
{
    /// <summary>
    /// Interaction logic for App.xaml
    /// </summary>
    public partial class App : PrismApplication
    {
        /// <summary>
        /// 注册服务
        /// </summary>
        /// <param name="containerRegistry"></param>
        protected override void RegisterTypes(IContainerRegistry containerRegistry)
        {
           
            
        }
        /// <summary>
        /// 设置启动窗口
        /// </summary>
        /// <returns></returns>
        protected override Window CreateShell()
        {
            return Container.Resolve<MainWindow>();
        }
    }
}
```

5）下载MaterialDesignThemes组件

```bash
NuGet\Install-Package MaterialDesignThemes -Version 5.0.1-ci633
```

使用说明：

https://github.com/MaterialDesignInXAML/MaterialDesignInXamlToolkit/wiki/Getting-Started

MaterialDesignThemes是一个针对WPF应用程序的开源UI框架，它提供了一套现代化的、基于Google Material Design风格的控件和样式。提供了丰富的控件和样式，包括按钮、文本框、下拉框、卡片、对话框等。这些控件都遵循Material Design的设计原则，具有醒目的颜色、扁平化的外观和动感的交互效果。

除了控件和样式，MaterialDesignThemes还提供了一些附加功能，如主题管理、阴影效果、图标集等。它还包含了一些实用的工具和扩展，帮助开发人员更轻松地使用和定制Material Design风格的界面。

使用MaterialDesignThemes框架，开发人员可以快速构建具有现代化外观和动态效果的WPF应用程序。通过简单的XAML标记，开发人员可以应用预定义的样式和主题，或者根据自己的需求进行自定义。

6）在app.xaml中引用组件，使用其中的资源

```xml
<prism:PrismApplication x:Class="LoginTest.App" xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
                        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" xmlns:local="clr-namespace:LoginTest"
                        xmlns:materialDesign="http://materialdesigninxaml.net/winfx/xaml/themes" xmlns:prism="http://prismlibrary.com/">
    <Application.Resources>
        <ResourceDictionary>
            <ResourceDictionary.MergedDictionaries>
                <materialDesign:BundledTheme BaseTheme="Dark" PrimaryColor="DeepPurple"
                                             SecondaryColor="Lime" />
                <ResourceDictionary Source="pack://application:,,,/MaterialDesignThemes.Wpf;component/Themes/MaterialDesign3.Defaults.xaml" />
            </ResourceDictionary.MergedDictionaries>
        </ResourceDictionary>
    </Application.Resources>
</prism:PrismApplication>
```

7）设置主窗口的字体

这些将确保窗口使用 Material Design 颜色，与 Toolkit 的样式和组件很好地融合在一起。但是，为了获得完整的 Material Design 体验，您应该按如下方式设置字体：

```xml
<Window [...]
        xmlns:materialDesign="http://materialdesigninxaml.net/winfx/xaml/themes"
        TextElement.Foreground="{DynamicResource MaterialDesign.Brush.Foreground}"
        Background="{DynamicResource MaterialDesign.Brush.Background}"
        TextElement.FontWeight="Medium"
        TextElement.FontSize="14"
        FontFamily="{materialDesign:MaterialDesignFont}"
        [...] >
```

如果想拉取源码并运行Demo样例，则需要按照下面的说明配置具体的环境

https://github.com/MaterialDesignInXAML/MaterialDesignInXamlToolkit/wiki/Compiling-From-Source



## 2、设计登录后主窗体的导航栏

```xml
<Window x:Class="MyTodo.MainWindow" xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml" xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:local="clr-namespace:MyTodo" xmlns:materialDesign="http://materialdesigninxaml.net/winfx/xaml/themes"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" xmlns:wpf="http://materialdesigninxaml.net/winfx/xaml/themes"
        Title="MainWindow" Width="1280"
        Height="768" AllowsTransparency="True"
        Background="{DynamicResource MaterialDesign.Brush.Background}"
        FontFamily="{wpf:MaterialDesignFont}"
        TextElement.FontSize="14" TextElement.FontWeight="Medium"
        TextElement.Foreground="{DynamicResource MaterialDesign.Brush.Foreground}"
        WindowStartupLocation="CenterScreen" WindowStyle="None"
        mc:Ignorable="d">
    <materialDesign:DialogHost DialogTheme="Inherit" Identifier="RootDialog"
                               SnackbarMessageQueue="{Binding ElementName=MainSnackbar, Path=MessageQueue}">

        <materialDesign:DrawerHost IsLeftDrawerOpen="{Binding ElementName=MenuToggleButton, Path=IsChecked}">
            <!--  左侧的抽屉  -->
            <materialDesign:DrawerHost.LeftDrawerContent>
                <DockPanel MinWidth="220" />
            </materialDesign:DrawerHost.LeftDrawerContent>

            <DockPanel>
                <materialDesign:ColorZone x:Name="ColorZone" Padding="16"
                                          materialDesign:ElevationAssist.Elevation="Dp4" DockPanel.Dock="Top"
                                          Mode="PrimaryMid">
                    <!--  左侧功能按钮  -->
                    <DockPanel LastChildFill="False">
                        <StackPanel Orientation="Horizontal">
                            <!--  菜单  -->
                            <ToggleButton x:Name="MenuToggleButton" AutomationProperties.Name="HamburgerToggleButton"
                                          IsChecked="False"
                                          Style="{StaticResource MaterialDesignHamburgerToggleButton}" />
                            <!--  回退  -->
                            <Button Margin="24,0,0,0"
                                    materialDesign:RippleAssist.Feedback="{Binding RelativeSource={RelativeSource Self}, Path=Foreground, Converter={StaticResource BrushRoundConverter}}"
                                    Command="{Binding MovePrevCommand}"
                                    Content="{materialDesign:PackIcon Kind=ArrowLeft,
                                                                      Size=24}"
                                    Foreground="{Binding RelativeSource={RelativeSource AncestorType={x:Type FrameworkElement}}, Path=(TextElement.Foreground)}"
                                    Style="{StaticResource MaterialDesignToolButton}"
                                    ToolTip="Previous Item" />
                            <!--  前进  -->
                            <Button Margin="16,0,0,0"
                                    materialDesign:RippleAssist.Feedback="{Binding RelativeSource={RelativeSource Self}, Path=Foreground, Converter={StaticResource BrushRoundConverter}}"
                                    Command="{Binding MoveNextCommand}"
                                    Content="{materialDesign:PackIcon Kind=ArrowRight,
                                                                      Size=24}"
                                    Foreground="{Binding RelativeSource={RelativeSource AncestorType={x:Type FrameworkElement}}, Path=(TextElement.Foreground)}"
                                    Style="{StaticResource MaterialDesignToolButton}"
                                    ToolTip="Next Item" />
                            <!--  标题  -->
                            <TextBlock Margin="16,0" HorizontalAlignment="Center"
                                       VerticalAlignment="Center" AutomationProperties.Name="Material Design In XAML Toolkit"
                                       FontSize="22" Text="笔记本" />
                        </StackPanel>
                        <!--  右侧功能按钮  -->
                        <StackPanel DockPanel.Dock="Right" Orientation="Horizontal">
                            <!--  头像  -->
                            <Image Width="25" Height="25"
                                   Source="/Images/Husky.jpg">
                                <!--  图片将只显示在椭圆形状的区域内，其余部分将被剪裁掉  -->
                                <Image.Clip>
                                    <!--使用<Image.Clip>属性来定义剪裁区域-->
                                    <EllipseGeometry Center="12.5,12.5" RadiusX="12.5"
                                                     RadiusY="12.5" />
                                </Image.Clip>
                            </Image>
                            <Button x:Name="btnMin" Content="—"
                                    Style="{StaticResource MaterialDesignFlatMidBgButton}" />
                            <Button x:Name="btnMax" Content="☐"
                                    Style="{StaticResource MaterialDesignFlatMidBgButton}" />
                            <Button x:Name="btnClose" Content="✕"
                                    Style="{StaticResource MaterialDesignFlatMidBgButton}" />
                        </StackPanel>
                    </DockPanel>
                </materialDesign:ColorZone>

            </DockPanel>
        </materialDesign:DrawerHost>
    </materialDesign:DialogHost>
</Window>

```

1）设置主窗口的样式

这些属性设置了窗口的标题、宽度、高度、是否允许透明度、启动位置和窗口样式。

- `Title` 设置窗口的标题为 "MainWindow"。
- `Width` 和 `Height` 分别设置窗口的宽度和高度为 1280 和 768 像素。
- `AllowsTransparency` 设置窗口是否允许透明度，为 `True` 表示允许透明度。
- `WindowStartupLocation` 设置窗口启动位置为屏幕中央。
- `WindowStyle` 设置窗口样式为无边框。

```xml
<Window [...]
        xmlns:wpf="http://materialdesigninxaml.net/winfx/xaml/themes"
        Title="MainWindow" Width="1280"
        Height="768" AllowsTransparency="True"
        WindowStartupLocation="CenterScreen" WindowStyle="None"
        [...] >
```

![image-20240519154504249](../TyporaImgs/image-20240519154504249.png)

由于右侧的 缩小、放大、关闭按钮没有绑定ViewModel的需求，所以直接设计三个click事件进行处理，在MainView.xaml.cs中

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Shapes;

namespace MyTodo.Views
{
    /// <summary>
    /// MainView.xaml 的交互逻辑
    /// </summary>
    public partial class MainView : Window
    {
        public MainView()
        {
            InitializeComponent();
            btnMin.Click += (s, e) =>
            {
                this.WindowState = WindowState.Minimized;
            };
            btnMax.Click += (s, e) =>
            {
                if (this.WindowState == WindowState.Maximized)
                    this.WindowState = WindowState.Normal;
                else
                    this.WindowState = WindowState.Maximized;

            };
            btnClose.Click += (s, e) =>
            {
                this.Close();
            };
            ColorZone.MouseMove += (s, e) =>
            {
                if (e.LeftButton == MouseButtonState.Pressed)
                {
                    this.DragMove();
                }
            };
            ColorZone.MouseDoubleClick += (s, e) =>
            {
                if (this.WindowState == WindowState.Maximized)
                    this.WindowState = WindowState.Normal;
                else
                    this.WindowState = WindowState.Maximized;
            }; ;
        }
        
    }
}
```

## 3、设置左侧菜单的弹出

将MainWindow删除，在Views文件夹下新建MainView，将代码迁移过去

在主页面中设计左侧抽屉的样式

```xml
 <!--  左侧的抽屉  -->
            <materialDesign:DrawerHost.LeftDrawerContent>
                <DockPanel MinWidth="220" />
            </materialDesign:DrawerHost.LeftDrawerContent>
```

```xml
    <!--  左侧的抽屉  -->
<materialDesign:DrawerHost.LeftDrawerContent>
    <DockPanel MinWidth="220">
        <!--  顶部的头像+昵称  -->
        <StackPanel Margin="0,20" DockPanel.Dock="Top">

            <Image Width="50" Height="50"
                   Source="/Images/Husky.jpg">
                <!--  图片将只显示在椭圆形状的区域内，其余部分将被剪裁掉  -->
                <Image.Clip>
                    <!--使用<Image.Clip>属性来定义剪裁区域-->
                    <EllipseGeometry Center="25,25" RadiusX="25"
                                     RadiusY="25" />
                </Image.Clip>
            </Image>
            <TextBlock Margin="0,10" HorizontalAlignment="Center"
                       Text="Eleanora" />
        </StackPanel>
        <!--  菜单列表  -->
        <ListBox ItemContainerStyle="{StaticResource MyListBoxItemStyle}" ItemsSource="{Binding MenuBars}">
            <ListBox.ItemTemplate>
                <DataTemplate>
                    <StackPanel Background="Transparent" Orientation="Horizontal">
                        <materialDesign:PackIcon Margin="10,0" Kind="{Binding Icon}" />
                        <TextBlock Margin="10,0" Text="{Binding Title}" />
                    </StackPanel>
                </DataTemplate>
            </ListBox.ItemTemplate>
        </ListBox>
    </DockPanel>
</materialDesign:DrawerHost.LeftDrawerContent>
```

在App.xaml中添加ListBoxItem的样式

```xml
  <!--  设置ListBoxItem的样式  -->
  <Style x:Key="MyListBoxItemStyle" TargetType="ListBoxItem">
      <Setter Property="MinHeight" Value="40" />
      <!--  设计ControlTemplate控件模版的算法逻辑  -->
      <Setter Property="Template">
          <Setter.Value>
              <ControlTemplate TargetType="{x:Type ListBoxItem}">
                  <Grid>
                      <Border x:Name="borderHeader" />
                      <Border x:Name="border" />
                      <!--  显示ListBoxItem的内容：水平对齐垂直对齐方式同ListBoxItem  -->
                      <ContentPresenter HorizontalAlignment="{TemplateBinding HorizontalAlignment}" VerticalAlignment="{TemplateBinding VerticalContentAlignment}" />
                  </Grid>
                  <ControlTemplate.Triggers>
                      <!--  选中列表项时左侧边框厚度为4，边框颜色随系统颜色；背景色设置透明度为0.2，颜色随系统变化  -->
                      <Trigger Property="IsSelected" Value="True">
                          <Setter TargetName="borderHeader" Property="BorderThickness" Value="4,0,0,0" />
                          <Setter TargetName="borderHeader" Property="BorderBrush" Value="{DynamicResource MaterialDesign.Brush.Primary.Light}" />
                          <Setter TargetName="border" Property="Background" Value="{DynamicResource MaterialDesign.Brush.Primary.Light}" />
                          <Setter TargetName="border" Property="Opacity" Value="0.2" />
                      </Trigger>
                      <Trigger Property="IsMouseOver" Value="True">
                          <Setter TargetName="border" Property="Background" Value="{DynamicResource MaterialDesign.Brush.Primary.Light}" />
                          <Setter TargetName="border" Property="Opacity" Value="0.2" />
                      </Trigger>
                  </ControlTemplate.Triggers>
              </ControlTemplate>
          </Setter.Value>
      </Setter>
  </Style>
```

新建一个类MenuBar存储列表项

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Prism.Mvvm;

namespace MyTodo.Common.Models
{
	
	/// <summary>
	/// 系统导航菜单实体类
	/// </summary>
    public class MenuBar:BindableBase
    {
		private string icon;
		/// <summary>
		/// 菜单图标
		/// </summary>
		public string Icon
		{
			get { return icon; }
			set { icon = value; }
		}
		private string title;
		/// <summary>
		/// 菜单名称
		/// </summary>
		public string Title
		{
			get { return title; }
			set { title = value; }
		}
		/// <summary>
		/// 菜单命名空间
		/// </summary>
		private string nameSpace;

		public string NameSpace
		{
			get { return nameSpace; }
			set { nameSpace = value; }
		}

	}
}
```

MainViewModel

```C#
using System;
using System.Collections.Generic;
using System.Collections.ObjectModel;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using MyTodo.Common.Models;
using Prism.Mvvm;

namespace MyTodo.ViewModels
{
    public class MainViewModel:BindableBase
    {
        public MainViewModel()
        {
            MenuBars = new ObservableCollection<MenuBar>();
            CreateMenuBar();
        }
        private ObservableCollection<MenuBar> menuBars;

        public ObservableCollection<MenuBar> MenuBars
        {
            get { return menuBars; }
            set { menuBars = value; RaisePropertyChanged();}
        }

        void CreateMenuBar()
        {
            MenuBars.Add(new MenuBar(){Icon = "Home", Title = "首页",NameSpace = "IndexView"});
            MenuBars.Add(new MenuBar(){Icon = "NotebookOutline", Title = "待办事项",NameSpace = "TodoView" });
            MenuBars.Add(new MenuBar(){Icon = "NotebookPlus", Title = "备忘录",NameSpace = "MeloView" });
            MenuBars.Add(new MenuBar(){Icon = "Cog", Title = "设置",NameSpace = "SettingsView" });
        }
    }
}
```

效果：

![](../TyporaImgs/DrawList.gif)