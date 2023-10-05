### Q1
#### The code below can be copy pasted directly to [dartpad.dev](https://dartpad.dev)
```dart
import 'dart:math' as math;

void main() {
  List<dynamic> deck = ['SA', 'S2', 'S3', 'S4', 'S5', 'S6', 'S7', 'S8', 'S9', 'S10', 'SJ', 'SQ', 'SK',
                        'HA', 'H2', 'H3', 'H4', 'H5', 'H6', 'H7', 'H8', 'H9', 'H10', 'HJ', 'HQ', 'HK',
                        'CA', 'C2', 'C3', 'C4', 'C5', 'C6', 'C7', 'C8', 'C9', 'C10', 'CJ', 'CQ', 'CK',
                        'DA', 'D2', 'D3', 'D4', 'D5', 'D6', 'D7', 'D8', 'D9', 'D10', 'DJ', 'DQ', 'DK'];
  
  Map<String,dynamic> dealt = shuffleAndDealCards(deck);
  
  for(var hand in dealt.entries){
    print('${hand.key}: ${hand.value}');
  }
}

Map<String, dynamic> shuffleAndDealCards(List<dynamic> deck) {
  Map<String, dynamic> dealt = {'player1': [], 'player2': [], 'player3': [], 'player4': []};

  for (int i = 0; i < deck.length; i++) {
    int swapIndex = math.Random().nextInt(deck.length - i);
    var temp = deck[swapIndex];
    deck[swapIndex] = deck[i];
    deck[i] = temp;
  }

  int index = 0;
  for (var card in deck) {
    if (index % 4 == 0) dealt.update('player1', (hand) => hand + [card]);
    if (index % 4 == 1) dealt.update('player2', (hand) => hand + [card]);
    if (index % 4 == 2) dealt.update('player3', (hand) => hand + [card]);
    if (index % 4 == 3) dealt.update('player4', (hand) => hand + [card]);
    index++;
  }

  return dealt;
}
```

### Q2
Assuming the infinite scrolling page is written in Flutter using Dart:
1. When the page is opened, fetch the first set of paginated data.
2. Save the data in a `List<Map<String,dynamic>>` variable, lets call it `displayItems`.
3. Define a `ScrollController` for the `ListView` which will display the items. The `ScrollController` can be set up to run a `fetchNextPage` function when the user has scrolled to the end of the list. The function will fetch the next set of paginated data from the API provided.
4. Append the data returned from the fetchNextPage function to the `displayItems` list and call the `setState((){})` function.
5. Inside the `ListView` builder, we can get the index of the item from `displayItems` list and decide to show a video or image depending on the `mimeType` of the item data.
6. Create 2 new `Stateful Widgets`: `ImageItemWidget` and `VideoItemWidget`, which will be used to display image items and video items in the `ListView`. 
7. The `ImageItemWidget` can be set up so that a placeholder UI will be shown while the image is loading, then the image will fade in once it has loaded.
8. For the `VideoItemWidget`, if autoplay is required inside the `ListView` when the item is visible, a `VideoPlayerController` will be used to respond to events from the `ListView`'s `ScrollController` so that the video items can be paused or played depending on if it is visible on the screen.
