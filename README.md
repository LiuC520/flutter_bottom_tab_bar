# bottom_tab_bar

 bottom_tab_bar, the same to bottom_navigation_bar, but add some new features.

##
![bottomtabbar](/screenshot.png)

For help getting started with Flutter, view our online [documentation](https://flutter.io/).

For help on editing package code, view the [documentation](https://flutter.io/developing-packages/).

### items : ```List<BottomTabBarItem>```
The interactive items laid out within the bottom navigation bar where each item has an icon and title.



###  onTap  : ```ValueChanged<int>```

The callback that is called when a item is tapped.

 The widget creating the bottom navigation bar needs to keep track of the current index and call `setState` to rebuild it with the newly provided index.

###  currentIndex  : ```int```
 The index into [items] of the current active item.


 ### type  : ```BottomTabBarType ```
Defines the layout and behavior of a [BottomTabBar].

 See documentation for [BottomTabBarType] for information on the meaning of different types.


 ### fixedColor  : ```Color ```
The color of the selected item when bottom navigation bar is [BottomTabBarType.fixed].

If [fixedColor] is null then the theme's primary color, [ThemeData.primaryColor], is used. However if [BottomTabBar.type] is [BottomTabBarType.shifting] then [fixedColor] is ignored.

### iconSize : ```double```
 The size of all of the [BottomTabBarItem] icons.

See [BottomTabBarItem.icon] for more information.


### [new] isAnimation : ```bool```
 Is animation avilable, default true final bool isAnimation;

### [new]  badgeColor : ```Color```
badge color, default is fixedColor

### [new]  isInkResponse : ```bool```
 Is InkResponse avilable, default true

### [new]  badge : ```Widget```
the Badge ,used for unread message ...

### [new]  badgeNo : ```String```
the Badge number , unread message ...


## How to Use?

first import dependeny in pubspec.yaml

```
dependencies:
  flutter:
    sdk: flutter
  bottom_tab_bar:
    git: https://github.com/LiuC520/flutter_bottom_tab_bar.git

```

example:

```

class HomeState extends State<Home> with SingleTickerProviderStateMixin {
  TabController _tabController;
  int _selectedIndex = 1;
  String badgeNo1;
  var titles = ['home', 'video', 'find', 'smallvideo', 'my'];
  var icons = [
    Icons.home,
    Icons.play_arrow,
    Icons.child_friendly,
    Icons.fiber_new,
    Icons.mic_none
  ];
  @override
  void initState() {
    super.initState();
    _tabController =
        new TabController(vsync: this, initialIndex: 1, length: titles.length);
    badgeNo1 = '12';
  }

  void _onItemSelected(int index) {
    setState(() {
      _selectedIndex = index;
      badgeNo1 = '';
    });
  }

  final _widgetOptions = [
    Text('Index 0: Home'),
    Text('Index 1: Video'),
    Text('Index 2: find someone'),
    Text('Index 3: small Video'),
    Text('Index 4: My'),
  ];
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Bottom Tab Bar'),
        actions: <Widget>[new Icon(Icons.photo_camera)],
      ),
      bottomNavigationBar: BottomTabBar(
        items: <BottomTabBarItem>[
          BottomTabBarItem(
              icon: Icon(icons[0]), title: Text(titles[0]), badgeNo: badgeNo1),
          BottomTabBarItem(icon: Icon(icons[1]), title: Text(titles[1])),
          BottomTabBarItem(icon: Icon(icons[2]), title: Text(titles[2])),
          BottomTabBarItem(
              icon: Icon(icons[3]),
              activeIcon: Icon(icons[3]),
              title: Text(titles[3])),
          BottomTabBarItem(icon: Icon(icons[4]), title: Text(titles[4])),
        ],
        fixedColor: Colors.blue,
        currentIndex: _selectedIndex,
        onTap: _onItemSelected,
        type: BottomTabBarType.fixed,
        isAnimation: false,
        isInkResponse: false,
        badgeColor: Colors.green,
      ),
      body: Center(
        child: _widgetOptions.elementAt(_selectedIndex),
      ),
    );
  }
}

```
