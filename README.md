
# react-native-recyclerview-list

A RecyclerView implementation for ReactNative. Only for Android.

## Getting started

`$ npm install react-native-recyclerview-list --save`

### Mostly automatic installation

`$ react-native link react-native-recyclerview-list`

### Manual installation


#### Android

1. Open up `android/app/src/main/java/[...]/MainActivity.java`
  - Add `import com.github.godness84.RNRecyclerViewList.RNRecyclerviewListPackage;` to the imports at the top of the file
  - Add `new RNRecyclerviewListPackage()` to the list returned by the `getPackages()` method
2. Append the following lines to `android/settings.gradle`:
  	```
  	include ':react-native-recyclerview-list'
  	project(':react-native-recyclerview-list').projectDir = new File(rootProject.projectDir, 	'../node_modules/react-native-recyclerview-list/android')
  	```
3. Insert the following lines inside the dependencies block in `android/app/build.gradle`:
  	```
      compile project(':react-native-recyclerview-list')
  	```


## Usage
```javascript
import RecyclerviewList, { DataSource } from 'react-native-recyclerview-list';

// Take an array as data
var rawdata = [
  { id: 1, text: 'Item #1' },
  { id: 2, text: 'Item #2' },
  { id: 3, text: 'Item #3' },
  { id: 4, text: 'Item #4' },
  { id: 5, text: 'Item #5' }
];

// Wrap your data in a DataSource.
// The second argument is the 'keyExtractor' function that returns the unique key of the item.
var dataSource = new DataSource(rawdata, (item, index) => item.id);    

...

// Render the list
render() {
  return (
    <RecyclerviewList
      style={{ flex: 1 }}
      dataSource={dataSource}
      renderItem={({item, index}) => (
        <Text>{item.text} - {index}</Text>
      )} />
  );
}   
```

# Props

Prop name             | Description   | Type      | Default value
----------------------|---------------|-----------|--------------
`style`               | Style for the list | object | {}
`dataSource`          | The datasource that contains the data to render | DataSource | none
`windowSize`          | Number of items to render at the top (and bottom) of the visible items | int | 30
`initialListSize`     | Number of items to render at startup. | int | 10
`initialScrollIndex`  | Index of the item to scroll at startup | int | none
`itemAnimatorEnabled` | Whether animates items when they are added or removed | boolean | true
`ListHeaderComponent` | Component to render as header | component | none
`ListFooterComponent` | Component to render as footer | component | none
`ListEmptyComponent`  | Component to render in case of no items | component | none
`ItemSeparatorComponent`  | Component to render as item separator | component | none
`onVisibleItemsChange`    | Called when the first and last index of the visible items change | function | none
`onScroll`                | Called when the list is scrolling | function | none
`onScrollBeginDrag`       | Called when the user starts scrolling | function | none
`onScrollEndDrag`         | Called when the user stops dragging | function | none

# Methods

Method name           | Params                          | Description
----------------------|---------------------------------|------------
`scrollToIndex`       | `{ index, animated, velocity }` | Scroll the list to the `index`ed item. It can be `animated`. `velocity` is the amount of pixels per inch.
`scrollToEnd`         | `{ animated, velocity }` | Scroll to the end of the list. It can be `animated`. `velocity` is the amount of pixels per inch.

# DataSource

It wraps your array, giving you some useful methods to update the data.

## Methods

Method name           | Params                          | Description
----------------------|---------------------------------|------------
`push`                | item                            | Add an item to the end of the array
`unshift`             | item                            | Add an item to the beginning of the array
`splice`              | index, deleteCount, ...items    | Equals to `Array.prototype.splice`
`set`                 | index, item                     | Set the item at the specified index
`get`                 | index                           | Returns the item at the specified index
`size`                |                                 | Returns the length of the array




  
