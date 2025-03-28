# Layout Constraints


> ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE**
> This attribute is supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.


## Required Permissions

None


## Attributes


  | Name | Type | Default Value | Description | 
| -------- | -------- | -------- | -------- |
| aspectRatio | number | - | Specifies an aspect ratio for the current component. | 
| displayPriority | number | - | Sets a display priority for the current component in the layout container. When the space of the parent container is insufficient, the component with a lower priority is hidden.<br/>> ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE**<br/>> This parameter is valid only for the Row/Column/Flex (single-row) container component. | 


## Example


```
@Entry
@Component
struct AspectRatioExample {
  private children : string[] = ['1', '2', '3', '4', '5', '6']

  build() {
    Column({space: 20}) {
      Text('using container: row').fontSize(14).fontColor(0xCCCCCC).width('100%')
      Row({space: 10}) {
        ForEach(this.children, (item) => {
          Text(item)
            .backgroundColor(0xbbb2cb)
            .fontSize(20)
            .aspectRatio(1.5)
            .height(60)
          Text(item)
            .backgroundColor(0xbbb2cb)
            .fontSize(20)
            .aspectRatio(1.5)
            .width(60)
        }, item=>item)
      }
      .size({width: "100%", height: 100})
      .backgroundColor(0xd2cab3)
      .clip(true)

      Text('using container: grid').fontSize(14).fontColor(0xCCCCCC).width('100%')
      Grid() {
        ForEach(this.children, (item) => {
          GridItem() {
            Text(item)
              .backgroundColor(0xbbb2cb)
              .fontSize(40)
              .aspectRatio(1.5)
          }
        }, item=>item)
      }
      .columnsTemplate('1fr 1fr 1fr')
      .columnsGap(10)
      .rowsGap(10)
      .size({width: "100%", height: 165})
      .backgroundColor(0xd2cab3)
    }.padding(10)
  }
}
```

  **Figure1** Portrait display
  ![en-us_image_0000001256978379](figures/en-us_image_0000001256978379.gif)

  **Figure2** Landscape display
  ![en-us_image_0000001212218476](figures/en-us_image_0000001212218476.gif)


```
class ContainerInfo {
  label : string = ''
  size : string = ''
}

class ChildInfo {
  text : string = ''
  priority : number = 0
}

@Entry
@Component
struct DisplayPriorityExample {
  private container : ContainerInfo[] = [
    {label: 'Big container', size: '90%'},
    {label: 'Middle container', size: '50%'},
    {label: 'Small container', size: '30%'}]
  private children : ChildInfo[] = [
    {text: '1\n(priority:2)', priority: 2},
    {text: '2\n(priority:1)', priority: 1},
    {text: '3\n(priority:3)', priority: 3},
    {text: '4\n(priority:1)', priority: 1},
    {text: '5\n(priority:2)', priority: 2}]
  @State currentIndex : number = 0

  build() {
    Column({space: 10}) {
      Button(this.container[this.currentIndex].label).backgroundColor(0x317aff)
        .onClick((event: ClickEvent) => {
          this.currentIndex = (this.currentIndex + 1) % this.container.length
        })
      Flex({justifyContent: FlexAlign.SpaceBetween}) {
        ForEach(this.children, (item)=>{
          Text(item.text)
            .width(120)
            .height(60)
            .fontSize(24)
            .textAlign(TextAlign.Center)
            .backgroundColor(0xbbb2cb)
            .displayPriority(item.priority)
        }, item=>item.text)
      }
      .width(this.container[this.currentIndex].size)
      .backgroundColor(0xd2cab3)
    }.width("100%").margin({top:50})
  }
}

```

![en-us_image_0000001212058504](figures/en-us_image_0000001212058504.gif)
