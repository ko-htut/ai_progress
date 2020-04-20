# example

aai_progress: [![pub package](https://img.shields.io/pub/v/ai_progress.svg)](https://pub.dev/packages/ai_progress) example

## Effect

|iOS-ai_progress|Android-ai_progress|
|:-|:-|
|![ios](https://github.com/pdliuw/ai_progress/blob/master/example/gif/ai_progress_ios.gif)|![android](https://github.com/pdliuw/ai_barcode/blob/master/example/gif/ai_progress_android.gif)|
|:-|:-|

|macOS-ai_progress|Web-ai_progress|
|:-|:-|
|![macOS](https://github.com/pdliuw/ai_barcode/blob/master/example/gif/ai_progress_macOS.gif)|![web](https://github.com/pdliuw/ai_barcode/blob/master/example/gif/ai_progress_web.gif)|
|:-|:-|


## Code

```
    
   import 'dart:ui';
   
   import 'package:ai_progress/ai_progress.dart';
   import 'package:flutter/cupertino.dart';
   import 'package:flutter/material.dart';
   
   void main() {
     runApp(MyApp());
   }
   
   class MyApp extends StatelessWidget {
     // This widget is the root of your application.
     @override
     Widget build(BuildContext context) {
       return MaterialApp(
         title: 'Flutter Demo',
         theme: ThemeData(
           primarySwatch: Colors.blue,
           visualDensity: VisualDensity.adaptivePlatformDensity,
         ),
         home: HomePage(),
       );
     }
   }
   
   class HomePage extends StatelessWidget {
     @override
     Widget build(BuildContext context) {
       return Column(
         children: [
           Expanded(
             flex: 1,
             child: MyHomePage(title: 'Flutter Demo Home Page'),
           ),
         ],
       );
     }
   }
   
   class MyHomePage extends StatefulWidget {
     MyHomePage({Key key, this.title}) : super(key: key);
   
     final String title;
   
     @override
     _MyHomePageState createState() => _MyHomePageState();
   }
   
   class _MyHomePageState extends State<MyHomePage>
       with SingleTickerProviderStateMixin {
     int _counter = 0;
   
     static const double MAX = 10.0;
     static const double MIN = 1.0;
     static int _divisions = 99;
   
     double _progressValue = 1;
     double _slideValue = MAX;
   
     AnimationController _controller;
     Animation<Color> _colorTween;
   
     @override
     void initState() {
       super.initState();
       _controller = AnimationController(vsync: this);
       _colorTween = _controller.drive(ColorTween(
         begin: Colors.grey,
         end: Colors.green,
       ));
       _controller.value = _progressValue;
     }
   
     @override
     void dispose() {
       super.dispose();
       _controller.dispose();
       Paint paint = Paint();
   
       paint..isAntiAlias = true;
     }
   
     Map<int, Widget> _segmentChildren = {
       1: Text("1"),
       2: Text("2"),
       3: Text("3"),
       4: Text("4"),
       5: Text("5"),
       6: Text("6"),
       7: Text("7"),
       8: Text("8"),
       9: Text("9"),
       10: Text("10"),
     };
     int _segmentValue = 1;
   
     @override
     Widget build(BuildContext context) {
       return Scaffold(
         appBar: AppBar(
           title: Text(widget.title),
         ),
         body: SingleChildScrollView(
           child: Column(
             children: [
               Row(
                 children: [
                   Expanded(
                     child: CupertinoSegmentedControl(
                       padding: EdgeInsets.all(5),
                       children: _segmentChildren,
                       onValueChanged: (int index) {
                         setState(() {
                           _segmentValue = index;
                           _controller.value = index * 10 / 100;
                         });
                       },
                       groupValue: _segmentValue,
                     ),
                   ),
                 ],
               ),
               Align(
                 child: Text("$_segmentValue"),
               ),
               Slider(
                 min: MIN,
                 max: MAX,
                 value: _segmentValue.toDouble(),
                 onChanged: (double newValue) {
                   setState(() {
                     _segmentValue = newValue.toInt();
                     _controller.value = newValue;
                   });
                 },
               ),
               Row(
                 children: [
                   Spacer(),
                   Stack(
                     alignment: Alignment.center,
                     children: <Widget>[
                       Container(
                         width: 150,
                         height: 150,
                         padding: EdgeInsets.all(5),
                         child: CircularProgressIndicator(
                           value: _segmentValue / 10,
                           strokeWidth: 10.0,
                           valueColor: _colorTween,
                         ),
                       ),
                       Text("${_segmentValue / 10 * 100}%"),
                     ],
                   ),
                   Spacer(),
                   Stack(
                     alignment: Alignment.center,
                     children: <Widget>[
                       Container(
                         width: 150,
                         height: 150,
                         padding: EdgeInsets.all(5),
                         child: AirDashboardStateProgressIndicator(
                           size: Size(150, 150),
                           value: _segmentValue / 10 * 100, //1~100
                           valueColor:
                               ColorTween(begin: Colors.grey, end: Colors.blue)
                                   .transform(_segmentValue / 10),
                           pathStrokeWidth: 10,
                           valueStrokeWidth: 10,
                           gapDegree: 60,
                           roundCap: true,
                         ),
                       ),
                       Text("${_segmentValue / 10 * 100}%"),
                     ],
                   ),
                   Spacer(),
                 ],
               ),
               //圆环、扇形样式的进度
               Row(
                 children: [
                   Spacer(),
                   Stack(
                     alignment: Alignment.center,
                     children: <Widget>[
                       Container(
                         width: 150,
                         height: 150,
                         padding: EdgeInsets.all(5),
                         child: AirCircularStateProgressIndicator(
                           size: Size(150, 150),
                           value: _segmentValue / 10 * 100, //1~100
                           pathColor: Colors.white,
                           valueColor:
                               ColorTween(begin: Colors.grey, end: Colors.blue)
                                   .transform(_segmentValue / 10),
                           pathStrokeWidth: 10.0,
                           valueStrokeWidth: 10.0,
                           useCenter: false,
                           filled: false,
                           roundCap: true,
                         ),
                       ),
                       Text("${_segmentValue / 10 * 100}%"),
                     ],
                   ),
                   Spacer(),
                   Stack(
                     alignment: Alignment.center,
                     children: <Widget>[
                       Container(
                         width: 150,
                         height: 150,
                         padding: EdgeInsets.all(5),
                         child: AirCircularStateProgressIndicator(
                           size: Size(150, 150),
                           value: _segmentValue / 10 * 100, //1~100
                           pathColor: Colors.white,
                           valueColor:
                               ColorTween(begin: Colors.grey, end: Colors.blue)
                                   .transform(_segmentValue / 10),
                           pathStrokeWidth: 10.0,
                           valueStrokeWidth: 10.0,
                           useCenter: true,
                           filled: true,
                           roundCap: true,
                         ),
                       ),
                       Text("${_segmentValue / 10 * 100}%"),
                     ],
                   ),
                   Spacer(),
                 ],
               ),
               //无进度值的加载
               CircularProgressIndicator(),
               //线性、步进样式的进度
               Row(
                 children: [
                   Spacer(),
                   Stack(
                     alignment: Alignment.center,
                     children: <Widget>[
                       Container(
                         width: 150,
                         height: 50,
                         padding: EdgeInsets.all(5),
                         child: AirLinearStateProgressIndicator(
                           size: Size(150, 150),
                           value: _segmentValue / 10 * 100, //1~100
                           valueColor:
                               ColorTween(begin: Colors.grey, end: Colors.blue)
                                   .transform(_segmentValue / 10),
                           pathStrokeWidth: 10.0,
                           valueStrokeWidth: 10.0,
                           roundCap: true,
                         ),
                       ),
                       Text("${_segmentValue / 10 * 100}%"),
                     ],
                   ),
                   Spacer(),
                   Row(
                     children: [
                       Container(
                         width: 90,
                         height: 10,
                         padding: EdgeInsets.all(0),
                         child: AirStepStateProgressIndicator(
                           size: Size(150, 150),
                           stepCount: _segmentChildren.length,
                           stepValue: _segmentValue,
                           valueColor:
                               ColorTween(begin: Colors.grey, end: Colors.blue)
                                   .transform(_segmentValue / 10),
                           pathStrokeWidth: 10.0,
                           valueStrokeWidth: 10.0,
                         ),
                       ),
                       Text("${_segmentValue / 10 * 100}%"),
                     ],
                   ),
                   Spacer(),
                 ],
               ),
               //Step progress round and square cap
               Column(
                 crossAxisAlignment: CrossAxisAlignment.center,
                 children: [
                   Row(
                     mainAxisAlignment: MainAxisAlignment.center,
                     children: [
                       Container(
                         width: 220,
                         height: 30,
                         padding: EdgeInsets.all(0),
                         child: AirStepStateProgressIndicator(
                           size: Size(150, 150),
                           stepCount: _segmentChildren.length,
                           stepValue: _segmentValue,
                           valueColor:
                               ColorTween(begin: Colors.grey, end: Colors.blue)
                                   .transform(_segmentValue / 10),
                           pathStrokeWidth: 30.0,
                           valueStrokeWidth: 30.0,
                         ),
                       ),
                       Text("${_segmentValue / 10 * 100}%"),
                     ],
                   ),
                   Divider(),
                   Row(
                     mainAxisAlignment: MainAxisAlignment.center,
                     children: [
                       Container(
                         clipBehavior: Clip.antiAlias,
                         decoration: ShapeDecoration(
                           shape: RoundedRectangleBorder(
                               borderRadius: BorderRadius.only(
                             topLeft: Radius.circular(45),
                             bottomLeft: Radius.circular(45),
                             topRight: Radius.circular(45),
                             bottomRight: Radius.circular(45),
                           )),
                         ),
                         width: 220,
                         height: 30.0,
                         child: AirStepStateProgressIndicator(
                           size: Size(150, 220),
                           stepCount: _segmentChildren.length,
                           stepValue: _segmentValue,
                           valueColor:
                               ColorTween(begin: Colors.grey, end: Colors.blue)
                                   .transform(_segmentValue / 10),
                           pathStrokeWidth: 30.0,
                           valueStrokeWidth: 30.0,
                         ),
                       ),
                       Text("${_segmentValue / 10 * 100}%"),
                     ],
                   ),
                 ],
               ),
               Divider(),
               //linear square progress
               Row(
                 mainAxisAlignment: MainAxisAlignment.center,
                 children: <Widget>[
                   Container(
                     width: 150,
                     padding: EdgeInsets.all(5),
                     child: LinearProgressIndicator(
                       value: _segmentValue / 10,
                       valueColor: _colorTween,
                     ),
                   ),
                   Text("${_segmentValue / 10 * 100}%"),
                 ],
               ),
             ],
           ),
         ),
       );
     }
   }


```