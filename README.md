# TCard

Tinder like cards.

[![GitHub stars](https://img.shields.io/github/stars/xrr2016/tcard)](https://github.com/xrr2016/tcard/stargazers) [![pub package](https://img.shields.io/pub/v/tcard.svg)](https://pub.dev/packages/tcard) ![Test](https://github.com/xrr2016/tcard/workflows/Test/badge.svg)

## Uasge

### Use normal widget

```dart
TCard(
  cards: [
    Container(color: Colors.blue),
    Container(color: Colors.yellow),
    Container(color: Colors.red),
  ],
)
```

<img src="./example/colors.gif" width="520"  style="width: 260px;" alt="colors">

### Use network image

```dart
List<String> images = [
  'https://gank.io/images/5ba77f3415b44f6c843af5e149443f94',
  'https://gank.io/images/02eb8ca3297f4931ab64b7ebd7b5b89c',
  'https://gank.io/images/31f92f7845f34f05bc10779a468c3c13',
  'https://gank.io/images/b0f73f9527694f44b523ff059d8a8841',
  'https://gank.io/images/1af9d69bc60242d7aa2e53125a4586ad',
];

List<Widget> cards = List.generate(
  images.length,
  (int index) {
    return Container(
      decoration: BoxDecoration(
        color: Colors.white,
        borderRadius: BorderRadius.circular(16.0),
        boxShadow: [
          BoxShadow(
            offset: Offset(0, 17),
            blurRadius: 23.0,
            spreadRadius: -13.0,
            color: Colors.black54,
          )
        ],
      ),
      child: ClipRRect(
        borderRadius: BorderRadius.circular(16.0),
        child: Image.network(
          images[index],
          fit: BoxFit.cover,
        ),
      ),
    );
  },
);

TCard(
  size: Size(400, 600),
  cards: cards,
);
```

![images](./example/images.gif)

Image from [gank.io](gank.io)

### Use a controller to control

```dart
class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  TCardController _controller = TCardController();

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            TCard(
              cards: cards,
              size: Size(360, 480),
              controller: _controller,
              onForward: (index, info) {
                print(index);
              },
              onBack: (index) {
                print(index);
              },
              onEnd: () {
                print('end');
              },
            ),
            SizedBox(
              height: 40,
            ),
            Row(
              mainAxisAlignment: MainAxisAlignment.spaceAround,
              children: <Widget>[
                OutlineButton(
                  onPressed: () {
                    print(_controller);
                    _controller.back();
                  },
                  child: Text('Back'),
                ),
                OutlineButton(
                  onPressed: () {
                    _controller.reset();
                  },
                  child: Text('Reset'),
                ),
                OutlineButton(
                  onPressed: () {
                    _controller.forward();
                  },
                  child: Text('Forward'),
                ),
              ],
            ),
          ],
        ),
      ),
    );
  }
}
```

![controller](./example/controller.gif)

### Determine the sliding direction

```dart
 TCard(
  cards: cards,
  size: Size(360, 480),
  controller: _controller,
  onForward: (index, info) {
    print(index);
    print(info.direction);
    if (info.direction == SwipDirection.Right) {
      print('like');
    } else {
      print('dislike');
    }
  },
  onBack: (index) {
    print(index);
  },
  onEnd: () {
    print('end');
  },
)
```

![like](./example/like.png)

## Property

| property   |       type        | default |        description         | required |
| :--------- | :---------------: | :-----: | :------------------------: | :------: |
| cards      |  `List<Widget>`   | `null`  |        Render cards        |  `true`  |
| size       |      `Size`       | `null`  |         Card size          | `false`  |
| controller | `TCardController` | `null`  |      Card controller       | `false`  |
| onForward  | `ForwardCallback` | `null`  | Forward animation callback | `false`  |
| onBack     |  `BackCallback`   | `null`  |  Back animation callback   | `false`  |
| onEnd      |   `EndCallback`   | `null`  |    Forward end callback    | `false`  |

## Contribute

1. Fork it (https://github.com/xrr2016/tcard.git)
2. Create your feature branch (git checkout -b feature/foo)
3. Commit your changes (git commit -am 'Add some foo')
4. Push to the branch (git push origin feature/foo)
5. Create a new Pull Request

## License

[MIT](./LICENSE)
