### Q1
```dart
Map<String, dynamic> shuffleAndDealCards(List<dynamic> deck){
	Map<String,dynamic> dealt = {'player1':[],'player2':[],'player3':[],'player4':[]};
	deck.shuffle(); //use the shuffle method from the List class in dart
	int index = 0;
	for(var card in deck){
		if(index%1==0) dealt.update('player1', (hand) => hand.add(card));
		if(index%2==0) dealt.update('player2', (hand) => hand.add(card));
		if(index%3==0) dealt.update('player3', (hand) => hand.add(card));
		if(index%4==0) dealt.update('player4', (hand) => hand.add(card));
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
