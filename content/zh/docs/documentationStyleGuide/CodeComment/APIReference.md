
---
title: "源代码API参考文档"
linkTitle: "源代码API参考文档"
weight: 10
---

创建API后，需要提供对应的API参考文档，通常是从源代码中生成的公开类、方法、常量及其他成员。根据不同的编程语言，依照本指南给出的基本准则，
并参照特定语言样式指南。

此指南不含该 Web API 的参考文档样式，编写 Web API 的参考文档样式时，请参考 Web API 的参考文档样式说明。

## 基础知识

API参考文档必须提供以下各项的描述：

* API的每个类、接口、结构体和其他类似的成员；
* 每个常量、字段、枚举、类型定义等；
* 每个方法、以及每个参数的说明、返回值和可能的异常说明。

以下是具体的规则。在某些情况下，它们对于特定的API或特定的语言没有意义，但一般来说，请遵循以下准则：

* 在每个唯一类，界面等上，在顶部都包含一个5-20行代码示例：

* 将所有API名称，类，方法，常量等放入代码中，并将每个名称链接到相应的参考文档（大多数文档生成器会自动为您执行此操作）；

* 将参数名用斜体表示。例如，当您引用类似 `doSomething(Uri data, int count)` 的参数时，将 *data*、*count* 斜体化。

* 确保文档中的类的拼写和代码中相同。

    * 不要使类名复数（Intents，Activities）; 而是添加一个复数名词（Intent对象，Activity实例）。

    * 如果一个类的名称是一个常用术语，则可以使用相应的英语单词来引用它，该单词要小写而不是使用代码字体（activities, action bar）。

## 类、接口、结构体

在类的注释的第一句话中，简要说明类或接口的预期用途和功能，以及一些无法从类名称或签名中得到的信息。文档工具和IDE会自动提取每个类的第一句话，
展示到类的文档列表，因此第一句话应精炼。然后，详细说明API的使用方法，包括：
如何调用或实例化API、一些关键功能以及最佳实践或陷阱。

**例子**

ActionBar 类的第一句注释：

处于活动状态的主工具栏，可以显示活动标题、应用程序级别的功能导航以及其他交互的对象。


## 成员

成员（常量、属性）的注释应尽可能简短，并链接到使用了该常量或属性的相关方法。

**例子**

ActionBar 类的 `DISPLAY_SHOW_HOME` 常量的注释：

在此操作栏中显示“主页”元素，从而为徽标、图标等其他导航元素留出更多空间。

另请参阅： `setDisplayOptions(int)`，`setDisplayOptions(int, int)`

## 方法

在方法注释的第一句话中，简要说明该方法执行的操作。在随后的句子中，解释为什么以及如何使用该方法，声明在调用之前必须满足的所有先决条件，
提供有关可能发生的异常的详细信息，并指定任何相关的API。

同时，描述调用该方法所需的任何依赖项，以及缺少此依赖时该方法的行为（例如该方法抛出 `SecurityException`或该方法返回`null`）。

**例子**

` Activity.isChangingConfigurations() ` 方法的注释：

检查此活动是否正在销毁中，以便使用新配置重新创建此活动。这通常用于 `onStop()` 
来确定状态从而判断是否要清除活动或者将活动传递给活动的下一个实例`onRetainNonConfigurationInstance()`

另请参阅： `setDisplayOptions(int)`，`setDisplayOptions(int, int)`

### 描述

* 如果某个方法执行某个操作并返回一些数据，请以描述该操作的动词开始描述，例如：

    * 添加新的鸟到鸟类列表中，并返回新条目的 ID；
* 如何它是 getter 方法并返回布尔值， 描述以 “检查是否...” 开始；
* 如果它是 getter 方法并且返回的不是布尔值，则以 “获取...” 开始；
* 如何它没有返回值，请使用类似下述的动词作为开头：
    * 启用一项新技能或设置： “设置...”；
    * 更新属性：“更新...”；
    * 删除内容：“删除...”；
    * 注册回调或其他元素以供以后参考：“Registers...”；
    * 对于回调：“由...调用”（例如：有注册器在...时调用，然后，子类将此方法实现为...）；

### 弃用 

如果该方法将在未来弃用，则需要在第一句话中告知用户该方法的最后支持版本。随后，可以向开发者解释为什么不推荐使用该API以及其他对开发人员有用的信息。

**例子**：

不推荐使用，请改用 `CameraPose`

不推荐使用，使用 `getField()`方法访问此字段