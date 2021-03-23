# DependencyProperty
### About us
Contributors [Here.](https://devncore.org/aboutus/contributors)

### DevNcore
GitHub Organization [Here.](https://github.com/devncore)   
Official Website [Here.](https://devncore.org) 

### License Policy
[![MIT license](https://img.shields.io/badge/License-MIT-blue.svg)](https://lbesson.mit-license.org/)
[![GPLv3 license](https://img.shields.io/badge/License-GPLv3-blue.svg)](http://perso.crans.org/besson/LICENSE.html)

<br />  

## _What is the DependencyProperty?_
The __DependencyProperty__ class is one of the most important design bases hidden deep in the .Net Framework WPF.

This class is protected by sealed from the .Net Framework.
This property differs from the one-dimensional general property in that it not only stores field values, but also takes advantage of the various functions provided within the class.
Most importantly, there is a full foundation for data binding. You can also send notifications whenever you bind something.  

The MVVM development methodology already has a limited set of DependencyProperty provided by the .Net Framework, so this technology is essential to more aggressive use of Binding.


## 1. Overview
DependencyProperty is one of the key design elements of the WPF. This involves a combination of concepts and logical structures rather than a single function, requiring in-depth research and a somewhat higher degree of difficulty in the scope and depth of the technology.

#### 1.1. Class Version 
The first target version of DependencyProperty is based on .NET Framework `3.0`
| Target Name    | Version                                                                                  |
|:---------------|:-----------------------------------------------------------------------------------------|
| .NET           | 5.0                                                                                      |
| .NET Core      | 3.0, 3.1                                                                                 |
| .NET Framework | 3.0, 3.5, 4.0, 4.5, 4.5.1, 4.5.2, 4.6, 4.6.1, 4.6.2, 4.7, 4.7.1, 4.7.2, 4.8              |

##### _So, .NET Framework 2.0 doesn't allow us to use DependencyProperty?_   
> That's right. WPF starts at 3.0. :smile:

#### 1.2. Class Information
| Assembly             | Namespace                   | Class Access        | Base Class      |
|:---------------------|:----------------------------|:--------------------|:----------------|
| WindowsBase.dll      | System.Windows              | `sealed`            | `Object`        |

#### 1.3. Class Structure
Access rights in the DependencyProperty class is `sealed` and have a structure that cannot be inherited directly from the custom class.

```csharp
namespace System.Windows
{
    public sealed class DependencyProperty
    {

    }   
}
```
<br />

## 2. Declaration
DependencyProperty can be registered in two ways.
- [Standard](#21-Standard)
- [Extender](#22-Extender)

### 2.1. Standard
Standard method is to connect(register) directly to the `Owner UI` class through the `DependencyProperty.Register` method.
- [Int](#211-Standard-Int)
- [Boolean](#212-Standard-Boolean)
- [String](#213-String-Type)
- [Object](#214-Object-Type)
- [Geometry](#215-Geometry-Type)
- [Brush](#216-Brush-Type)
- [Double](#217-Double-Type)
- [ICommand](#218-ICommand-Type)

#### 2.1.1. [Standard] Int
```csharp
public static readonly DependencyProperty AgeProperty = DependencyProperty.Register(
    "Age", typeof(int), typeof(<class>), new PropertyMetadata(0));
```
```csharp
public int Age
{
    get { return (int)this.GetValue(AgeProperty); }
    set { this.SetValue(AgeProperty, value); }
}
```
 
#### 2.1.2. [Standard] Boolean
```csharp
public static readonly DependencyProperty IsUsedProperty = DependencyProperty.Register(
    "IsUsed", typeof(bool), typeof(<class>), new PropertyMetadata(false));
```
```csharp
public bool IsUsed 
{ 
    get { return (bool)this.GetValue(IsUsedProperty); }
    set { this.SetValue(IsUsedProperty, value); }
}
```

#### 2.1.3. [Standard] String
```csharp
public static readonly DependencyProperty PlaceHolderProperty = DependencyProperty.Register(
    "PlaceHolder", typeof(string), typeof(<class>), new PropertyMetadata(""));
```
```csharp
public string PlaceHolder
{
    get { return (string)this.GetValue(PlaceHolderProperty); }
    set { this.SetValue(PlaceHolderProperty, value); }
}
```

#### 2.1.4. [Standard] Object

It is actually the same as the Content Property included in the `ContentControl` class.  
If you inherit ContentControl and create a control that defines ContentPresenter, use Object-type DependencyProperty.

```csharp
public static readonly DependencyProperty ContentProperty = DependencyProperty.Register(
    "Content", typeof(object), typeof(<class>), new PropertyMetadata(""));
```
```csharp
public object Content
{
    get { return (object)this.GetValue(ContentProperty); }
    set { this.SetValue(ContentProperty, value); }
}
```
- #### Exists Properties
  - Content in `ContentControl` (Button, CheckBox, userControl, Window Etc...)
  - Tag in `Control` (Button, Window, Grid, StackPanel, Etc...)

#### 2.1.5. [Standard] Geometry
```csharp
public static readonly DependencyProperty DataProperty = DependencyProperty.Register(
    "Data", typeof(Geometry), typeof(<class>), new PropertyMetadata(null));
```
```csharp
public Geometry Data
{
    get { return (Geometry)this.GetValue(DataProperty); }
    set { this.SetValue(DataProperty, value); }
}
```
- #### Exists Properties
  - Data in `Path`

#### 2.1.6. [Standard] Brush
```csharp
public static readonly DependencyProperty FillProperty = DependencyProperty.Register(
    "Fill", typeof(Brush), typeof(<class>), new PropertyMetadata(null));
```
```csharp
public Brush Fill
{
    get { return (Brush)this.GetValue(FillProperty); }
    set { this.SetValue(FillProperty, value); }
}
```


#### 2.1.7. [Standard] Double
```csharp
public static readonly DependencyProperty IconWidthProperty = DependencyProperty.Register(
    "IconWidth", typeof(double), typeof(<class>), new PropertyMetadata(0));
```
```csharp
public double IconWidth
{
    get { return (double)this.GetValue(IconWidthProperty); }
    set { this.SetValue(IconWidthProperty, value); }
}
```

#### 2.1.8. [Standard] ICommand
```csharp
public static readonly DependencyProperty SelectionCommandProperty = DependencyProperty.Register(
    "SelectionCommand", typeof(ICommand), typeof(<class>));
```
```csharp
public ICommand SelectionCommand
{
    get { return (ICommand)this.GetValue(SelectionCommandProperty); }
    set { this.SetValue(SelectionCommandProperty, value); }
}
```
<br />

### 2.2. Extender
#### 2.2.1. [Extender] String
```csharp
class PasswordExtender
{
    public static readonly DependencyProperty PasswordProperty =
        DependencyProperty.RegisterAttached("Password",
        typeof(string), typeof(PasswordExtender),
        new FrameworkPropertyMetadata(string.Empty, OnPasswordPropertyChanged));
    public static string GetPassword(DependencyObject dp)
    {
        return (string)dp.GetValue(PasswordProperty);
    }

    public static void SetPassword(DependencyObject dp, string value)
    {
        dp.SetValue(PasswordProperty, value);
    }
    
    private static void OnPasswordPropertyChanged(DependencyObject sender,
        DependencyPropertyChangedEventArgs e)
    {
    }
}
```
<br />

### 3. Property Changed
```csharp
public string Password
{
    get { return (string)this.GetValue(PasswordProperty); }
    set { this.SetValue(PasswordProperty, value); }
}
public static readonly DependencyProperty PasswordProperty =
    DependencyProperty.Register("Password", typeof(string), typeof(VisualPassword),
        new PropertyMetadata(string.Empty, PasswordPropertyChanged));

private static void PasswordPropertyChanged(DependencyObject d, DependencyPropertyChangedEventArgs e)
{
    
}
```
<br />

### 4. CoerceValueCallback
```csharp
public string Password
{
    get { return (string)this.GetValue(PasswordProperty); }
    set { this.SetValue(PasswordProperty, value); }
}

public static readonly DependencyProperty PasswordProperty =
DependencyProperty.Register(
        "Password", 
        typeof(string), 
        typeof(VisualPassword),
        new FrameworkPropertyMetadata( 
                string.Empty, 
                FrameworkPropertyMetadataOptions.BindsTwoWayByDefault | FrameworkPropertyMetadataOptions.Journal,
                new PropertyChangedCallback(OnPasswordPropertyChanged),
                new CoerceValueCallback(CoercePassword),
                true, 
                UpdateSourceTrigger.LostFocus 
                ));


private static void OnPasswordPropertyChanged(DependencyObject sender, DependencyPropertyChangedEventArgs args)
{
    VisualPassword p = sender as VisualPassword;

    if (!p._password.Password.Equals(args.NewValue?.ToString()))
    {
        p._password.PasswordChanged -= p._password_PasswordChanged;
        p._password.Password = args.NewValue?.ToString();
        p._password.PasswordChanged += p._password_PasswordChanged;
    }

    private static object CoercePassword(DependencyObject d, object value)
    {
        if (value == null)
        {
            return String.Empty;
        }

        return value;
    }
}
```
<br />

## 5. Quiz
1. Which is the appropriate Access Modifier for the DependencyProperty class? 
- ① Abstruct   
- ② Sealed   
- ③ Virtual   
- ④ struct   

2. Select the Namespace you need to use the DependencyProperty.
- ① using System;   
- ② using System.Windows;   
- ③ using System.Windows.Threading;   
- ④ using System.ComponentModel;   

3. What assembly in the .Net Framework provides DependencyProperty class?
- ① System.dll;   
- ② System.Windows.dll;   
- ③ WindowsBase.dll;   
- ④ PresentationFramework.dll;  
<br />

## 6. References
### 6.1 Community Docs
#### WPF Tutorial
> DependencyProperties [here.](https://www.wpftutorial.net/DependencyProperties.html)   
#### SO Documentation
> Dependency-Properties [here.](https://sodocumentation.net/wpf/topic/2914/dependency-properties)   
#### Microsoft Docs
> DependencyProperty Class [Here.](https://docs.microsoft.com/ko-kr/dotnet/api/system.windows.dependencyproperty?view=netframework-4.8)   

