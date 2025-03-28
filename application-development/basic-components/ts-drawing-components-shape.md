# Shape


> ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE**
> This component is supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.


The **&lt;Shape&gt;** component is the parent component of the drawing components. The attributes described in this topic are universal attributes supported by all the drawing components.


1. The drawing components use **&lt;Shape&gt;** as the parent component to implement the effect similar to SVG.


2. The **&lt;Shape&gt;** component is used independently to draw a specific shape.


## Required Permissions

None


## Child Components

The **&lt;Shape&gt;** component can contain child components.


## APIs

Shape(value:{target?: PixelMap})

- Parameters
    | Name | Type | Mandatory | Default Value | Description | 
  | -------- | -------- | -------- | -------- | -------- |
  | target | PixelMap | No | null | Shape to draw. You can draw a shape in the specified **PixelMap** object. If no object is specified, the shape is drawn in the current drawing target. | 


## Attributes

  | Name | Type | Default Value | Mandatory | Description | 
| -------- | -------- | -------- | -------- | -------- |
| viewPort | {<br/>x: Length,<br/>y: Length,<br/>width: Length,<br/>height: Length<br/>} | - | Yes | View port of the shape. | 
| fill | Color | Black | No | Fill color. | 
| stroke | Color | - | No | Stroke color. | 
| strokeDashArray | Array&lt;Length&gt; | [] | No | Stroke dash. | 
| strokeDashOffset | Length | 0 | No | Offset of the start point for drawing the stroke. | 
| strokeLineCap | LineCapStyle | LineCapStyle.Butt | No | Cap style of the stroke. | 
| strokeLineJoin | LineJoinStyle | LineJoinStyle.Miter | No | Join style of the stroke. | 
| strokeMiterLimit | number | 4 | No | Limit value when the sharp angle is drawn as a miter. | 
| strokeOpacity | number | 1 | No | Stroke opacity. | 
| strokeWidth | Length | 1 | No | Stroke width. | 
| antiAlias | boolean | true | No | Whether anti-aliasing is enabled. | 

- LineJoinStyle enums
    | Name | Description | 
  | -------- | -------- |
  | Bevel | Bevel is used to connect paths. | 
  | Miter | Miter is used to connect paths. | 
  | Round | Round is used to connect paths. | 


## Example

  
```
@Entry
@Component
struct ShapeExample {
  build() {
    Column({ space: 5 }) {
      Text('basic').fontSize(30).fontColor(0xCCCCCC).width(320)
      // Draw a 300 x 50 rectangle with strokes at (-2, -2). The fill color is 0x317Af7, the stroke color is black, the stroke width is 4, the stroke dash is 20, the offset is 10 to the left, the cap style is rounded, the join style is rounded, and anti-aliasing is enabled (default).
      // Draw a 300 x 50 ellipse with strokes at (-2, 58). The fill color is 0x317Af7, the stroke color is black, the stroke width is 4, the stroke dash is 20, the offset is 10 to the left, the cap style is rounded, the join style is rounded, and anti-aliasing is enabled (default).
      // Draw a 300 x 10 path at (-2, 118). The fill color is 0x317Af7, the stroke color is black, the stroke width is 4, the stroke dash is 20, the offset is 10 to the left, the cap style is rounded, and the join style is rounded, and anti-aliasing is enabled (default).
      Shape() {
        Rect().width(300).height(50)
        Ellipse().width(300).height(50).offset({ x: 0, y: 60 })
        Path().width(300).height(10).commands('M0 0 L900 0').offset({ x: 0, y: 120 })
      }
      .viewPort({ x: -2, y: -2, width: 304, height: 130 })
      .fill(0x317Af7).stroke(Color.Black).strokeWidth(4)
      .strokeDashArray([20]).strokeDashOffset(10).strokeLineCap(LineCapStyle.Round)
      .strokeLineJoin(LineJoinStyle.Round).antiAlias(true)
      // Draw a 300 x 50 rectangle with strokes at (-1, -1). The fill color is 0x317Af7, the stroke color is black, and the stroke width is 2.
      Shape() {
        Rect().width(300).height(50)
      }.viewPort({ x: -1, y: -1, width: 302, height: 52 }).fill(0x317Af7).stroke(Color.Black).strokeWidth(2)

      Text('border').fontSize(30).fontColor(0xCCCCCC).width(320).margin({top:30})
      // Draw a 300 x 10 path at (0, -5). The color is 0xEE8443, the stroke width is 10, and the stroke gap is 20.
      Shape() {
        Path().width(300).height(10).commands('M0 0 L900 0')
      }.viewPort({ x: 0, y: -5, width: 300, height: 20 }).stroke(0xEE8443).strokeWidth(10).strokeDashArray([20])
      // Draw a 300 x 10 path at (0, -5). The fill color is 0xEE8443, the stroke width is 10, the stroke gap is 20, and the offset is 10 to the left.
      Shape() {
        Path().width(300).height(10).commands('M0 0 L900 0')
      }
      .viewPort({ x: 0, y: -5, width: 300, height: 20 })
      .stroke(0xEE8443).strokeWidth(10).strokeDashArray([20]).strokeDashOffset(10)
      // Draw a 300 x 10 path at (0, -5). The fill color is 0xEE8443, the stroke width is 10, and the stroke opacity is 0.5.
      Shape() {
        Path().width(300).height(10).commands('M0 0 L900 0')
      }.viewPort({ x: 0, y: -5, width: 300, height: 20 }).stroke(0xEE8443).strokeWidth(10).strokeOpacity(0.5)
      // Draw a 300 x 10 path at (0, -5). The fill color is 0xEE8443, the stroke width is 10, the stroke dash is 20, the offset is 10 to the left, and the cap style is rounded.
      Shape() {
        Path().width(300).height(10).commands('M0 0 L900 0')
      }
      .viewPort({ x: 0, y: -5, width: 300, height: 20 })
      .stroke(0xEE8443).strokeWidth(10).strokeDashArray([20]).strokeLineCap(LineCapStyle.Round)
      // Draw a 300 x 50 rectangle with strokes at (-5, -5). The fill color is 0x317Af7, the stroke width is 10, the stroke color is 0xEE8443, and the join style is rounded.
      Shape() {
        Rect().width(300).height(100)
      }
      .viewPort({ x: -5, y: -5, width: 310, height: 120 })
      .fill(0x317Af7).stroke(0xEE8443).strokeWidth(10).strokeLineJoin(LineJoinStyle.Round)
      Shape() {
        Path().width(300).height(60).commands('M0 0 L400 0 L400 200 Z')
      }
      .viewPort({ x: -80, y: -5, width: 310, height: 100 })
      .fill(0x317Af7).stroke(0xEE8443).strokeWidth(10)
      .strokeLineJoin(LineJoinStyle.Miter).strokeMiterLimit(5)
    }.width('100%').margin({ top: 15 })
  }
}
```

![en-us_image_0000001257058393](figures/en-us_image_0000001257058393.png)
