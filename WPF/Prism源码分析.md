

## 1、Dialog.ShowDialog()

prism中打开对话框的实现

```C#
public void ShowDialog(string name, IDialogParameters parameters, DialogCallback callback) 
{

    //如果参数为null,则初始化为新的DialogParameters对象
    parameters ??= new DialogParameters();   

    //从参数中检查是否为模态对话框
    var isModal = parameters.TryGetValue<bool>(KnownDialogParameters.ShowNonModal, out var show) ? !show : true;    

   //从参数中检查窗口名称
    var windowName = parameters.TryGetValue<string>(KnownDialogParameters.WindowName, out var wName) ? wName : null;

   //创建对话框窗口
    IDialogWindow dialogWindow = CreateDialogWindow(windowName);    

   //配置对话框窗口事件,如加载、关闭等
   ConfigureDialogWindowEvents(dialogWindow, callback);    

   //配置对话框窗口内容
   ConfigureDialogWindowContent(name, dialogWindow, parameters);

   //根据是否为模态显示对话框窗口
   ShowDialogWindow(dialogWindow, isModal);
}
```

 配置对话框窗口事件,如加载、关闭等

```C#
protected virtual void ConfigureDialogWindowEvents(IDialogWindow dialogWindow, DialogCallback callback)
{

  Action<IDialogResult> requestCloseHandler = (r) => 
  {
    //设置对话框结果
    dialogWindow.Result = r;  

    //关闭对话框窗口
    dialogWindow.Close();
  };

  RoutedEventHandler loadedHandler = null;

  loadedHandler = (o, e) => 
  {
    //在加载完成后移除加载事件处理
    dialogWindow.Loaded -= loadedHandler;  

    //初始化对话框视图模型
    DialogUtilities.InitializeListener(dialogWindow.GetDialogViewModel(), requestCloseHandler);
  };

  //添加加载事件处理
  dialogWindow.Loaded += loadedHandler;

  
  CancelEventHandler closingHandler = null;

  closingHandler = (o, e) =>
  {
    //如果对话框不可以关闭,则取消关闭操作    
    if (!dialogWindow.GetDialogViewModel().CanCloseDialog())     
      e.Cancel = true;
  };

  //添加关闭事件处理
  dialogWindow.Closing += closingHandler;

  

  EventHandler closedHandler = null;

  closedHandler = async (o, e) => 
  {
    //在关闭后移除相关事件处理

    //调用关闭后的业务逻辑

    //设置对话框结果

    //执行回调方法

    //清理资源
  };

  //添加关闭完成事件处理
  dialogWindow.Closed += closedHandler;

}
```

配置对话框窗口内容

```C#
protected virtual void ConfigureDialogWindowContent(string dialogName, IDialogWindow window, IDialogParameters parameters)
{

  //通过对话框名称从依赖注入容器中解析对话框内容对象
  var content = _containerExtension.Resolve<object>(dialogName);  

  if (!(content is FrameworkElement dialogContent))
    throw new NullReferenceException("Content must be a FrameworkElement");

  //将内容对象的视图模型自动与其绑定
  MvvmHelpers.AutowireViewModel(dialogContent);

  if (!(dialogContent.DataContext is IDialogAware viewModel))   
    throw new NullReferenceException("ViewModel must implement IDialogAware");

  //配置对话框窗口的属性
  ConfigureDialogWindowProperties(window, dialogContent, viewModel);

  //将参数传给视图模型的打开方法
  MvvmHelpers.ViewAndViewModelAction<IDialogAware>(viewModel, d => d.OnDialogOpened(parameters));

}
```

 //根据是否为模态显示对话框窗口

```C#
protected virtual void ShowDialogWindow(IDialogWindow dialogWindow, bool isModal)
{

  //如果模态,使用ShowDialog方法显示
  if (isModal)
    dialogWindow.ShowDialog();

  //如果非模态,使用Show方法显示    
  else
   dialogWindow.Show();

}
```



