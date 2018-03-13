第一个 Flutter 应用
=========

这事一个创建 Flutter 应用的向导。如果你熟悉面向对象编程，和基础的编程概念如 变量，循环，和条件，你可以完成这个教程。不需要有 Dart 经验和移动开发经验。

* [第一步：创建第一个界面](#第一步：创建第一个界面)
* [第二步：使用额外的库](第二步：使用额外的库)
* [第三步：添加状态部件](第三步：添加状态部件)
* [第四步：创建一个无穷的滚动的列表](#第四步：创建一个无穷的滚动的列表)
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

* 这个例子创建了一个材料设计的 app。[材料设计](https://material.io/guidelines/)是一个虚拟的设计语言是一种移动端和 web 的设计标准。 Flutter 提供了丰富的材料设计部件。
* main 方法使用了箭头(`=>`) 符号，用于缩短一行功能或方法
* 这个 app 继承 StatelessWidget ，StatelessWidget 将 app 也变成了一个部件。在 Flutter 中几乎所有的东西都是部件，包含对齐，内边距，布局。
* 材料库中的 Scaffold 部件提供了一个默认的 app bar，title 和 body 属性用于组成整合 home 界面树，子部件也可以是非常复杂的。
* 这个部件的主要工作是 ``build()`` 方法，描述了怎样组织和显示部件
* 这个部件树包含了一个 Center widget， Center widget 内部含有一个 Text widget，Center widget 将其子部件居中显示。


## 第二步：使用额外的库

这一步你将使用一个名为  **english_words** 的开源库，这个库包含了几千个常用的英语单词。

你可以在  [pub.dartlang.org](https://pub.dartlang.org/flutter/) 中找到  [english_words](https://pub.dartlang.org/packages/english_words) 包，它包含了很多的开源三方库。

1.  Flutter 应用通过 pubspec 文件管理资源， 修改  **pubspec.yaml** 文件，添加 **english_words** （3.1.0 或更高版本）将其加入到依赖中（最后一行）：

  ```
  dependencies:
    flutter:
        sdk: flutter

    cupertino_icons: ^0.1.0
    english_words: ^3.1.0
  ```

2. 点击右上方的 **Packages get** 将这个库拉取到项目。你将在 console 中看到下面的信息：

   ```shell
   flutter packages get
   Running "flutter packages get" in startup_namer...
   Process finished with exit code 0
   ```

3.  按照下面的方式将 english_words 添加到 **lib/main.dart** 文件中：

    ```dart
    import 'package:flutter/material.dart';
    import 'package:english_words/english_words.dart';
    ```

    如果你在 AndroidStudio 中添加， AS会在输入的时候提示，并且在输入完成后将北京变成灰色代表你还没使用这个库。

4.  使用这个库来生成的随机单词取代 "Hello World":

    ```dart
    import 'package:flutter/material.dart';
    import 'package:english_words/english_words.dart';

    void main() => runApp(new MyApp());

    class MyApp extends StatelessWidget {
      @override
      Widget build(BuildContext context) {
        final wordPair = new WordPair.random(); // 声明一个常量
        return new MaterialApp(
          title: 'Welcome to Flutter',
          home: new Scaffold(
            appBar: new AppBar(
              title: new Text('Welcome to Flutter'),
            ),
            body: new Center(
              //child: new Text('Hello World'), // 替换成下面的代码...
              child: new Text(wordPair.asPascalCase),  // asPascalCase：驼峰标记法
            ),
          ),
        );
      }
    }
    ```

5.  如果 app 已经运行，点击热更新按钮 (![lightning bolt icon](https://flutter.io/get-started/codelab/images/hot-reload-button.png)) 更新 app 内容。每次点击热更新或保存项目你都将看到一个不同的单词显示在屏幕上。这是因为 word pairing 会在 build 方法内，每次 MaterialApp 需要渲染的时候都会调用。

    ![screenshot at completion of second step](https://flutter.io/get-started/codelab/images/step2-screenshot.png)

#### 遇到问题？

如果你的应用没有正常的运行，通过对比下面链接给出的文件修改你的项目，使其正常运行。

- [**pubspec.yaml**](https://gist.githubusercontent.com/Sfshaza/bb51e3b7df4ebbf3dfd02a4a38db2655/raw/57c25b976ec34d56591cb898a3df0b320e903b99/pubspec.yaml) (这个文件不会在涉及修改了)
- [**lib/main.dart**](https://gist.githubusercontent.com/Sfshaza/bb51e3b7df4ebbf3dfd02a4a38db2655/raw/57c25b976ec34d56591cb898a3df0b320e903b99/main.dart)

## 第三步：添加状态部件

State*less* widgets 是不可变的，它的属性是不可以修改的--所有的属性都是 final 的。

State*ful* widgets 包含一个在部件生命周期内可以修改的状态。实现一个 State*ful* widgets 需要至少两个类：实现 State*ful* widgets 的类 和 一个 State 类的实例。 State*ful* widgets 本身是不可变的的但是 State 类会存在于整个生命周期中。

1. 在 main.dart 中添加 stateful RandomWords widget 。他可以文件的任意位置，建议放在文件的末尾。 RandomWords widget 除了需要创建 State 外没有其他方法。

   ```dart
   class RandomWords extends StatefulWidget {
     @override
     createState() => new RandomWordsState();
   }
   ```

2. 添加 RandomWordsState 类，大部分的 app 代码都在这个类里面。这个类会保存生成的的 word pairs ，用于在用户滚动的时候生成无尽的单词。用户通过点击列表项的安心图标来将单词加入删除保存的列表。

   你将一点一点地实现这个类，通过下面的代码创建一个最小的类：

   ```
   class RandomWordsState extends State<RandomWords> {
   }
   ```

3. 添加完这个状态类后 IDE 会报告缺少一个 build 方法。接下来，将添加一个基础的 build 方法将生成单词的工作从 MyApp 类迁移到 RandomWordsState 中。
   将下面的代码添加到 RandomWordState 中：

   ```
   class RandomWordsState extends State<RandomWords> {
     @override
     Widget build(BuildContext context) {
       final wordPair = new WordPair.random();
       return new Text(wordPair.asPascalCase);
     }
   }
   ```

4. 删除 MyApp 中生成单词的代码，替换成下面的代码：

   ```
   class MyApp extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       //final wordPair = new WordPair.random();  // 删除这一行

       return new MaterialApp(
         title: 'Welcome to Flutter',
         home: new Scaffold(
           appBar: new AppBar(
             title: new Text('Welcome to Flutter'),
           ),
           body: new Center(
             //child: new Text(wordPair.asPascalCase), // 修改成下面的代码
             child: new RandomWords(), // ... 替换成 RandomWords
           ),
         ),
       );
     }
   }
   ```

5. 重启应用，如果你尝试热更新，你可能得到下面的警告：

   ```
   Reloading...
   Not all changed program elements ran during view reassembly; consider
   restarting.
   ```

   这可能是误报，但是请考虑重启来保证你的修改已经应用到界面上。应用的界面应该和之前一样，每次你热更新或保存 app 的时候都会显示一个新的单词。

   ![screenshot at completion of third step](https://flutter.io/get-started/codelab/images/step3-screenshot.png)

#### 遇到问题？

如果你的 app 没有预期执行，通过对比下面链接给出的代码修正

- [**lib/main.dart**](https://gist.githubusercontent.com/Sfshaza/d7f13ddd8888556232476be8578efe40/raw/329c397b97309ce99f834bf70ebb90778baa5cfe/main.dart)

## 第四步：创建一个无穷的滚动的列表

这一步，你会拓展 RandomWordsState 来生成显示一个列表。随着用户的滚动，这个列表会显示在 ListView Widget 中，可以无限的滚动。 ListView 的 `builder` 工厂构造函数允许你根据需求构建一个懒加载的列表函数。

1. 添加一个名为 _suggestions 列表