# Menu

> ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE**
> The APIs of this module are supported since API version 8. Updates will be marked with a superscript to indicate their earliest API version.

## ContextMenu.close

close(): void

Closes the menu bound to this component through [bindContextMenu](./ts-universal-attributes-menu.md#Atrributes) on a page.

- Example
  ```
  @Entry
  @Component
  struct Index {
    @Builder MenuBuilder(){
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Text('close')
          .fontSize(30)
          .fontWeight(FontWeight.Bold)
          .onClick(() => {
            ContextMenu.close();
          })
      }.height(400)
      .backgroundColor(Color.Pink)
  
    }
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Start, justifyContent: FlexAlign.Start }) {
        Column(){
          Text("Text")
        }.bindContextMenu(this.MenuBuilder, ResponseType.LongPress)
      }
      .width('100%')
      .height('100%')
    }
  }
  ```
