# OffscreenCanvasRenderingContext2D


> ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE**
> The APIs of this module are supported since API version 8. Updates will be marked with a superscript to indicate their earliest API version.


Use **OffscreenCanvasRenderingContext2D** to draw rectangles, images, and text offscreen onto a canvas. Drawing offscreen onto a canvas is a process where content to draw onto the canvas is first drawn in the buffer, and then converted into a picture, and finally the picture is drawn on the canvas. This process increases the drawing efficiency.


## APIs

OffscreenCanvasRenderingContext2D(width: number, height: number, setting: RenderingContextSettings)

- Parameters
    | Name    | Type                                     | Mandatory | Default Value | Description                     |
    | ------- | ---------------------------------------- | --------- | ------------- | ------------------------------- |
    | width   | number                                   | Yes       | -             | Width of the offscreen canvas.  |
    | height  | number                                   | Yes       | -             | Height of the offscreen canvas. |
    | setting | [RenderingContextSettings](ts-canvasrenderingcontext2d.md#renderingcontextsettings) | Yes       | -             | See RenderingContextSettings.   |


## Attributes

| Name                                     | Type                                     | Default Value                   | Description                              |
| ---------------------------------------- | ---------------------------------------- | ------------------------------- | ---------------------------------------- |
| [fillStyle](#fillstyle)                  | &lt;color&gt; \| [CanvasGradient](ts-components-canvas-canvasgradient.md) \| [CanvasPattern](#canvaspattern) | -                               | Style used to fill an area.<br/>- When the type is **&lt;color&gt;**, this attribute indicates the fill color.<br/>- When the type is **CanvasGradient**, this attribute indicates a gradient object, which is created using the [createLinearGradient](#createlineargradient) method.<br/>- When the type is **CanvasPattern**, this attribute indicates a pattern, which is created using the [createPattern](#createpattern) method. |
| [lineWidth](#linewidth)                  | number                                   | -                               | Line width.                              |
| [strokeStyle](#strokestyle)              | &lt;color&gt; \| [CanvasGradient](ts-components-canvas-canvasgradient.md) \| [CanvasPattern](#canvaspattern) | -                               | Stroke style.<br/>- When the type is **&lt;color&gt;**, this attribute indicates the stroke color.<br/>- When the type is **CanvasGradient**, this attribute indicates a gradient object, which is created using the [createLinearGradient](#createlineargradient) method.<br/>- When the type is **CanvasPattern**, this attribute indicates a pattern, which is created using the [createPattern](#createpattern) method. |
| [lineCap](#linecap)                      | string                                   | 'butt'                          | Style of the line endpoints. The options are as follows:<br/>- **'butt'**: The endpoints of the line are squared off.<br/>- **'round'**: The endpoints of the line are rounded.<br/>- **'square'**: The endpoints of the line are squared off by adding a box with an equal width and half the height of the line's thickness. |
| [lineJoin](#linejoin)                    | string                                   | 'miter'                         | Style of the shape used to join line segments. The options are as follows:<br/>- **'round'**: The shape used to join line segments is a rounded corner with the radius equal to the line width.<br/>- **'bevel'**: The shape used to join line segments is a beveled corner. The rectangular corner of each line is independent.<br/>- **'miter'**: The shape used to join line segments is a mitered corner. The corner is formed by extending the outside edges of the lines until they meet. You can adjust the effect of this attribute using **miterLimit**. |
| [miterLimit](#miterlimit)                | number                                   | 10                              | Maximum miter length. The miter length is the distance between the inner corner and the outer corner where two lines meet. |
| [font](#font)                            | string                                   | 'normal normal 14px sans-serif' | Font style.<br/>Syntax: ctx.font='font-size font-family'<br/>- (Optional) **font-size**: font size and row height. The unit can only be px.<br/>- (Optional) **font-family**: font family.<br/>Syntax: ctx.font='font-style font-weight font-size font-family'<br/>- (Optional) **font-style**: specifies the font style. Available values are **'normal'** and **'italic'**.<br/>- (Optional) **font-weight**: font weight. Available values are as follows: **'normal'**, **'bold'**, **'bolder'**, **'lighter'**, **100**, **200**, **300**, **400**, **500**, **600**, **700**, **800**, **900**<br/>- (Optional) **font-size**: font size and row height. The unit can only be px.<br/>- (Optional) **font-family**: font family. Available values are **'sans-serif'**, **'serif'**, and **'monospace'**. |
| [textAlign](#textalign)                  | string                                   | 'left'                          | Text alignment mode. Available values are as follows:<br/>- **'left'**: The text is left-aligned.<br/>- **'right'**: The text is right-aligned.<br/>- **'center'**: The text is center-aligned.<br/>- **'start'**: The text is aligned with the start bound.<br/>- **'end'**: The text is aligned with the end bound.<br/>> ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE**<br/>> In the **ltr** layout mode, the value **start** equals **left**. In the **rtl** layout mode, the value **start** equals **right**. |
| [textBaseline](#textbaseline)            | string                                   | 'alphabetic'                    | Horizontal alignment mode of text. Available values are as follows:<br/>- **'alphabetic'**: The text baseline is the normal alphabetic baseline.<br/>- **'top'**: The text baseline is on the top of the text bounding box.<br/>- **'hanging'**: The text baseline is a hanging baseline over the text.<br/>- **'middle'**: The text baseline is in the middle of the text bounding box.<br/>- **'ideographic'**: The text baseline is the ideographic baseline. If a character exceeds the alphabetic baseline, the ideographic baseline is located at the bottom of the excess character.<br/>- **'bottom'**: The text baseline is at the bottom of the text bounding box. Its difference from the ideographic baseline is that the ideographic baseline does not consider letters in the next line. |
| [globalAlpha](#globalalpha)              | number                                   | -                               | Opacity. **0.0**: completely transparent; **1.0**: completely opaque. |
| [lineDashOffset](#linedashoffset)        | number                                   | 0.0                             | Offset of the dashed line. The precision is float. |
| [globalCompositeOperation](#globalcompositeoperation) | string                                   | 'source-over'                   | Composition operation type. Available values are as follows: **'source-over'**, **'source-atop'**, **'source-in'**, **'source-out'**, **'destination-over'**, **'destination-atop'**, **'destination-in'**, **'destination-out'**, **'lighter'**, **'copy'**, and **'xor'**. |
| [shadowBlur](#shadowblur)                | number                                   | 0.0                             | Blur level during shadow drawing. A larger value indicates a more blurred effect. The precision is float. |
| [shadowColor](#shadowcolor)              | &lt;color&gt;                            | -                               | Shadow color.                            |
| [shadowOffsetX](#shadowoffsetx)          | number                                   | -                               | X-axis shadow offset relative to the original object. |
| [shadowOffsetY](#shadowoffsety)          | number                                   | -                               | Y-axis shadow offset relative to the original object. |
| [imageSmoothingEnabled](#imagesmoothingenabled) | boolean                                  | true                            | Whether to adjust the image smoothness during image drawing. The value **true** means to enable this feature, and **false** means the opposite. |
| imageSmoothingQuality                    | string                                   | 'low'                           | Image smoothness. The value can be **'low'**, **'medium'**, or **'high'**. |

> ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE**
> The value of the **&lt;color&gt;** type can be in 'rgb(255, 255, 255)', 'rgba(255, 255, 255, 1.0)', or '\#FFFFFF' format.


### fillStyle


```
@Entry
@Component
struct FillStyleExample {
  private settings: RenderingContextSettings = new RenderingContextSettings(true)
  private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
  private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)

  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Canvas(this.context)
        .width('100%')
        .height('100%')
        .backgroundColor('#ffff00')
        .onReady(() =>{
          this.offContext.fillStyle = '#0000ff'
          this.offContext.fillRect(20, 160, 150, 100)
          var image = this.offContext.transferToImageBitmap();
          this.context.transferFromImageBitmap(image);
        })
    }
    .width('100%')
    .height('100%')
  }
}
```

![en-us_image_0000001211898510](figures/en-us_image_0000001211898510.png)


### lineWidth


```
@Entry
@Component
struct LineWidthExample {
  private settings: RenderingContextSettings = new RenderingContextSettings(true)
  private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
  private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)

  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Canvas(this.context)
        .width('100%')
        .height('100%')
        .backgroundColor('#ffff00')
        .onReady(() =>{
          this.offContext.lineWidth = 5
          this.offContext.strokeRect(25, 25, 85, 105)
          var image = this.offContext.transferToImageBitmap()
          this.context.transferFromImageBitmap(image)
      })
    }
    .width('100%')
    .height('100%')
  }
}
```

![en-us_image_0000001257058439](figures/en-us_image_0000001257058439.png)


### strokeStyle


```
@Entry
@Component
struct StrokeStyleExample {
  private settings: RenderingContextSettings = new RenderingContextSettings(true)
  private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
  private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)

  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Canvas(this.context)
        .width('100%')
        .height('100%')
        .backgroundColor('#ffff00')
        .onReady(() =>{
          this.offContext.lineWidth = 10
          this.offContext.strokeStyle = '#0000ff'
          this.offContext.strokeRect(25, 25, 155, 105)
          var image = this.offContext.transferToImageBitmap()
          this.context.transferFromImageBitmap(image)
        })
    }
    .width('100%')
    .height('100%')
  }
}
```


![en-us_image_0000001257058429](figures/en-us_image_0000001257058429.png)


### lineCap


```
@Entry
@Component
struct LineCapExample {
  private settings: RenderingContextSettings = new RenderingContextSettings(true)
  private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
  private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)

  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Canvas(this.context)
        .width('100%')
        .height('100%')
        .backgroundColor('#ffff00')
        .onReady(() =>{
          this.offContext.lineWidth = 8
          this.offContext.beginPath()
          this.offContext.lineCap = 'round'
          this.offContext.moveTo(30, 50)
          this.offContext.lineTo(220, 50)
          this.offContext.stroke()
          var image = this.offContext.transferToImageBitmap()
          this.context.transferFromImageBitmap(image)
        })
    }
    .width('100%')
    .height('100%')
  }
}
```

![en-us_image_0000001256858427](figures/en-us_image_0000001256858427.png)


### lineJoin


```
@Entry
@Component
struct LineJoinExample {
  private settings: RenderingContextSettings = new RenderingContextSettings(true)
  private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
  private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)

  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Canvas(this.context)
        .width('100%')
        .height('100%')
        .backgroundColor('#ffff00')
        .onReady(() =>{
          this.offContext.beginPath()
          this.offContext.lineWidth = 8
          this.offContext.lineJoin = 'miter'
          this.offContext.moveTo(30, 30)
          this.offContext.lineTo(120, 60)
          this.offContext.lineTo(30, 110)
          this.offContext.stroke()
          var image = this.offContext.transferToImageBitmap()
          this.context.transferFromImageBitmap(image)
      })
    }
    .width('100%')
    .height('100%')
  }
}
```

![en-us_image_0000001256858429](figures/en-us_image_0000001256858429.png)


### miterLimit


```
@Entry
@Component
struct MiterLimit {
  private settings: RenderingContextSettings = new RenderingContextSettings(true)
  private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
  private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
  
  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Canvas(this.context)
        .width('100%')
        .height('100%')
        .backgroundColor('#ffff00')
        .onReady(() =>{
          this.offContext.lineWidth = 8
          this.offContext.lineJoin = 'miter'
          this.offContext.miterLimit = 3
          this.offContext.moveTo(30, 30)
          this.offContext.lineTo(60, 35)
          this.offContext.lineTo(30, 37)
          this.offContext.stroke()
          var image = this.offContext.transferToImageBitmap()
          this.context.transferFromImageBitmap(image)
      })
    }
    .width('100%')
    .height('100%')
  }
}
```

![en-us_image_0000001212218472](figures/en-us_image_0000001212218472.png)


### font


```
@Entry
@Component
struct Font {
  private settings: RenderingContextSettings = new RenderingContextSettings(true)
  private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
  private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
  
  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Canvas(this.context)
        .width('100%')
        .height('100%')
        .backgroundColor('#ffff00')
        .onReady(() =>{
          this.offContext.font = '30px sans-serif'
          this.offContext.fillText("Hello World", 20, 60)
          var image = this.offContext.transferToImageBitmap()
          this.context.transferFromImageBitmap(image)
      })
    }
    .width('100%')
    .height('100%')
  }
}
```

![en-us_image_0000001211898508](figures/en-us_image_0000001211898508.png)


### textAlign


```
@Entry
@Component
struct CanvasExample {
  private settings: RenderingContextSettings = new RenderingContextSettings(true)
  private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
  private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
  
  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Canvas(this.context)
        .width('100%')
        .height('100%')
        .backgroundColor('#ffff00')
        .onReady(() =>{
        this.offContext.strokeStyle = '#0000ff'
        this.offContext.moveTo(140, 10)
        this.offContext.lineTo(140, 160)
        this.offContext.stroke()

        this.offContext.font = '18px sans-serif'

        this.offContext.textAlign = 'start'
        this.offContext.fillText('textAlign=start', 140, 60)
        this.offContext.textAlign = 'end'
        this.offContext.fillText('textAlign=end', 140, 80)
        this.offContext.textAlign = 'left'
        this.offContext.fillText('textAlign=left', 140, 100)
        this.offContext.textAlign = 'center'
        this.offContext.fillText('textAlign=center',140, 120)
        this.offContext.textAlign = 'right'
        this.offContext.fillText('textAlign=right',140, 140)
        var image = this.offContext.transferToImageBitmap()
        this.context.transferFromImageBitmap(image)
      })
    }
    .width('100%')
    .height('100%')
  }
}
```

![en-us_image_0000001257138377](figures/en-us_image_0000001257138377.png)


### textBaseline


```
@Entry
@Component
struct TextBaseline {
  private settings: RenderingContextSettings = new RenderingContextSettings(true)
  private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
  private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
  
  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Canvas(this.context)
        .width('100%')
        .height('100%')
        .backgroundColor('#ffff00')
        .onReady(() =>{
          this.offContext.strokeStyle = '#0000ff'
          this.offContext.moveTo(0, 120)
          this.offContext.lineTo(400, 120)
          this.offContext.stroke()

          this.offContext.font = '20px sans-serif'

          this.offContext.textBaseline = 'top'
          this.offContext.fillText('Top', 10, 120)
          this.offContext.textBaseline = 'bottom'
          this.offContext.fillText('Bottom', 55, 120)
          this.offContext.textBaseline = 'middle'
          this.offContext.fillText('Middle', 125, 120)
          this.offContext.textBaseline = 'alphabetic'
          this.offContext.fillText('Alphabetic', 195, 120)
          this.offContext.textBaseline = 'hanging'
          this.offContext.fillText('Hanging', 295, 120)
          var image = this.offContext.transferToImageBitmap()
          this.context.transferFromImageBitmap(image)
      })
    }
    .width('100%')
    .height('100%')
  }
}
```

![en-us_image_0000001256978375](figures/en-us_image_0000001256978375.png)


### globalAlpha


```
@Entry
@Component
struct GlobalAlpha {
  private settings: RenderingContextSettings = new RenderingContextSettings(true)
  private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
  private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
  
  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Canvas(this.context)
        .width('100%')
        .height('100%')
        .backgroundColor('#ffff00')
        .onReady(() =>{
          this.offContext.fillStyle = 'rgb(255,0,0)'
          this.offContext.fillRect(0, 0, 50, 50)
          this.offContext.globalAlpha = 0.4
          this.offContext.fillStyle = 'rgb(0,0,255)'
          this.offContext.fillRect(50, 50, 50, 50)
          var image = this.offContext.transferToImageBitmap()
          this.context.transferFromImageBitmap(image)
      })
    }
    .width('100%')
    .height('100%')
  }
}
```

![en-us_image_0000001211898506](figures/en-us_image_0000001211898506.png)


### lineDashOffset


```
@Entry
@Component
struct LineDashOffset {
  private settings: RenderingContextSettings = new RenderingContextSettings(true)
  private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
  private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
  
  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Canvas(this.context)
        .width('100%')
        .height('100%')
        .backgroundColor('#ffff00')
        .onReady(() =>{
          this.offContext.arc(100, 75, 50, 0, 6.28)
          this.offContext.setLineDash([10,20])
          this.offContext.stroke();
          var image = this.offContext.transferToImageBitmap()
          this.context.transferFromImageBitmap(image)
      })
    }
    .width('100%')
    .height('100%')
  }
}
```

![en-us_image_0000001212058506](figures/en-us_image_0000001212058506.png)


### globalCompositeOperation

| Name             | Description                              |
| ---------------- | ---------------------------------------- |
| source-over      | Displays the new drawing above the existing drawing. This attribute is used by default. |
| source-atop      | Displays the new drawing on the top of the existing drawing. |
| source-in        | Displays the new drawing inside the existing drawing. |
| source-out       | Displays the part of the new drawing that is outside of the existing drawing. |
| destination-over | Displays the existing drawing above the new drawing. |
| destination-atop | Displays the existing drawing on the top of the new drawing. |
| destination-in   | Displays the existing drawing inside the new drawing. |
| destination-out  | Displays the part of the existing drawing that is outside of the new drawing. |
| lighter          | Displays both the new drawing and the existing drawing. |
| copy             | Displays the new drawing and neglects the existing drawing. |
| xor              | Combines the new drawing and existing drawing using the XOR operation. |


```
@Entry
@Component
struct GlobalCompositeOperation {
  private settings: RenderingContextSettings = new RenderingContextSettings(true)
  private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
  private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
  
  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Canvas(this.context)
        .width('100%')
        .height('100%')
        .backgroundColor('#ffff00')
        .onReady(() =>{
          this.offContext.fillStyle = 'rgb(255,0,0)'
          this.offContext.fillRect(20, 20, 50, 50)
          this.offContext.globalCompositeOperation = 'source-over'
          this.offContext.fillStyle = 'rgb(0,0,255)'
          this.offContext.fillRect(50, 50, 50, 50)
          this.offContext.fillStyle = 'rgb(255,0,0)'
          this.offContext.fillRect(120, 20, 50, 50)
          this.offContext.globalCompositeOperation = 'destination-over'
          this.offContext.fillStyle = 'rgb(0,0,255)'
          this.offContext.fillRect(150, 50, 50, 50)
          var image = this.offContext.transferToImageBitmap()
          this.context.transferFromImageBitmap(image)
      })
    }
    .width('100%')
    .height('100%')
  }
}
```

![en-us_image_0000001212218474](figures/en-us_image_0000001212218474.png)


### shadowBlur


```
@Entry
@Component
struct ShadowBlur {
  private settings: RenderingContextSettings = new RenderingContextSettings(true)
  private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
  private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
  
  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Canvas(this.context)
        .width('100%')
        .height('100%')
        .backgroundColor('#ffff00')
        .onReady(() =>{
          this.offContext.shadowBlur = 30
          this.offContext.shadowColor = 'rgb(0,0,0)'
          this.offContext.fillStyle = 'rgb(255,0,0)'
          this.offContext.fillRect(20, 20, 100, 80)
          var image = this.offContext.transferToImageBitmap()
          this.context.transferFromImageBitmap(image)
      })
    }
    .width('100%')
    .height('100%')
  }
}
```

![en-us_image_0000001211898514](figures/en-us_image_0000001211898514.png)


### shadowColor


```
@Entry
@Component
struct ShadowColor {
  private settings: RenderingContextSettings = new RenderingContextSettings(true)
  private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
  private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
  
  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Canvas(this.context)
        .width('100%')
        .height('100%')
        .backgroundColor('#ffff00')
        .onReady(() =>{
          this.offContext.shadowBlur = 30
          this.offContext.shadowColor = 'rgb(0,0,255)'
          this.offContext.fillStyle = 'rgb(255,0,0)'
          this.offContext.fillRect(30, 30, 100, 100)
          var image = this.offContext.transferToImageBitmap
()
          this.context.transferFromImageBitmap(image)
      })
    }
    .width('100%')
    .height('100%')
  }
}
```

![en-us_image_0000001212058502](figures/en-us_image_0000001212058502.png)


### shadowOffsetX


```
@Entry
@Component
struct ShadowOffsetX {
  private settings: RenderingContextSettings = new RenderingContextSettings(true)
  private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
  private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
  
  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Canvas(this.context)
        .width('100%')
        .height('100%')
        .backgroundColor('#ffff00')
        .onReady(() =>{
          this.offContext.shadowBlur = 10
          this.offContext.shadowOffsetX = 20
          this.offContext.shadowColor = 'rgb(0,0,0)'
          this.offContext.fillStyle = 'rgb(255,0,0)'
          this.offContext.fillRect(20, 20, 100, 80)
          var image = this.offContext.transferToImageBitmap()
          this.context.transferFromImageBitmap(image)
      })
    }
    .width('100%')
    .height('100%')
  }
}
```

![en-us_image_0000001257138379](figures/en-us_image_0000001257138379.png)


### shadowOffsetY


```
@Entry
@Component
struct ShadowOffsetY {
  private settings: RenderingContextSettings = new RenderingContextSettings(true)
  private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
  private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)

  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Canvas(this.context)
        .width('100%')
        .height('100%')
        .backgroundColor('#ffff00')
        .onReady(() =>{
          this.offContext.shadowBlur = 10
          this.offContext.shadowOffsetY = 20
          this.offContext.shadowColor = 'rgb(0,0,0)'
          this.offContext.fillStyle = 'rgb(255,0,0)'
          this.offContext.fillRect(30, 30, 100, 100)
          var image = this.offContext.transferToImageBitmap()
          this.context.transferFromImageBitmap(image)
      })
    }
    .width('100%')
    .height('100%')
  }
}
```

![en-us_image_0000001257058427](figures/en-us_image_0000001257058427.png)


### imageSmoothingEnabled


```
@Entry
@Component
struct ImageSmoothingEnabled {
  private settings: RenderingContextSettings = new RenderingContextSettings(true)
  private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
  private img:ImageBitmap = new ImageBitmap("common/images/icon.jpg")
  private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
  
  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Canvas(this.context)
        .width('100%')
        .height('100%')
        .backgroundColor('#ffff00')
        .onReady(() =>{
          this.offContext.imageSmoothingEnabled = false
          this.offContext.drawImage( this.img,0,0,400,200)
          var image = this.offContext.transferToImageBitmap()
          this.context.transferFromImageBitmap(image)
      })
    }
    .width('100%')
    .height('100%')
  }
}
```

![en-us_image_0000001257138385](figures/en-us_image_0000001257138385.png)


## Methods


### fillRect

fillRect(x: number, y: number, w: number, h: number): void

Fills a rectangle on the canvas.

- Parameters
    | Name   | Type   | Mandatory | Default Value | Description                              |
    | ------ | ------ | --------- | ------------- | ---------------------------------------- |
    | x      | number | Yes       | 0             | X-coordinate of the upper left corner of the rectangle. |
    | y      | number | Yes       | 0             | Y-coordinate of the upper left corner of the rectangle. |
    | width  | number | Yes       | 0             | Width of the rectangle.                  |
    | height | number | Yes       | 0             | Height of the rectangle.                 |

- Example

  ```
  @Entry
  @Component
  struct FillRect {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.fillRect(0,30,100,100)
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
         })
        }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001257138375](figures/en-us_image_0000001257138375.png)


### strokeRect

strokeRect(x: number, y: number, w: number, h: number): void

Draws an outlined rectangle on the canvas.

- Parameters
    | Name   | Type   | Mandatory | Default Value | Description                              |
    | ------ | ------ | --------- | ------------- | ---------------------------------------- |
    | x      | number | Yes       | 0             | X-coordinate of the upper left corner of the rectangle. |
    | y      | number | Yes       | 0             | Y-coordinate of the upper left corner of the rectangle. |
    | width  | number | Yes       | 0             | Width of the rectangle.                  |
    | height | number | Yes       | 0             | Height of the rectangle.                 |

- Example

  ```
  @Entry
  @Component
  struct StrokeRect {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.strokeRect(30, 30, 200, 150)
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
        })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001212378436](figures/en-us_image_0000001212378436.png)


### clearRect

clearRect(x: number, y: number, w: number, h: number): void

Clears the content in a rectangle on the canvas.

- Parameters
    | Name   | Type   | Mandatory | Default Value | Description                              |
    | ------ | ------ | --------- | ------------- | ---------------------------------------- |
    | x      | number | Yes       | 0             | X-coordinate of the upper left corner of the rectangle. |
    | y      | number | Yes       | 0             | Y-coordinate of the upper left corner of the rectangle. |
    | width  | number | Yes       | 0             | Width of the rectangle.                  |
    | height | number | Yes       | 0             | Height of the rectangle.                 |

- Example

  ```
  @Entry
  @Component
  struct ClearRect {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.fillStyle = 'rgb(0,0,255)'
            this.offContext.fillRect(0,0,500,500)
            this.offContext.clearRect(20,20,150,100)
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
        })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001212058500](figures/en-us_image_0000001212058500.png)


### fillText

fillText(text: string, x: number, y: number): void

Draws filled text on the canvas.

- Parameters
    | Name | Type   | Mandatory | Default Value | Description                              |
    | ---- | ------ | --------- | ------------- | ---------------------------------------- |
    | text | string | Yes       | ""            | Text to draw.                            |
    | x    | number | Yes       | 0             | X-coordinate of the lower left corner of the text. |
    | y    | number | Yes       | 0             | Y-coordinate of the lower left corner of the text. |

- Example

  ```
  @Entry
  @Component
  struct FillText {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.font = '30px sans-serif'
            this.offContext.fillText("Hello World!", 20, 100)
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
        })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001257058437](figures/en-us_image_0000001257058437.png)


### strokeText

strokeText(text: string, x: number, y: number): void

Draws a text stroke on the canvas.

- Parameters
    | Name | Type   | Mandatory | Default Value | Description                              |
    | ---- | ------ | --------- | ------------- | ---------------------------------------- |
    | text | string | Yes       | ""            | Text to draw.                            |
    | x    | number | Yes       | 0             | X-coordinate of the lower left corner of the text. |
    | y    | number | Yes       | 0             | Y-coordinate of the lower left corner of the text. |

- Example

  ```
  @Entry
  @Component
  struct StrokeText {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.font = '55px sans-serif'
            this.offContext.strokeText("Hello World!", 20, 60)
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
        })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001212218466](figures/en-us_image_0000001212218466.png)


### measureText

measureText(text: string): TextMetrics

Returns a **TextMetrics** object used to obtain the width of specified text.

- Parameters
    | Name | Type   | Mandatory | Default Value | Description          |
    | ---- | ------ | --------- | ------------- | -------------------- |
    | text | string | Yes       | ""            | Text to be measured. |

- Return value
    | Type        | Description             |
    | ----------- | ----------------------- |
    | TextMetrics | **TextMetrics** object. |

- **TextMetrics** attributes
    | Name  | Type   | Description        |
    | ----- | ------ | ------------------ |
    | width | number | Width of the text. |

- Example

  ```
  @Entry
  @Component
  struct MeasureText {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.font = '50px sans-serif'
            this.offContext.fillText("Hello World!", 20, 100)
            this.offContext.fillText("width:" + this.context.measureText("Hello World!").width, 20, 200)
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
        })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001256858431](figures/en-us_image_0000001256858431.png)


### stroke

stroke(path?: Path2D): void

Strokes a path.

- Parameters
    | Name | Type                                     | Mandatory | Default Value | Description                |
    | ---- | ---------------------------------------- | --------- | ------------- | -------------------------- |
    | path | [Path2D](ts-components-canvas-path2d.md) | No        | null          | A **Path2D** path to draw. |

- Example

  ```
  @Entry
  @Component
  struct Stroke {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.moveTo(25, 25)
            this.offContext.lineTo(25, 105)
            this.offContext.strokeStyle = 'rgb(0,0,255)'
            this.offContext.stroke()
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001257138373](figures/en-us_image_0000001257138373.png)


### beginPath

beginPath(): void

Creates a drawing path.

- Example

  ```
  @Entry
  @Component
  struct BeginPath {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.beginPath()
            this.offContext.lineWidth = 6
            this.offContext.strokeStyle = '#0000ff'
            this.offContext.moveTo(15, 80)
            this.offContext.lineTo(280, 160)
            this.offContext.stroke()
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001212378440](figures/en-us_image_0000001212378440.png)


### moveTo

moveTo(x: number, y: number): void

Moves a drawing path to a target position on the canvas.

- Parameters
    | Name | Type   | Mandatory | Default Value | Description                          |
    | ---- | ------ | --------- | ------------- | ------------------------------------ |
    | x    | number | Yes       | 0             | X-coordinate of the target position. |
    | y    | number | Yes       | 0             | Y-coordinate of the target position. |

- Example

  ```
  @Entry
  @Component
  struct MoveTo {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.beginPath()
            this.offContext.moveTo(10, 10)
            this.offContext.lineTo(280, 160)
            this.offContext.stroke()
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001212058498](figures/en-us_image_0000001212058498.png)


### lineTo

lineTo(x: number, y: number): void

Connects the current point to a target position using a straight line.

- Parameters
    | Name | Type   | Mandatory | Default Value | Description                          |
    | ---- | ------ | --------- | ------------- | ------------------------------------ |
    | x    | number | Yes       | 0             | X-coordinate of the target position. |
    | y    | number | Yes       | 0             | Y-coordinate of the target position. |

- Example

  ```
  @Entry
  @Component
  struct LineTo {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.beginPath()
            this.offContext.moveTo(10, 10)
            this.offContext.lineTo(280, 160)
            this.offContext.stroke()
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001257058435](figures/en-us_image_0000001257058435.png)


### closePath

closePath(): void

Draws a closed path.

- Example

  ```
  @Entry
  @Component
  struct ClosePath {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
              this.offContext.beginPath()
              this.offContext.moveTo(30, 30)
              this.offContext.lineTo(110, 30)
              this.offContext.lineTo(70, 90)
              this.offContext.closePath()
              this.offContext.stroke()
              var image = this.offContext.transferToImageBitmap()
              this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001257058431](figures/en-us_image_0000001257058431.png)


### createPattern

createPattern(image: ImageBitmap, repetition: string): CanvasPattern

Creates a pattern for image filling based on a specified source image and repetition mode.

- Parameters
    | Name       | Type                                     | Mandatory | Default Value | Description                              |
    | ---------- | ---------------------------------------- | --------- | ------------- | ---------------------------------------- |
    | image      | [ImageBitmap](ts-components-canvas-imagebitmap.md) | Yes       | null          | Source image. For details, see ImageBitmap. |
    | repetition | string                                   | Yes       | ""            | Repetition mode. The value can be **'repeat'**, **'repeat-x'**, **'repeat-y'**, or **'no-repeat'**. |

- Example

  ```
  @Entry
  @Component
  struct CreatePattern {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private img:ImageBitmap = new ImageBitmap("common/images/icon.jpg")
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            var pattern = this.offContext.createPattern(this.img, 'repeat')
            this.offContext.fillStyle = pattern
            this.offContext.fillRect(0, 0, 200, 200)
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001257138387](figures/en-us_image_0000001257138387.png)


### bezierCurveTo

bezierCurveTo(cp1x: number, cp1y: number, cp2x: number, cp2y: number, x: number, y: number): void

Draws a cubic bezier curve on the canvas.

- Name
    | Name | Type   | Mandatory | Default Value | Description                              |
    | ---- | ------ | --------- | ------------- | ---------------------------------------- |
    | cp1x | number | Yes       | 0             | X-coordinate of the first parameter of the bezier curve. |
    | cp1y | number | Yes       | 0             | Y-coordinate of the first parameter of the bezier curve. |
    | cp2x | number | Yes       | 0             | X-coordinate of the second parameter of the bezier curve. |
    | cp2y | number | Yes       | 0             | Y-coordinate of the second parameter of the bezier curve. |
    | x    | number | Yes       | 0             | X-coordinate of the end point on the bezier curve. |
    | y    | number | Yes       | 0             | Y-coordinate of the end point on the bezier curve. |

- Example

  ```
  @Entry
  @Component
  struct BezierCurveTo {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.beginPath()
            this.offContext.moveTo(10, 10)
            this.offContext.bezierCurveTo(20, 100, 200, 100, 200, 20)
            this.offContext.stroke()
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001212378442](figures/en-us_image_0000001212378442.png)


### quadraticCurveTo

quadraticCurveTo(cpx: number, cpy: number, x: number, y: number): void

Draws a quadratic curve on the canvas.

- Parameters
    | Name | Type   | Mandatory | Default Value | Description                              |
    | ---- | ------ | --------- | ------------- | ---------------------------------------- |
    | cpx  | number | Yes       | 0             | X-coordinate of the bezier curve parameter. |
    | cpy  | number | Yes       | 0             | Y-coordinate of the bezier curve parameter. |
    | x    | number | Yes       | 0             | X-coordinate of the end point on the bezier curve. |
    | y    | number | Yes       | 0             | Y-coordinate of the end point on the bezier curve. |

- Example

  ```
  @Entry
  @Component
  struct QuadraticCurveTo {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.beginPath();
            this.offContext.moveTo(20, 20);
            this.offContext.quadraticCurveTo(100, 100, 200, 20);
            this.offContext.stroke();
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
        })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001256978383](figures/en-us_image_0000001256978383.png)


### arc

arc(x: number, y: number, radius: number, startAngle: number, endAngle: number, anticlockwise?: boolean): void

Draws an arc on the canvas.

- Parameters
    | Name          | Type    | Mandatory | Default Value | Description                              |
    | ------------- | ------- | --------- | ------------- | ---------------------------------------- |
    | x             | number  | Yes       | 0             | X-coordinate of the center point of the arc. |
    | y             | number  | Yes       | 0             | Y-coordinate of the center point of the arc. |
    | radius        | number  | Yes       | 0             | Radius of the arc.                       |
    | startAngle    | number  | Yes       | 0             | Start radian of the arc.                 |
    | endAngle      | number  | Yes       | 0             | End radian of the arc.                   |
    | anticlockwise | boolean | No        | false         | Whether to draw the arc counterclockwise. |

- Example

  ```
  @Entry
  @Component
  struct Arc {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.beginPath()
            this.offContext.arc(100, 75, 50, 0, 6.28)
            this.offContext.stroke()
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001212378430](figures/en-us_image_0000001212378430.png)


### arcTo

arcTo(x1: number, y1: number, x2: number, y2: number, radius: number): void

Draws an arc based on the radius and points on the arc.

- Parameters
    | Name   | Type   | Mandatory | Default Value | Description                              |
    | ------ | ------ | --------- | ------------- | ---------------------------------------- |
    | x1     | number | Yes       | 0             | X-coordinate of the first point on the arc. |
    | y1     | number | Yes       | 0             | Y-coordinate of the first point on the arc. |
    | x2     | number | Yes       | 0             | X-coordinate of the second point on the arc. |
    | y2     | number | Yes       | 0             | Y-coordinate of the second point on the arc. |
    | radius | number | Yes       | 0             | Radius of the arc.                       |

- Example

  ```
  @Entry
  @Component
  struct ArcTo {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.moveTo(100, 20);
            this.offContext.arcTo(150, 20, 150, 70, 50);
            this.offContext.stroke();
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001257138383](figures/en-us_image_0000001257138383.png)


### ellipse

ellipse(x: number, y: number, radiusX: number, radiusY: number, rotation: number, startAngle: number, endAngle: number, anticlockwise?: boolean): void

Draws an ellipse in the specified rectangular region.

- Parameters
    | Name          | Type    | Mandatory | Default Value | Description                              |
    | ------------- | ------- | --------- | ------------- | ---------------------------------------- |
    | x             | number  | Yes       | 0             | X-coordinate of the ellipse center.      |
    | y             | number  | Yes       | 0             | Y-coordinate of the ellipse center.      |
    | radiusX       | number  | Yes       | 0             | Ellipse radius on the x-axis.            |
    | radiusY       | number  | Yes       | 0             | Ellipse radius on the y-axis.            |
    | rotation      | number  | Yes       | 0             | Rotation angle of the ellipse, in radians. |
    | startAngle    | number  | Yes       | 0             | Angle of the start point for drawing the ellipse, in radians. |
    | endAngle      | number  | Yes       | 0             | Angle of the end point for drawing the ellipse, in radians. |
    | anticlockwise | boolean | No        | false         | Whether to draw the ellipse in the counterclockwise direction. |

- Example


  ```
  @Entry
  @Component
  struct CanvasExample {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.beginPath()
            this.offContext.ellipse(200, 200, 50, 100, Math.PI * 0.25, Math.PI * 0.5, Math.PI)
            this.offContext.stroke()
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001256858423](figures/en-us_image_0000001256858423.png)


### rect

rect(x: number, y: number, width: number, height: number): void

Creates a rectangle.

- Parameters
    | Name   | Type   | Mandatory | Default Value | Description                              |
    | ------ | ------ | --------- | ------------- | ---------------------------------------- |
    | x      | number | Yes       | 0             | X-coordinate of the upper left corner of the rectangle. |
    | y      | number | Yes       | 0             | Y-coordinate of the upper left corner of the rectangle. |
    | width  | number | Yes       | 0             | Width of the rectangle.                  |
    | height | number | Yes       | 0             | Height of the rectangle.                 |

- Example

  ```
  @Entry
  @Component
  struct CanvasExample {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.rect(20, 20, 100, 100) // Create a 100*100 rectangle at (20, 20)
            this.offContext.stroke()
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001257138381](figures/en-us_image_0000001257138381.png)


### fill

fill(): void

Fills the area inside a closed path.

- Example

  ```
  @Entry
  @Component
  struct Fill {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.rect(20, 20, 100, 100) // Create a 100*100 rectangle at (20, 20)
            this.offContext.fill()
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001256858421](figures/en-us_image_0000001256858421.png)


### clip

clip(): void

Sets the current path to a clipping path.

- Example

  ```
  @Entry
  @Component
  struct Clip {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.rect(0, 0, 200, 200)
            this.offContext.stroke()
            this.offContext.clip()
            this.offContext.fillStyle = "rgb(255,0,0)"
            this.offContext.fillRect(0, 0, 150, 150)
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001257058441](figures/en-us_image_0000001257058441.png)


### rotate

rotate(rotate: number): void

Rotates a canvas clockwise around its coordinate axes.

- Parameters
    | Name   | Type   | Mandatory | Default Value | Description                              |
    | ------ | ------ | --------- | ------------- | ---------------------------------------- |
    | rotate | number | Yes       | 0             | Clockwise rotation angle. You can use **Math.PI / 180** to convert the angle to a radian. |

- Example

  ```
  @Entry
  @Component
  struct Rotate {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.rotate(45 * Math.PI / 180) // Rotate the rectangle 45 degrees
            this.offContext.fillRect(70, 20, 50, 50)
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001212218478](figures/en-us_image_0000001212218478.png)


### scale

scale(x: number, y: number): void

Scales a canvas based on scale factors.

- Parameters
    | Name | Type   | Mandatory | Default Value | Description              |
    | ---- | ------ | --------- | ------------- | ------------------------ |
    | x    | number | Yes       | 0             | Horizontal scale factor. |
    | y    | number | Yes       | 0             | Vertical scale factor.   |

- Example

  ```
  @Entry
  @Component
  struct Scale {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.strokeRect(10, 10, 25, 25)
            this.offContext.scale(2, 2) // Scale to 200%
            this.offContext.strokeRect(10, 10, 25, 25)
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001211898516](figures/en-us_image_0000001211898516.png)


### transform

transform(scaleX: number, skewX: number, skewY: number, scaleY: number, translateX: number, translateY: number): void

Defines a transformation matrix. To transform a graph, you only need to set parameters of the matrix. The coordinates of the graph are multiplied by the matrix values to obtain new coordinates of the transformed graph. You can use the matrix to implement multiple transform effects.

> ![icon-note.gif](public_sys-resources/icon-note.gif) **NOTE**
> The following formulas calculate coordinates of the transformed graph. **x** and **y** represent coordinates before transformation, and **x'** and **y'** represent coordinates after transformation.
>
> - x' = scaleX \* x + skewY \* y + translateX
>
> - y' = skewX \* x + scaleY \* y + translateY

- Parameters
    | Name       | Type   | Mandatory | Default Value | Description         |
    | ---------- | ------ | --------- | ------------- | ------------------- |
    | scaleX     | number | Yes       | 0             | X-axis scale.       |
    | skewX      | number | Yes       | 0             | X-axis skew.        |
    | skewY      | number | Yes       | 0             | Y-axis skew.        |
    | scaleY     | number | Yes       | 0             | Y-axis scale.       |
    | translateX | number | Yes       | 0             | X-axis translation. |
    | translateY | number | Yes       | 0             | Y-axis translation. |

- Example

  ```
  @Entry
  @Component
  struct Transform {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.fillStyle = 'rgb(0,0,0)'
            this.offContext.fillRect(0, 0, 100, 100)
            this.offContext.transform(1, 0.5, -0.5, 1, 10, 10)
            this.offContext.fillStyle = 'rgb(255,0,0)'
            this.offContext.fillRect(0, 0, 100, 100)
            this.offContext.transform(1, 0.5, -0.5, 1, 10, 10)
            this.offContext.fillStyle = 'rgb(0,0,255)'
            this.offContext.fillRect(0, 0, 100, 100)
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001212378438](figures/en-us_image_0000001212378438.png)


### setTransform

setTransform(scaleX: number, skewX: number, skewY: number, scale: number, translateX: number, translateY: number): void

Resets the existing transformation matrix and creates a new transformation matrix by using the same parameters as the **transform()** function.

- Parameters
    | Name       | Type   | Mandatory | Default Value | Description         |
    | ---------- | ------ | --------- | ------------- | ------------------- |
    | scaleX     | number | Yes       | 0             | X-axis scale.       |
    | skewX      | number | Yes       | 0             | X-axis skew.        |
    | skewY      | number | Yes       | 0             | Y-axis skew.        |
    | scaleY     | number | Yes       | 0             | Y-axis scale.       |
    | translateX | number | Yes       | 0             | X-axis translation. |
    | translateY | number | Yes       | 0             | Y-axis translation. |

- Example

  ```
  @Entry
  @Component
  struct SetTransform {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.fillStyle = 'rgb(255,0,0)'
            this.offContext.fillRect(0, 0, 100, 100)
            this.offContext.setTransform(1,0.5, -0.5, 1, 10, 10)
            this.offContext.fillStyle = 'rgb(0,0,255)'
            this.offContext.fillRect(0, 0, 100, 100)
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001211898518](figures/en-us_image_0000001211898518.png)


### translate

translate(x: number, y: number): void

Moves the origin of the coordinate system.

- Parameters
    | Name | Type   | Mandatory | Default Value | Description         |
    | ---- | ------ | --------- | ------------- | ------------------- |
    | x    | number | Yes       | 0             | X-axis translation. |
    | y    | number | Yes       | 0             | Y-axis translation. |

- Example

  ```
  @Entry
  @Component
  struct Translate {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.fillRect(10, 10, 50, 50)
            this.offContext.translate(70, 70)
            this.offContext.fillRect(10, 10, 50, 50)
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001256978373](figures/en-us_image_0000001256978373.png)


### drawImage

drawImage(image: ImageBitmap, dx: number, dy: number): void

drawImage(image: ImageBitmap, dx: number, dy: number, dWidth: number, dHeight: number): void

drawImage(image: ImageBitmap, sx: number, sy: number, sWidth: number, sHeight: number, dx: number, dy: number, dWidth: number, dHeight: number):void

Draws an image.

- Parameters
    | Name    | Type                                     | Mandatory | Default Value | Description                              |
    | ------- | ---------------------------------------- | --------- | ------------- | ---------------------------------------- |
    | image   | [ImageBitmap](ts-components-canvas-imagebitmap.md) | Yes       | null          | Image resource. For details, see ImageBitmap. |
    | sx      | number                                   | No        | 0             | X-coordinate of the upper left corner of the rectangle used to crop the source image. |
    | sy      | number                                   | No        | 0             | Y-coordinate of the upper left corner of the rectangle used to crop the source image. |
    | sWidth  | number                                   | No        | 0             | Target width to crop the source image.   |
    | sHeight | number                                   | No        | 0             | Target height to crop the source image.  |
    | dx      | number                                   | Yes       | 0             | X-coordinate of the upper left corner of the drawing area on the canvas. |
    | dy      | number                                   | Yes       | 0             | Y-coordinate of the upper left corner of the drawing area on the canvas. |
    | dWidth  | number                                   | No        | 0             | Width of the drawing area.               |
    | dHeight | number                                   | No        | 0             | Height of the drawing area.              |


- Example

  ```
  @Entry
  @Component
  struct Index {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private img:ImageBitmap = new ImageBitmap("common/images/icon.jpg")
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
        .width('100%')
        .height('100%')
        .backgroundColor('#ffff00')
        .onReady(() => {
            this.offContext.drawImage( this.img,0,0,400,200)
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
        })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001256978377](figures/en-us_image_0000001256978377.png)


### createImageData

createImageData(width: number, height: number): Object

Creates an **ImageData** object based on the specified width and height. For details, see [ImageData](ts-components-canvas-imagebitmap.md).

- Parameters
    | Name   | Type   | Mandatory | Default Value | Description                         |
    | ------ | ------ | --------- | ------------- | ----------------------------------- |
    | width  | number | Yes       | 0             | Width of the **ImageData** object.  |
    | height | number | Yes       | 0             | Height of the **ImageData** object. |


### createImageData

createImageData(imageData: ImageData): Object

Creates an **ImageData** object by copying an existing **ImageData** object. For details, see [ImageData](ts-components-canvas-imagebitmap.md).

- Parameters
    | Name      | Type                                     | Mandatory | Default Value | Description                   |
    | --------- | ---------------------------------------- | --------- | ------------- | ----------------------------- |
    | imagedata | [ImageData](ts-components-canvas-imagebitmap.md) | Yes       | null          | **ImageData** object to copy. |


### getImageData

getImageData(sx: number, sy: number, sw: number, sh: number): Object

Creates an [ImageData](ts-components-canvas-imagebitmap.md) object with pixels in the specified area on the canvas.

- Parameters
    | Name | Type   | Mandatory | Default Value | Description                              |
    | ---- | ------ | --------- | ------------- | ---------------------------------------- |
    | sx   | number | Yes       | 0             | X-coordinate of the upper left corner of the output area. |
    | sy   | number | Yes       | 0             | Y-coordinate of the upper left corner of the output area. |
    | sw   | number | Yes       | 0             | Width of the output area.                |
    | sh   | number | Yes       | 0             | Height of the output area.               |


### putImageData

putImageData(imageData: Object, dx: number, dy: number, dirtyX?: number, dirtyY?: number, dirtyWidth?: number, dirtyHeight?: number): void

Puts the [ImageData](ts-components-canvas-imagebitmap.md) onto a rectangular area on the canvas.

- Parameters
    | Name        | Type   | Mandatory | Default Value                      | Description                              |
    | ----------- | ------ | --------- | ---------------------------------- | ---------------------------------------- |
    | imagedata   | Object | Yes       | null                               | **ImageData** object with pixels to put onto the canvas. |
    | dx          | number | Yes       | 0                                  | X-axis offset of the rectangular area on the canvas. |
    | dy          | number | Yes       | 0                                  | Y-axis offset of the rectangular area on the canvas. |
    | dirtyX      | number | No        | 0                                  | X-axis offset of the upper left corner of the rectangular area relative to that of the source image. |
    | dirtyY      | number | No        | 0                                  | Y-axis offset of the upper left corner of the rectangular area relative to that of the source image. |
    | dirtyWidth  | number | No        | Width of the **ImageData** object  | Width of the rectangular area to crop the source image. |
    | dirtyHeight | number | No        | Height of the **ImageData** object | Height of the rectangular area to crop the source image. |

- Example

  ```
  @Entry
  @Component
  struct PutImageData {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            var imageData = this.offContext.createImageData(100, 100)
            for (var i = 0; i < imageData.data.length; i += 4) {
              imageData.data[i + 0] = 255
              imageData.data[i + 1] = 0
              imageData.data[i + 2] = 255
              imageData.data[i + 3] = 255
            }
            this.offContext.putImageData(imageData, 10, 10)
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001212058496](figures/en-us_image_0000001212058496.png)


### restore

restore(): void

Restores the saved drawing context.

- Example

  ```
  @Entry
  @Component
  struct CanvasExample {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.restore()
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```


### save

save(): void

Saves the current drawing context.

- Example

  ```
  @Entry
  @Component
  struct CanvasExample {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            this.offContext.save()
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
        })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```


### createLinearGradient

createLinearGradient(x0: number, y0: number, x1: number, y1: number): void

Creates a linear gradient.

- Parameters
    | Name | Type   | Mandatory | Default Value | Description                      |
    | ---- | ------ | --------- | ------------- | -------------------------------- |
    | x0   | number | Yes       | 0             | X-coordinate of the start point. |
    | y0   | number | Yes       | 0             | Y-coordinate of the start point. |
    | x1   | number | Yes       | 0             | X-coordinate of the end point.   |
    | y1   | number | Yes       | 0             | Y-coordinate of the end point.   |

- Example

  ```
  @Entry
  @Component
  struct CreateLinearGradient {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            var grad = this.offContext.createLinearGradient(50,0, 300,100)
            grad.addColorStop(0.0, 'red')
            grad.addColorStop(0.5, 'white')
            grad.addColorStop(1.0, 'green')
            this.offContext.fillStyle = grad
            this.offContext.fillRect(0, 0, 500, 500)
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001212378434](figures/en-us_image_0000001212378434.png)


### createRadialGradient

createRadialGradient(x0: number, y0: number, r0: number, x1: number, y1: number, r1: number): void

Creates a linear gradient.

- Parameters
    | Name | Type   | Mandatory | Default Value | Description                              |
    | ---- | ------ | --------- | ------------- | ---------------------------------------- |
    | x0   | number | Yes       | 0             | X-coordinate of the center of the start circle. |
    | y0   | number | Yes       | 0             | Y-coordinate of the center of the start circle. |
    | r0   | number | Yes       | 0             | Radius of the start circle, which must be a non-negative finite number. |
    | x1   | number | Yes       | 0             | X-coordinate of the center of the end circle. |
    | y1   | number | Yes       | 0             | Y-coordinate of the center of the end circle. |
    | r1   | number | Yes       | 0             | Radius of the end circle, which must be a non-negative finite number. |

- Example

  ```
  @Entry
  @Component
  struct CreateRadialGradient {
    private settings: RenderingContextSettings = new RenderingContextSettings(true)
    private context: CanvasRenderingContext2D = new CanvasRenderingContext2D(this.settings)
    
    private offContext: OffscreenCanvasRenderingContext2D = new OffscreenCanvasRenderingContext2D(600, 600, this.settings)
    build() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Canvas(this.context)
          .width('100%')
          .height('100%')
          .backgroundColor('#ffff00')
          .onReady(() =>{
            var grad = this.offContext.createRadialGradient(200,200,50, 200,200,200)
            grad.addColorStop(0.0, 'red')
            grad.addColorStop(0.5, 'white')
            grad.addColorStop(1.0, 'green')
            this.offContext.fillStyle = grad
            this.offContext.fillRect(0, 0, 500, 500)
            var image = this.offContext.transferToImageBitmap()
            this.context.transferFromImageBitmap(image)
          })
      }
      .width('100%')
      .height('100%')
    }
  }
  ```

  ![en-us_image_0000001212218480](figures/en-us_image_0000001212218480.png)


## CanvasPattern

Defines an object created by using the [createPattern](#createpattern) method.
