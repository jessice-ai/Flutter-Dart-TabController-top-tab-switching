# sun009

A new Flutter application.

## Getting Started


Flutter 1.22.3 Dart SDK 2.10.3 通过TabControllers实现顶部tab切换 介绍生命周期函数

说明：使用TabControllers实现顶部tab切换,必须使用动态组件,也就是 StatefulWiget

一、TabControllers实现顶部tab切换实例

说明：使用 TabControllers 如果这里面代码修改执行，记得点一下 Flutter Hot Restart 重新编译一下，否则会出现错误

import 'package:flutter/material.dart';

void main() {
  runApp(sunApp());
}

/**
 * 自定义 Widget 组件
 * StatelessWidget 状态不可改变组件，抽象类，需要实现build方法
 * StatefulWidget 状态可改变组件
 */
class sunApp extends StatelessWidget{
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    //throw UnimplementedError();
    /**
     *  一般我们会使用 MaterialApp() 作为Flutter的一个根组件使用
     *  常用属性：
     *  home 主页
     *  title 标题
     *  color 颜色
     *  theme 主题
     *  routes 路由
     */
    return MaterialApp(
      home:Scaffold(
        //appBar 导航
        //body 主体
        body: sunHomeContent(),
      ),
      //theme 主体
      theme: ThemeData(
          primarySwatch: Colors.amber  //修改主体颜色
      ),
    );
  }
}

/**
 * StatelessWidget 无状态组件
 * StatefulWidget 有状态组件，点击页面脚本出发页面数据发生变化
 */
//说明：使用TabControllers实现顶部tab切换,必须使用动态组件,也就是 StatefulWiget
class sunHomeContent extends StatefulWidget{
  @override
  State<StatefulWidget> createState() {
    // TODO: implement createState
    //throw UnimplementedError();
    //这里不能直接返回组件，因为返回的数据类型是 State<StatefulWidget>
    return sunHomeContentState();
  }
}
/**
 * 必须集成 SingleTickerProviderStateMixin
 */
class sunHomeContentState extends State with SingleTickerProviderStateMixin{
  TabController _tabController;

  @override
  void initState() {
    super.initState();
    _tabController = TabController(length: 4, vsync: this);
  }

  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    //throw UnimplementedError();
    return Scaffold(
      appBar: AppBar(
        title: Text("分类"),
        bottom: TabBar(
          controller: this._tabController, //注意，必须得加
          tabs: <Widget>[
            Tab(
              text: "热销", //关键词
              //icon: Icon(Icons.directions_bike), //图标
            ),
            Tab(
              text: "内衣",
              //icon: Icon(Icons.directions_bike),
            ),
            Tab(
              text: "数码",
              //icon: Icon(Icons.directions_bike),
            ),
            Tab(
              text: "特产",
              //icon: Icon(Icons.directions_bike),
            ),
          ],

        ),
      ),
      body: TabBarView(
        controller: _tabController, //注意，必须得加
        children: <Widget>[
          Center(
            child: Text("热销"), //内容
          ),
          Center(
            child: Text("内衣"), //内容
          ),
          Center(
            child: Text("数码"), //内容
          ),
          Center(
            child: Text("特产"), //内容
          ),
        ],
      ),
    );
  }
}


问题：Flutter: Unimplemented handling of missing static target

解决方法：

1) Android Studio -> 提示框中 -> Run选项 -> Flutter Hot Restart (图标是一个椭圆圈，中间是个闪电符号)
2) Flutter Hot Restart 重新编译一下，否则会出现错误


二、TabControllers实现顶部tab切换 - 侦听

侦听选中了那个Index


import 'package:flutter/material.dart';

void main() {
  runApp(sunApp());
}

/**
 * 自定义 Widget 组件
 * StatelessWidget 状态不可改变组件，抽象类，需要实现build方法
 * StatefulWidget 状态可改变组件
 */
class sunApp extends StatelessWidget{
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    //throw UnimplementedError();
    /**
     *  一般我们会使用 MaterialApp() 作为Flutter的一个根组件使用
     *  常用属性：
     *  home 主页
     *  title 标题
     *  color 颜色
     *  theme 主题
     *  routes 路由
     */
    return MaterialApp(
      home:Scaffold(
        //appBar 导航
        //body 主体
        body: sunHomeContent(),
      ),
      //theme 主体
      theme: ThemeData(
          primarySwatch: Colors.amber  //修改主体颜色
      ),
    );
  }
}

/**
 * StatelessWidget 无状态组件
 * StatefulWidget 有状态组件，点击页面脚本出发页面数据发生变化
 */
//说明：使用TabControllers实现顶部tab切换,必须使用动态组件,也就是 StatefulWiget
class sunHomeContent extends StatefulWidget{
  @override
  State<StatefulWidget> createState() {
    // TODO: implement createState
    //throw UnimplementedError();
    //这里不能直接返回组件，因为返回的数据类型是 State<StatefulWidget>
    return sunHomeContentState();
  }
}
/**
 * 必须集成 SingleTickerProviderStateMixin
 */
class sunHomeContentState extends State with SingleTickerProviderStateMixin{
  TabController _tabController;

  @override
  void initState() {
    super.initState();
    _tabController = TabController(length: 4, vsync: this);
    //侦听
    _tabController.addListener(() {
      //打印选中项索引值
      var index = _tabController.index;
      print("Jessice:${index}");
    });
  }

  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    //throw UnimplementedError();
    return Scaffold(
      appBar: AppBar(
        title: Text("分类"),
        bottom: TabBar(
          controller: this._tabController, //注意，必须得加
          tabs: <Widget>[
            Tab(
              text: "热销", //关键词
              //icon: Icon(Icons.directions_bike), //图标
            ),
            Tab(
              text: "内衣",
              //icon: Icon(Icons.directions_bike),
            ),
            Tab(
              text: "数码",
              //icon: Icon(Icons.directions_bike),
            ),
            Tab(
              text: "特产",
              //icon: Icon(Icons.directions_bike),
            ),
          ],

        ),
      ),
      body: TabBarView(
        controller: _tabController, //注意，必须得加
        children: <Widget>[
          Center(
            child: Text("热销"), //内容
          ),
          Center(
            child: Text("内衣"), //内容
          ),
          Center(
            child: Text("数码"), //内容
          ),
          Center(
            child: Text("特产"), //内容
          ),
        ],
      ),
    );
  }
}


三、TabControllers实现顶部tab切换 - 生命周期

import 'package:flutter/material.dart';

void main() {
  runApp(sunApp());
}

/**
 * 自定义 Widget 组件
 * StatelessWidget 状态不可改变组件，抽象类，需要实现build方法
 * StatefulWidget 状态可改变组件
 */
class sunApp extends StatelessWidget{
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    //throw UnimplementedError();
    /**
     *  一般我们会使用 MaterialApp() 作为Flutter的一个根组件使用
     *  常用属性：
     *  home 主页
     *  title 标题
     *  color 颜色
     *  theme 主题
     *  routes 路由
     */
    return MaterialApp(
      home:Scaffold(
        //appBar 导航
        //body 主体
        body: sunHomeContent(),
      ),
      //theme 主体
      theme: ThemeData(
          primarySwatch: Colors.amber  //修改主体颜色
      ),
    );
  }
}

/**
 * StatelessWidget 无状态组件
 * StatefulWidget 有状态组件，点击页面脚本出发页面数据发生变化
 */
//说明：使用TabControllers实现顶部tab切换,必须使用动态组件,也就是 StatefulWiget
class sunHomeContent extends StatefulWidget{
  @override
  State<StatefulWidget> createState() {
    // TODO: implement createState
    //throw UnimplementedError();
    //这里不能直接返回组件，因为返回的数据类型是 State<StatefulWidget>
    return sunHomeContentState();
  }
}
/**
 * 必须集成 SingleTickerProviderStateMixin
 */
class sunHomeContentState extends State with SingleTickerProviderStateMixin{
  TabController _tabController;

  //dispose生命周期函数
  //dispose 当组件销毁时，触发的生命周期函数
  @override
  // ignore: must_call_super
  void dispose(){
    super.dispose();
    _tabController.dispose(); //把它自己销毁
  }

  //initState 当组件初始化时，触发的生命周期函数,初始化TabController
  @override
  void initState() {
    super.initState();
    _tabController = TabController(length: 4, vsync: this);
    //侦听
    _tabController.addListener(() {
      //打印选中项索引值
      var index = _tabController.index;
      print("Jessice:${index}");
    });
  }

  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    //throw UnimplementedError();
    return Scaffold(
      appBar: AppBar(
        title: Text("分类"),
        bottom: TabBar(
          controller: this._tabController, //注意，必须得加
          tabs: <Widget>[
            Tab(
              text: "热销", //关键词
              //icon: Icon(Icons.directions_bike), //图标
            ),
            Tab(
              text: "内衣",
              //icon: Icon(Icons.directions_bike),
            ),
            Tab(
              text: "数码",
              //icon: Icon(Icons.directions_bike),
            ),
            Tab(
              text: "特产",
              //icon: Icon(Icons.directions_bike),
            ),
          ],

        ),
      ),
      body: TabBarView(
        controller: _tabController, //注意，必须得加
        children: <Widget>[
          Center(
            child: Text("热销"), //内容
          ),
          Center(
            child: Text("内衣"), //内容
          ),
          Center(
            child: Text("数码"), //内容
          ),
          Center(
            child: Text("特产"), //内容
          ),
        ],
      ),
    );
  }
}


四、TabControllers实现顶部tab切换 - 多Tab不叠加,滑动展示

import 'package:flutter/material.dart';

void main() {
  runApp(sunApp());
}

/**
 * 自定义 Widget 组件
 * StatelessWidget 状态不可改变组件，抽象类，需要实现build方法
 * StatefulWidget 状态可改变组件
 */
class sunApp extends StatelessWidget{
  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    //throw UnimplementedError();
    /**
     *  一般我们会使用 MaterialApp() 作为Flutter的一个根组件使用
     *  常用属性：
     *  home 主页
     *  title 标题
     *  color 颜色
     *  theme 主题
     *  routes 路由
     */
    return MaterialApp(
      home:Scaffold(
        //appBar 导航
        //body 主体
        body: sunHomeContent(),
      ),
      //theme 主体
      theme: ThemeData(
          primarySwatch: Colors.amber  //修改主体颜色
      ),
    );
  }
}

/**
 * StatelessWidget 无状态组件
 * StatefulWidget 有状态组件，点击页面脚本出发页面数据发生变化
 */
//说明：使用TabControllers实现顶部tab切换,必须使用动态组件,也就是 StatefulWiget
class sunHomeContent extends StatefulWidget{
  @override
  State<StatefulWidget> createState() {
    // TODO: implement createState
    //throw UnimplementedError();
    //这里不能直接返回组件，因为返回的数据类型是 State<StatefulWidget>
    return sunHomeContentState();
  }
}
/**
 * 必须集成 SingleTickerProviderStateMixin
 */
class sunHomeContentState extends State with SingleTickerProviderStateMixin{
  TabController _tabController;

  //dispose生命周期函数
  //dispose 当组件销毁时，触发的生命周期函数
  @override
  // ignore: must_call_super
  void dispose(){
    super.dispose();
    _tabController.dispose(); //把它自己销毁
  }

  //initState 当组件初始化时，触发的生命周期函数,初始化TabController
  @override
  void initState() {
    super.initState();
    _tabController = TabController(length: 8, vsync: this);
    //侦听
    _tabController.addListener(() {
      //打印选中项索引值
      var index = _tabController.index;
      print("Jessice:${index}");
    });
  }

  @override
  Widget build(BuildContext context) {
    // TODO: implement build
    //throw UnimplementedError();
    return Scaffold(
      appBar: AppBar(
        title: Text("分类"),
        bottom: TabBar(
          isScrollable:true, //多Tab不叠加,滑动展示
          controller: this._tabController, //注意，必须得加
          tabs: <Widget>[
            Tab(
              text: "热销", //关键词
              //icon: Icon(Icons.directions_bike), //图标
            ),
            Tab(
              text: "内衣",
              //icon: Icon(Icons.directions_bike),
            ),
            Tab(
              text: "数码",
              //icon: Icon(Icons.directions_bike),
            ),
            Tab(
              text: "特产",
              //icon: Icon(Icons.directions_bike),
            ),
            Tab(
              text: "黄渤",
              //icon: Icon(Icons.directions_bike),
            ),
            Tab(
              text: "王迅",
              //icon: Icon(Icons.directions_bike),
            ),
            Tab(
              text: "罗志祥",
              //icon: Icon(Icons.directions_bike),
            ),
            Tab(
              text: "黄磊",
              //icon: Icon(Icons.directions_bike),
            ),
          ],

        ),
      ),
      body: TabBarView(
        controller: _tabController, //注意，必须得加
        children: <Widget>[
          Center(
            child: Text("热销"), //内容
          ),
          Center(
            child: Text("内衣"), //内容
          ),
          Center(
            child: Text("数码"), //内容
          ),
          Center(
            child: Text("特产"), //内容
          ),
          Center(
            child: Text("特产"), //内容
          ),
          Center(
            child: Text("特产"), //内容
          ),
          Center(
            child: Text("特产"), //内容
          ),
          Center(
            child: Text("特产"), //内容
          ),
        ],
      ),
    );
  }
}
