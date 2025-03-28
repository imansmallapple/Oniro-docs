# TabContent


> ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE**
> This component is supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.


The **&lt;TabContent&gt;** component is used only in the **&lt;Tabs&gt;** component. It corresponds to the content view of a switched tab page.


## Required Permissions

None


## Child Components

This component supports only one child component.


## APIs

TabContent()


## Attributes

Touch target configuration is not supported.

| Name | Type | Default Value | Description |
| -------- | -------- | -------- | -------- |
| tabBar | string \| {<br/>icon?: string,<br/>text?: string<br/>}<br/>\| [CustomBuilder](../../ui/ts-types.md)<sup>8+</sup> | - | Content displayed on the tab bar.<br/>**CustomBuilder**: builder, to which components can be passed (applicable to API version 8 and later versions).<br/>> ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE**<br/>> If an icon uses an SVG image, the width and height attributes of the SVG image must be deleted. Otherwise, the icon size will be determined by the width and height attributes of the SVG image. |

> ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE**
> - The **&lt;TabContent&gt;** component does not support setting of the common width attribute. By default, its width is the same as that of the parent **&lt;Tabs&gt;** component.
> 
> - The **&lt;TabContent&gt;** component does not support setting of the common height attribute. Its height is determined by the height of the parent **&lt;Tabs&gt;** component and the **&lt;TabBar&gt;** component.


## Example


```
@Entry
@Component
struct TabContentExample  {
  @State fontColor: string = 'rgba(0, 0, 0, 0.4)'
  @State selectedFontColor: string = 'rgba(10, 30, 255, 1)'
  @State currentIndex: number = 0
  private controller: TabsController = new TabsController()
  @Builder TabBuilder(index: number) {
    Column() {
      Image(this.currentIndex === index ? '/resources/ic_public_contacts_filled_selected.png' : '/resources/ic_public_contacts_filled.png')
        .width(10)
        .height(10)
        .opacity(this.currentIndex === index ? 1 : 0.4)
        .objectFit(ImageFit.Contain)
      Text(`Tab${(index > 2 ? (index - 1) : index) + 1}`)
        .fontColor(this.currentIndex === index ? this.selectedFontColor : this.fontColor)
        .fontSize(10)
        .margin({top: 2})
    }
  }

  @Builder AddBuilder() {
    Column() {
      Image(this.currentIndex === 2 ? '/resources/ic_public_add_norm_filled_selected.png' : '/resources/ic_public_add_norm_filled.png')
        .width(this.currentIndex === 2 ? 26 : 24)
        .height(this.currentIndex === 2 ? 26 : 24)
        .opacity(this.currentIndex === 2 ? 1 : 0.4)
        .objectFit(ImageFit.Contain)
        .animation({duration: 200})
    }
  }

  build() {
    Column() {
      Tabs({ barPosition: BarPosition.End, controller: this.controller }) {
        TabContent() {
          Flex({justifyContent: FlexAlign.Center}) {
            Text('Tab1').fontSize(32)
          }
        }.tabBar(this.TabBuilder(0))

        TabContent() {
          Flex({justifyContent: FlexAlign.Center}) {
            Text('Tab2').fontSize(32)
          }
        }.tabBar(this.TabBuilder(1))

        TabContent() {
          Flex({justifyContent: FlexAlign.Center}) {
            Text('Add').fontSize(32)
          }
        }.tabBar(this.AddBuilder())

        TabContent() {
          Flex({justifyContent: FlexAlign.Center}) {
            Text('Tab3').fontSize(32)
          }
        }.tabBar(this.TabBuilder(3))

        TabContent() {
          Flex({justifyContent: FlexAlign.Center}) {
            Text('Tab4').fontSize(32)
          }
        }.tabBar(this.TabBuilder(4))
      }
      .vertical(false)
      .barWidth(300).barHeight(56)
      .onChange((index: number) => {
        this.currentIndex = index
      })
      .width('90%').backgroundColor('rgba(241, 243, 245, 0.95)')
    }.width('100%').height(200).margin({ top: 5 })
  }
}
```

![en-us_image_0000001256978331](figures/en-us_image_0000001256978331.gif)
