## swipeable-multi-def-headref
## Swipeable List

Swipable List are ListItems that swipe open and close.Handles default native behavior such as closing rows when other rows are opened.<br />

![Preview ios swipeable-multi-def-headref](https://raw.githubusercontent.com/GeekyAnts/NativeBase-KitchenSink/v2.2.0/screenshots/ios/list-swipe-multiple.gif)
![Preview android swipeable-multi-def-headref](https://raw.githubusercontent.com/GeekyAnts/NativeBase-KitchenSink/v2.2.0/screenshots/android/list-swipe-multiple.gif)

*Syntax*

<pre class="line-numbers"><code class="language-jsx">import React, { Component } from 'react';
import { ListView } from 'react-native';
import { Container, Header, Content, List, ListItem, Text, Icon, Button } from 'native-base';
import datas from './datas';
​export default class SwipeableListExample extends Component {
  constructor(props) {
    super(props);
    this.ds = new ListView.DataSource({ rowHasChanged: (r1, r2) => r1 !== r2 });
    this.state = {
      basic: true,
      listViewData: datas,
    };
  }
  deleteRow(secId, rowId, rowMap) {
    rowMap[`${secId}${rowId}`].props.closeRow();
    const newData = [...this.state.listViewData];
    newData.splice(rowId, 1);
    this.setState({ listViewData: newData });
  }
  render() {
    return (
      &lt;Container>
        &lt;Header />
        &lt;Content scrollEnabled={false}>
          &lt;List
            dataSource={this.ds.cloneWithRows(this.state.listViewData)}
            leftOpenValue={75}
            rightOpenValue={-75}
            renderRow={data =>
              &lt;ListItem>
                &lt;Text>{data}&lt;/Text>
              &lt;/ListItem>
            }
            renderLeftHiddenRow={data =>
              &lt;Button info onPress={() => alert(data)}>
                &lt;Icon active name="information-circle" />
              &lt;/Button>
            }
            right={
              &lt;Button danger onPress={_ => this.deleteRow(secId, rowId, rowMap)}>
                &lt;Icon active name="trash" />
              &lt;/Button>
            }
          />
        &lt;/Content>
      &lt;/Container>
    );
  }
}</code></pre><br />

**Configuration**

<table class="table table-bordered">
        <thead>
            <tr>
                <th>Property</th>
                <th>Default</th>
                <th>Option</th>
                <th width="50%">Description</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>dataSource</td>
                <td> - </td>
                <td> user defined object </td>
                <td>
                    data chunks to render iteratively
                </td>
            </tr>
            <tr>
                <td>renderRow</td>
                <td> - </td>
                <td> Function </td>
                <td>
                    Callback which takes a chunk of data from dataSource and returns as a body component, which is visible. 
                </td>
            </tr>
            <tr>
                <td>renderLeftHiddenRow</td>
                <td> - </td>
                <td> Function </td>
                <td>
                    Callback which takes a chunk of data from dataSource and returns as a left component, which is hidden.
                </td>
            </tr>
            <tr>
                <td>renderRighHiddenRow</td>
                <td> - </td>
                <td> Function </td>
                <td>
                    Callback which takes a chunk of data from dataSource and returns as a right component, which is hidden.
                </td>
            </tr>
            <tr>
                <td>leftOpenValue</td>
                <td> - </td>
                <td> number </td>
                <td>
                    TranslateX value for opening the row to the left (<i>Positive Value</i>)
                </td>
            </tr>
            <tr>
                <td>rightOpenValue</td>
                <td> - </td>
                <td> number </td>
                <td>
                    TranslateX value for opening the row to the right (<i>Negative Value</i>)
                </td>
            </tr>
            <tr>
                <td>closeOnRowBeginSwipe</td>
                <td> false </td>
                <td> boolean </td>
                <td>
                    Open row be closed as soon as a row begin to swipe open
                </td>
            </tr>
            <tr>
                <td>swipeToOpenPercent</td>
                <td> 50% </td>
                <td> % </td>
                <td>
                    Swipe percent of left/right component's width to trigger the row opening
                </td>
            </tr>
            <tr>
                <td>disableLeftSwipe</td>
                <td> false </td>
                <td> boolean </td>
                <td>
                    Disable ability to swipe the row left
                </td>
            </tr>
            <tr>
                <td>disableRightSwipe</td>
                <td> false </td>
                <td> boolean </td>
                <td>
                    Disable ability to swipe the row right
                </td>
            </tr>
            <tr>
                <td>onRowOpen, onRowClose</td>
                <td> - </td>
                <td> Function </td>
                <td>
                    Callback function which triggers when a swipe row is animating open/close
                </td>
            </tr>
            <tr>
                <td>onRowDidOpen, onRowDidClose</td>
                <td> - </td>
                <td> Function </td>
                <td>
                    Callback function which triggers when a swipe row has animated open/close
                </td>
            </tr>
        </tbody>
    </table><br />
<br />
**Known Issues :** Native behavior of closing row when List is scrolled doesn't work. <br />