第一个 Flutter 应用
=========

这事一个创建 Flutter 应用的向导。如果你熟悉面向对象编程，和基础的编程概念如 变量，循环，和条件，你可以完成这个教程。不需要有 Dart 经验和移动开发经验。

* [第一步：创建第一个界面](#第一步：创建第一个界面)
* 第二步：使用额外的包
* 第三步：添加状态部件
* 第四部：创建一个无穷的滚动的列表
* 第五步：添加操作
* 第六步：跳转到新页面
* 第七步：修改 UI 主题
* 完事

### 你要做的

你将实现一个简单的手机应用，这个应用为新公司的名称生成一些建议。用户可以选中和取消一个名字，保存选中的名字。代码会一次生成十个名字，随证用户的滑动新的名字也会继续生成。用户可以点击标题栏的列表图标跳转到新的界面查看已经选中的名字。

![演示图片](https://flutter.io/get-started/codelab/images/startup-namer-app.gif)

GIF 动画展示了最终的应用。

你将学到：

* Flutter 应用的基础架构
* 通过查找和使用包拓展应用
* 通过热更新实现快速迭代
* 怎样实现有状态的部件
* 怎样创建一个 无尽，懒加载的列表
* 怎样创建，跳转到一个界面
* 怎样通过使用主题修改应用样式

你将用到：

* Flutter SDK（包含 Flutter 引擎，framework ，部件和 Dart SDK）v0.1.4或更新
* Android Studio IDE（其他 IDE或命令行也可以）
* IDE 的插件

## 第一步：创建第一个界面

通过 IDE 创建一个空的 Flutter 应用，并将其命名为 **startup_namer** 。修改生成的代码来完成本应用。

在这一步你只需要 **lib/main.dart** 文件，并在这个文件中写 Dart 代码。

> 粘贴代码到 IDE 中可能造成缩紧不一致，通过右击 IDE > 格式代码
>
> AS ：**Reformat Code with dartfmt**. 
>
> VS Code ：**Format Document**
>
> 命令行：``flutter format <filename>``

1. 修改 lib/main.dart 文件，将原始的代码替换成下面的代码。在设备的屏幕中间会显示 “Hello World”

```dart
import 'package:flutter/material.dart';

void main() => runApp(new MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'Welcome to Flutter',
      home: new Scaffold(
        appBar: new AppBar(
          title: new Text('Welcome to Flutter'),
        ),
        body: new Center(
          child: new Text('Hello World'),
        ),
      ),
    );
  }
}
```

2. 运行这个 app。

![Hello-World](https://flutter.io/get-started/codelab/images/hello-world-screenshot.png)

#### 分解

* 这个例子创建了一个材料设计的 app。[材料设计](https://material.io/guidelines/)是一个虚拟的设计语言是一种移动端和 web 的设计标准。 Flutter 提供了丰富的材料设计组件。
* main 方法使用了箭头(`=>`) 符号，用于缩短一行功能或方法
* 这个 app 继承 StatelessWidget ，StatelessWidget 将 app 也变成了一个部件。在 Flutter 中几乎所有的东西都是部件，包含对齐，内边距，布局。
* 材料包中的 Scaffold 部件提供了一个默认的 app bar，title 和 body 属性用于组成整合 home 界面树，子部件也可以是非常复杂的。
* 这个部件的主要工作是 ``build()`` 方法，描述了怎样组织和显示部件
* 这个部件树包含了一个 Center widget， Center widget 内部含有一个 Text widget，Center widget 将其子部件居中显示。



