



## 1、Function To Open The Browser

The difference between `Process.Start(new ProcessStartInfo("cmd", $"/c start {url}"));` and `Process.Start(new ProcessStartInfo(url) { UseShellExecute = true });` lies in how they open the URL.

1. `Process.Start(new ProcessStartInfo("cmd", $"/c start {url}"));`:
   This code uses the Windows command prompt (`cmd.exe`) to open the URL. It starts a new process with the command prompt and passes the `/c start {url}` argument, where `{url}` is the URL you want to open. The `/c` flag tells the command prompt to execute the command and then terminate.

    

   This method allows you to open the URL using the default browser on the user's system. It essentially simulates the same behavior as if the user had manually typed the URL in the command prompt and pressed Enter. However, using the command prompt may introduce a slight delay before the URL opens.

2. `Process.Start(new ProcessStartInfo(url) { UseShellExecute = true });`:
   This code directly starts a new process with the specified URL. The `UseShellExecute` property is set to `true`, which allows the operating system shell to handle the execution of the URL.

    

   When `UseShellExecute` is set to `true`, the operating system will use the default application associated with that URL scheme to open the URL. For example, if the URL is a web address (http/https), it will open in the default web browser. This method provides a more direct and efficient way to open the URL compared to using the command prompt.

In summary, the first approach uses the command prompt to open the URL, while the second approach directly starts a process with the URL using the default application associated with that URL scheme. Both methods achieve the goal of opening the URL, but the second method is generally more straightforward and efficient.

> `Process.Start(new ProcessStartInfo("cmd", $"/c start {url}"));` 和 `Process.Start(new ProcessStartInfo(url) { UseShellExecute = true });` 的区别在于它们打开URL的方式。
>
> 1. `Process.Start(new ProcessStartInfo("cmd", $"/c start {url}"));`：
>    这段代码使用了Windows命令提示符（`cmd.exe`）来打开URL。它启动一个新的进程，并传递`/c start {url}`参数，其中`{url}`是你想打开的URL。`/c`标志告诉命令提示符执行命令后立即终止。
>
>     
>
>    这种方法允许你使用用户系统上的默认浏览器来打开URL。它实际上模拟了用户在命令提示符中手动输入URL并按下回车键的行为。然而，使用命令提示符可能会在URL打开之前引入轻微的延迟。
>
> 2. `Process.Start(new ProcessStartInfo(url) { UseShellExecute = true });`：
>    这段代码直接启动一个新的进程，并使用指定的URL。`UseShellExecute`属性被设置为`true`，这允许操作系统的Shell来处理URL的执行。
>
>     
>
>    当`UseShellExecute`设置为`true`时，操作系统将使用与该URL方案关联的默认应用程序来打开URL。例如，如果URL是一个网址（http/https），它将在默认的Web浏览器中打开。与使用命令提示符相比，这种方法提供了一种更直接和高效的打开URL的方式。
>
> 总结起来，第一种方法使用命令提示符来打开URL，而第二种方法直接启动一个进程，并使用与该URL方案关联的默认应用程序。这两种方法都能实现打开URL的目标，但第二种方法通常更直接和高效。

## 2、Use `TextBlock` To Simulate Hyperlink

When using the Prism framework with MVVM pattern, you can combine the above functionality with MVVM.

First, create a view model called "MainViewModel" and create a command called "NavigateCommand" to handle the navigation logic.

```csharp
public class MainViewModel : BindableBase
{
    public DelegateCommand<string> NavigateCommand { get; }

    public MainViewModel()
    {
        NavigateCommand = new DelegateCommand<string>(NavigateToBrowser);
    }

    private void NavigateToBrowser(string url)
    {
        Process.Start(new ProcessStartInfo(url));
    }
}
```

In this view model, we use the BindableBase base class from the Prism library to implement property notification. NavigateCommand is a delegate command with a string parameter to handle the navigation logic.

In the view, you can use the TextBlock control and utilize Prism's EventToCommand behavior to bind the click event to the NavigateCommand.

```xml
<TextBlock Text="Click Me">
    <i:Interaction.Triggers>
        <i:EventTrigger EventName="MouseLeftButtonDown">
            <prism:InvokeCommandAction Command="{Binding NavigateCommand}" CommandParameter="https://www.example.com" />
        </i:EventTrigger>
    </i:Interaction.Triggers>
</TextBlock>
```

In this example, we use the TextBlock control to display the text. Then, we use Prism's Interaction.Triggers and EventTrigger to capture the left mouse button down event. Finally, we use Prism's InvokeCommandAction to bind the event to the NavigateCommand and pass "https://www.example.com" as the CommandParameter.

By following this approach, you can implement the functionality of clicking the text and navigating to the specified URL using the Prism framework with MVVM pattern.

> 当使用Prism框架的MVVM模式时，你可以将上述功能与MVVM结合起来实现。
>
> 首先，创建一个名为"MainViewModel"的视图模型，并在其中创建一个名为"NavigateCommand"的命令来处理跳转逻辑。
>
> ```csharp
> public class MainViewModel : BindableBase
> {
>     public DelegateCommand<string> NavigateCommand { get; }
> 
>     public MainViewModel()
>     {
>         NavigateCommand = new DelegateCommand<string>(NavigateToBrowser);
>     }
> 
>     private void NavigateToBrowser(string url)
>     {
>         Process.Start(new ProcessStartInfo(url));
>     }
> }
> ```
>
> 在这个视图模型中，我们使用了Prism库中的BindableBase基类来实现属性通知机制。NavigateCommand是一个带有字符串参数的委托命令，用于处理跳转逻辑。
>
> 在视图中，你可以使用TextBlock控件，并使用Prism的EventToCommand行为来将点击事件绑定到NavigateCommand命令。
>
> ```xml
> <TextBlock Text="Click Me">
>     <i:Interaction.Triggers>
>         <i:EventTrigger EventName="MouseLeftButtonDown">
>             <prism:InvokeCommandAction Command="{Binding NavigateCommand}" CommandParameter="https://www.example.com" />
>         </i:EventTrigger>
>     </i:Interaction.Triggers>
> </TextBlock>
> ```
>
> 在这个示例中，我们使用TextBlock控件来显示文本。然后，我们使用Prism库的Interaction.Triggers和EventTrigger来捕获鼠标左键点击事件。最后，我们使用Prism的InvokeCommandAction将事件绑定到NavigateCommand命令，并将"https://www.example.com"作为CommandParameter传递。
>
> 通过这种方式，你可以使用Prism框架的MVVM模式来实现一个点击文本后跳转到指定URL的功能。

## 

> 1. 

## Interaction.Triggers



```xml
<ListBox Grid.Row="1" Margin="0,20"
         ItemsSource="{Binding AboutList}">
    <ListBox.ItemTemplate>
        <DataTemplate>
            <StackPanel Orientation="Horizontal">
                <!--  地址中文概要  -->
                <TextBlock Text="{Binding ItemName}" />
                <!--  超链接样式  -->
                <TextBlock FontSize="15" Foreground="RoyalBlue"
                           Text="{Binding Url}"
                           TextDecorations="Underline">
                    <b:Interaction.Triggers>
                        <b:EventTrigger EventName="MouseLeftButtonDown">
                            <b:InvokeCommandAction Command="{Binding DataContext.NavigateToTargetCommand, RelativeSource={RelativeSource AncestorType=UserControl}}" CommandParameter="{Binding Url}" />
                        </b:EventTrigger>
                    </b:Interaction.Triggers>
                </TextBlock>
            </StackPanel>
        </DataTemplate>
    </ListBox.ItemTemplate>
</ListBox>
```

nteraction.Triggers is an attached property that allows us to define triggers and actions for specific events. In this example, we define an EventTrigger for the TextBlock, which triggers the specified action when the MouseLeftButtonDown event occurs.

Within the EventTrigger, we use InvokeCommandAction as the action. InvokeCommandAction is a behavior that allows us to execute commands. We bind the Command property to the NavigateToTargetCommand property in the DataContext.

To correctly bind the NavigateToTargetCommand, we use RelativeSource to find the nearest UserControl as the binding source. This binding allows us to access the NavigateToTargetCommand in the UserControl's DataContext.

The CommandParameter property is bound to the Url property, which means that when the command is executed, the value of the Url property will be passed as a parameter to the NavigateToAction method.

> 1. `Interaction.Triggers`是一个附加属性，它允许我们为特定的事件定义触发器和操作。在这个例子中，我们为`TextBlock`定义了一个`EventTrigger`，当`MouseLeftButtonDown`事件发生时，触发执行操作。
> 2. 在`EventTrigger`中，我们使用了`InvokeCommandAction`作为操作。`InvokeCommandAction`是一个可以执行命令的行为。我们将`Command`属性绑定到`DataContext`中的`NavigateToTargetCommand`属性。
> 3. 为了正确绑定`NavigateToTargetCommand`，我们使用了`RelativeSource`来找到最近的`UserControl`作为绑定源。这个绑定允许我们在`UserControl`的`DataContext`中找到`NavigateToTargetCommand`。
> 4. `CommandParameter`属性绑定到`Url`属性，这意味着当命令执行时，`Url`属性的值将作为参数传递给`NavigateToAction`方法。

<b:Interaction.Triggers> is a mechanism in Prism library (Prism is a development framework for building extensible, modular, and testable WPF applications) that provides a convenient way to handle triggering actions in XAML when specific events occur.

<b:Interaction.Triggers> is typically used to bind XAML events to commands in the ViewModel. It allows you to define triggers for specific events and execute specified actions when those events occur.

<b:Interaction.Triggers> consists of two main parts: EventTrigger and TriggerAction.

1. EventTrigger: It defines the specific event to trigger. By specifying the name of the event, you can instruct EventTrigger to execute the associated actions when that event occurs.
2. TriggerAction: It defines the action to execute. Actions can be of various types, such as commands, animations, property changes, etc. You can attach one or multiple TriggerActions to an EventTrigger to execute those actions when the event occurs.

In our example, we use `<b:Interaction.Triggers>` to define an EventTrigger and within the EventTrigger, we use a TriggerAction, specifically `InvokeCommandAction`. When the `MouseLeftButtonDown` event occurs, the `InvokeCommandAction` will execute the bound command and pass the bound parameter to the command's execution method.

By using `<b:Interaction.Triggers>`, we can bind XAML events to ViewModel commands and achieve the functionality of executing specified actions when specific events occur.

> 
>
> `<b:Interaction.Triggers>`是Prism库（Prism是一个用于构建可扩展、模块化、可测试的WPF应用程序的开发框架）中的一部分，它提供了一种简单的方式来处理在特定事件发生时执行操作的需求。
>
> `<b:Interaction.Triggers>`通常用于将XAML中的事件与ViewModel中的命令进行绑定。它允许你为特定事件定义触发器，并在该事件发生时执行指定的操作。
>
> `<b:Interaction.Triggers>`有两个主要的部分：`EventTrigger`和`TriggerAction`。
>
> 1. `EventTrigger`：它定义了要触发的特定事件。通过指定事件的名称，你可以告诉`EventTrigger`在该事件发生时触发相应的操作。
> 2. `TriggerAction`：它定义了要执行的操作。操作可以是各种类型，如命令、动画、更改属性等。你可以将一个或多个`TriggerAction`附加到`EventTrigger`中，以在事件发生时执行这些操作。
>
> 在我们的示例中，我们使用了`<b:Interaction.Triggers>`来定义一个`EventTrigger`，并在`EventTrigger`中使用了一个`TriggerAction`，即`InvokeCommandAction`。当`MouseLeftButtonDown`事件发生时，`InvokeCommandAction`会执行绑定的命令，并将绑定的参数传递给命令的执行方法。
>
> 通过使用`<b:Interaction.Triggers>`，我们可以将XAML中的事件与ViewModel的命令进行绑定，实现了在特定事件发生时执行指定操作的功能。

I