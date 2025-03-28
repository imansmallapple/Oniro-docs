# Navigation


> ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE**
> This component is supported since API version 8. Updates will be marked with a superscript to indicate their earliest API version.


The **&lt;Navigation&gt;** component typically functions as the root container of a page and displays the page title, toolbar, and menu based on the attribute settings.


## Required Permissions

None


## Child Components

Supported


## APIs

Navigation()

Creates a component that can automatically display the navigation bar, title, and toolbar based on the attribute settings.


## Attributes

| Name | Type | Default Value | Description |
| -------- | -------- | -------- | -------- |
| title | string \| [CustomBuilder](../../ui/ts-types.md)<sup>8+</sup> | - | Page title. |
| subtitle | string | - | Subtitle of the page. |
| menus | Array&lt;NavigationMenuItem&gt; \| [CustomBuilder](../../ui/ts-types.md)<sup>8+</sup> | - | Menu in the upper right corner of the page. |
| titleMode | NavigationTitleMode | NavigationTitleMode.Free | Display mode of the page title bar. |
| toolBar | {<br/>items:[<br/>Object<br/>] }<br/>\| [CustomBuilder](../../ui/ts-types.md)<sup>8+</sup> | - | Content of the toolbar.<br/>**items**: all items on the toolbar. |
| hideToolBar | boolean | false | Whether to hide the toolbar.<br/>**true**: Hide the toolbar.<br/>**false**: Show the toolbar. |
| hideTitleBar | boolean | false | Whether to hide the title bar. |
| hideBackButton | boolean | false | Whether to hide the back button. |

- NavigationMenuItem attributes
    | Name | Type | Mandatory | Default Value | Description |
  | -------- | -------- | -------- | -------- | -------- |
  | value | string | Yes | - | Text of an option on the menu bar. |
  | icon | string | No | - | Icon path of an option on the menu bar. |
  | action | () =&gt; void | No | - | Callback invoked when an option is selected. |

- Object attributes
    | Name | Type | Mandatory | Default Value | Description |
  | -------- | -------- | -------- | -------- | -------- |
  | value | string | Yes | - | Text of an option on the toolbar. |
  | icon | string | No | - | Icon path of an option on the toolbar. |
  | action | () =&gt; void | No | - | Callback invoked when an option is selected. |

- NavigationTitleMode enums
    | Name | Description |
  | -------- | -------- |
  | Free | When the content is a scrollable component, the title shrinks as the content scrolls up (the subtitle fades out with its size remaining unchanged) and restores as the content scrolls down. |
  | Mini | The mode is fixed at mini mode (icon + main title and subtitle). |
  | Full | The mode is fixed at full mode (main title and subtitle). |

  > ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE**
  > Currently, only the scrollable component **&lt;List&gt;** is supported.


## Events

| Name | Description |
| -------- | -------- |
| onTitleModeChange(callback:&nbsp;(titleMode:&nbsp;NavigationTitleMode)&nbsp;=&gt;&nbsp;void) | Triggered when **titleMode** is set to **NavigationTitleMode.Free** and the title bar mode changes as content scrolls. |


## Example


```
// Example 01
@Entry
@Component
struct NavigationExample {
  private arr: number[] = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
  @State hideBar: boolean = true

  @Builder NavigationTitle() {
    Column() {
      Text('title')
        .width(80)
        .height(60)
        .fontColor(Color.Blue)
        .fontSize(30)
    }
    .onClick(() => {
      console.log("title")
    })
  }

  @Builder NavigationMenus() {
    Row() {
      Image('images/add.png')
        .width(25)
        .height(25)
      Image('comment/more.png')
        .width(25)
        .height(25)
        .margin({ left: 30 })
    }.width(100)
  }

  build() {
    Column() {
      Navigation() {
        Search({ value: '', placeholder: "" }).width('85%').margin(26)
        List({ space: 5, initialIndex: 0 }) {
          ForEach(this.arr, (item) => {
            ListItem() {
              Text('' + item)
                .width('90%')
                .height(80)
                .backgroundColor('#3366CC')
                .borderRadius(15)
                .fontSize(16)
                .textAlign(TextAlign.Center)
            }.editable(true)
          }, item => item)
        }
        .listDirection(Axis.Vertical)
        .height(300)
        .margin({ top: 10, left: 18 })
        .width('100%')

        Button(this.hideBar ? "tool bar" : "hide bar")
          .onClick(() => {
            this.hideBar = !this.hideBar
          })
          .margin({ left: 135, top: 60 })
      }
      .title(this.NavigationTitle)
      .subTitle('subtitle')
      .menus(this.NavigationMenus)
      .titleMode(NavigationTitleMode.Free)
      .hideTitleBar(false)
      .hideBackButton(false)
      .onTitleModeChange((titleModel: NavigationTitleMode) => {
        console.log('titleMode')
      })
      .toolBar({ items: [
        { value: 'app', icon: 'images/grid.svg', action: () => {
          console.log("app")
        } },
        { value: 'add', icon: 'images/add.svg', action: () => {
          console.log("add")
        } },
        { value: 'collect', icon: 'images/collect.svg', action: () => {
          console.log("collect")
        } }] })
      .hideToolBar(this.hideBar)
    }
  }
}
```

![en-us_image_0000001256978359](figures/en-us_image_0000001256978359.gif)


```
// Example 02
@Entry
@Component
struct ToolbarBuilderExample {
  @State currentIndex: number = 0
  @State Build: Array<Object> = [
    {
      icon: $r('app.media.ic_public_add'),
      icon_after: $r('app.media.ic_public_addcolor'),
      text: 'add',
      num: 0
    },
    {
      icon: $r('app.media.ic_public_app'),
      icon_after: $r('app.media.ic_public_appcolor'),
      text: 'app',
      num: 1
    },
    {
      icon: $r('app.media.ic_public_collect'),
      icon_after: $r('app.media.ic_public_collectcolor'),
      text: 'collect',
      num: 2
    }
  ]

  @Builder NavigationToolbar() {
    Row() {
      ForEach(this.Build, item => {
        Column() {
          Image(this.currentIndex == item.num ? item.icon_after : item.icon)
            .width(25)
            .height(25)
          Text(item.text)
            .fontColor(this.currentIndex == item.num ? "#ff7500" : "#000000")
        }
        .onClick(() => {
          this.currentIndex = item.num
        })
        .margin({ left: 70 })
      })
    }
  }

  build() {
    Column() {
      Navigation() {
        Flex() {
        }
      }
      .toolBar(this.NavigationToolbar)
    }
  }
}
```

![en-us_image_0000001212058484](figures/en-us_image_0000001212058484.gif)
