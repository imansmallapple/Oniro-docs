**Content Table:**
[Introduction](#introduction)  

[Basic Syntax Overview](#basic-syntax-overview)  

[Key Features](#key-features)  
- [Declarative UI](#declarative-ui)  
- [Componentization](#componentization)  
    - [Basic Component](#basic-component)  
    - [Custom Component](#custom-component)  
- [State Management](#state-management)  
- [Event Binding](#event-binding)  
- [Rendering Control](#rendering-control)  

[ArkTS Basics](/application-development/arkts-basics.md)  

[Start Sample: Controlling Fan]()  

# Introduction
Welcome to the tutorial for ArkTS, a TypeScript-based programming language designed specifically to build high-performance mobile applications.

ArkTS is optimized to provide better performance and efficiency, while still maintaining the familiar syntax of TypeScript.

# Basic Syntax Overview  
[Text Source](https://gitee.com/openharmony/docs/blob/master/en/application-dev/quick-start/arkts-basic-syntax-overview.md)
With a basic understanding of the ArkTS language, let's look into the composition of ArkTS through an example. As shown below, when the user clicks the button, the text content changes from Hello World to Hello ArkUI.  

  **Figure 1** Example effect drawing 
    <img src='/application-development/image-basic/v1.gif'>

In this example, the basic composition of ArkTS is as follows.


  **Figure 2** Basic composition of ArkTS 
    <img src='/application-development/image-basic/image3.png'>

> **NOTE**
>
> The name of a custom variable cannot be the same as that of any universal attribute or event.


- **Decorator**: design pattern used to decorate classes, structs, methods, and variables to assign special meanings to them. In the preceding sample code, `@Entry`, `@Component`, and `@State` are decorators. 
  - `@Component` indicates a custom component
  - `@Entry` indicates that the custom component is an entry component
  - `@State` indicates a state variable in the component, whose change will trigger the UI to re-render.

- **UI description**: declarative description of the UI structure, such as the code block of the **build()** method.

- **Custom component**: reusable UI unit, which can be used with other components, such as the struct **Hello** decorated by @Component.

- **Built-in component**: default basic or container component preset in ArkTS, which can be directly invoked, such as **Column**, **Text**, **Divider**, and **Button** components in the sample code.

- **Attribute method**: method used to configure component attributes, such as **fontSize()**, **width()**, **height()**, and **backgroundColor()**. You can configure multiple attributes of a component in method chaining mode.

- **Event method**: method used to add the logic for a component to respond to an event. In the sample code, **onClick()** following **Button** is an event method. You can configure response logic for multiple events in method chaining mode.

# Key Features
## Declarative UI
[Text Source](https://gitee.com/openharmony/docs/blob/master/en/application-dev/quick-start/arkts-declarative-ui-description.md)  
ArkTS declaratively combines and extends components to describe the UI of an application. It also provides basic methods for configuring attributes, events, and child components to help you implement application interaction logic.

### Creating a Component

Depending on the builder, you can create components with or without mandatory parameters.

>  **NOTE**
>  The **new** operator is not required when you create a component.

#### Without Mandatory Parameters
A struct without mandatory parameters is a component defined with empty parentheses. For example, the Divider component:

```ts
Column() {
  Text('item 1')
  Divider()
  Text('item 2')
}
```

#### With Mandatory Parameters

A struct with mandatory parameters is a component whose API definition expects parameters enclosed in parentheses.

- Set the mandatory parameter **src** of the **Image** component as follows:

  ```ts
  Image('https://xyz/test.jpg')
  ```

- Set the optional parameter **content** of the **Text** component.

  ```ts
  // Parameter of the string type
  Text('test')
  // Add application resources in $r format, which can be used in multi-language scenarios.
  Text($r('app.string.title_value'))
  // No mandatory parameters
  Text()
  ```

- You can also use variables or expressions to assign values to parameters. The result type returned by an expression must meet the parameter type requirements.
    For example, to set a variable or expression to construct the **Image** and **Text** components:

    ```ts
    Image(this.imagePath)
    Image('https://' + this.imageUrl)
    Text(`count: ${this.count}`)
    ```



### Configuring Attributes

Use chainable attribute methods to configure the style and other attributes of built-in components. It is recommended that a separate line be used for each attribute method.


- Example of configuring the **fontSize** attribute for the **Text** component:

  ```ts
  Text('test')
    .fontSize(12)
  ```

- Example of configuring multiple attributes for the **Image** component:

  ```ts
  Image('test.jpg')
    .alt('error.jpg')    
    .width(100)    
    .height(100)
  ```

- Attribute methods accept expressions and variables as well constant parameters.

  ```ts
  Text('hello')
    .fontSize(this.size)
  Image('test.jpg')
    .width(this.count % 2 === 0 ? 100 : 200)    
    .height(this.offset + 100)
  ```

- For built-in components, ArkUI also predefines some enumeration types. These enumeration types can be passed as parameters, as long as they meet the parameter type requirements.
  Example of configuring the font color and style of the **Text** component:

  ```ts
  Text('hello')
    .fontSize(20)
    .fontColor(Color.Red)
    .fontWeight(FontWeight.Bold)
  ```


### Handling Events

Use chainable event methods to configure events supported by built-in components. It is recommended that a separate line be used for each event method.


- Example of using an arrow function expression to configure the event of a component:

  ```ts
  Button('Click me')
    .onClick(() => {
      this.myText = 'ArkUI';
    })
  ```

- Example of using an arrow function expression to configure the event of a component (**() => {...}** must be used to ensure that the function is bound to the component and complies with the ArkTS syntax specifications):

  ```ts
  Button('add counter')
    .onClick(() => {
      this.counter += 2;
    })
  ```

- Example of using a component's member function to configure the event of the component, where **this** binding is needed: (This usage is not recommended in ArkTS.)

  ```ts
  myClickHandler(): void {
    this.counter += 2;
  }
  ...
  Button('add counter')
    .onClick(this.myClickHandler.bind(this))
  ```

- Example of using an arrow function expression for a declaration, where **this** binding is not needed:

  ```ts
  fn = () => {
    console.info(`counter: ${this.counter}`)
    this.counter++
  }
  ...
  Button('add counter')
    .onClick(this.fn)
  ```

> **NOTE**
> In arrow functions, **this** inherits its value from the surrounding (lexical) scope in which they are defined. This means that, in anonymous functions, **this** may present an unclear reference and is therefore not allowed in ArkTS.


### Configuring Child Components

For a component with child components, for example, a container component, add the UI descriptions of the child components inside parentheses. The **Column**, **Row**, **Stack**, **Grid**, and **List** components are all container components.


- Simple example of configuring child components for the **Column** component:

  ```ts
  Column() {
    Text('Hello')
      .fontSize(100)
    Divider()
    Text(this.myText)
      .fontSize(100)
      .fontColor(Color.Red)
  }
  ```

- Example of nested child components in the **Column** component:.

  ```ts
  Column() {
    Row() {
      Image('test1.jpg')
        .width(100)
        .height(100)
      Button('click +1')
        .onClick(() => {
          console.info('+1 clicked!');
        })
    }
  }
  ```

## Componentization
Components are the fundamental building blocks of a user interface. Everything you see on the screen is created by combining multiple components. Designing a user interface is essentially about assembling these components in a meaningful way. ArkTS provides a wide range of built-in components, such as `Text`, `Button`, and `Image`. Moreover, it allows developers to create custom components to better suit specific requirements.
### Basic Component
#### Row Component

The **<Row\>** component lays out child components horizontally.

>  **NOTE**
>
>  This component is supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.


##### Child Components
Supported

##### APIs

Row(value?:{space?:  number | string })

This API can be used in ArkTS widgets since API version 9.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| space | number \| string | No| Horizontal spacing between two adjacent child components.<br>Since API version 9, this parameter does not take effect when it is set to a negative number or when **justifyContent** is set to **FlexAlign.SpaceBetween**, **FlexAlign.SpaceAround** or **FlexAlign.SpaceEvenly**.<br>Default value: **0**, in vp<br>**NOTE**<br>The value can be a number greater than or equal to 0 or a string that can be converted to a number.|


##### Attributes

| Name| Type| Description|
| -------- | -------- | -------- |
| alignItems | VerticalAlign | Alignment mode of child components in the vertical direction.<br>Default value: **VerticalAlign.Center**<br>This API can be used in ArkTS widgets since API version 9.|
| justifyContent | FlexAlign | Alignment mode of the child components in the horizontal direction.<br>Default value: **FlexAlign.Start**<br>This API can be used in ArkTS widgets since API version 9.|

>  **NOTE**   
>
>  During row layout, child components do not shrink if flexShrink is not set for them. In this case, the total size of the child components on the main axis can exceed the size of the container on the main axis.

##### Example

```ts
// xxx.ets
@Entry
@Component
struct RowExample {
  build() {
    Column({ space: 5 }) {
      // Set the horizontal spacing between two adjacent child components to 5.
      Text('space').width('90%')
      Row({ space: 5 }) {
        Row().width('30%').height(50).backgroundColor(0xAFEEEE)
        Row().width('30%').height(50).backgroundColor(0x00FFFF)
      }.width('90%').height(107).border({ width: 1 })

      // Set the alignment mode of the child components in the vertical direction.
      Text('alignItems(Bottom)').width('90%')
      Row() {
        Row().width('30%').height(50).backgroundColor(0xAFEEEE)
        Row().width('30%').height(50).backgroundColor(0x00FFFF)
      }.width('90%').alignItems(VerticalAlign.Bottom).height('15%').border({ width: 1 })

      Text('alignItems(Center)').width('90%')
      Row() {
        Row().width('30%').height(50).backgroundColor(0xAFEEEE)
        Row().width('30%').height(50).backgroundColor(0x00FFFF)
      }.width('90%').alignItems(VerticalAlign.Center).height('15%').border({ width: 1 })

      // Set the alignment mode of the child components in the horizontal direction.
      Text('justifyContent(End)').width('90%')
      Row() {
        Row().width('30%').height(50).backgroundColor(0xAFEEEE)
        Row().width('30%').height(50).backgroundColor(0x00FFFF)
      }.width('90%').border({ width: 1 }).justifyContent(FlexAlign.End)

      Text('justifyContent(Center)').width('90%')
      Row() {
        Row().width('30%').height(50).backgroundColor(0xAFEEEE)
        Row().width('30%').height(50).backgroundColor(0x00FFFF)
      }.width('90%').border({ width: 1 }).justifyContent(FlexAlign.Center)
    }.width('100%')
  }
}
```

<img src='/application-development/image-basic/image4.png'>

#### Column

The **<Column\>** component lays out child components vertically.

>  **NOTE**
>
>  This component is supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.

##### Child Components

Supported


##### APIs

Column(value?: {space?: string | number})

This API can be used in ArkTS widgets since API version 9.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| space | string \| number | No| Vertical spacing between two adjacent child components.<br>Since API version 9, this parameter does not take effect when it is set to a negative number or when **justifyContent** is set to **FlexAlign.SpaceBetween**, **FlexAlign.SpaceAround** or **FlexAlign.SpaceEvenly**.<br>Default value: **0**<br>Unit: vp<br>**NOTE**<br>The value can be a number greater than or equal to 0 or a string that can be converted to a number.|

##### Attributes

| Name| Type| Description|
| -------- | -------- | -------- |
| alignItems | HorizontalAlign | Alignment mode of the child components in the horizontal direction.<br>Default value: **HorizontalAlign.Center**<br>This API can be used in ArkTS widgets since API version 9.|
| justifyContent | FlexAlign | Alignment mode of the child components in the vertical direction.<br>Default value: **FlexAlign.Start**<br>This API can be used in ArkTS widgets since API version 9.|

>  **NOTE**   
>
>  During column layout, child components do not shrink if flexShrink is not set for them. In this case, the total size of the child components on the main axis can exceed the size of the container on the main axis.

##### Example

```ts
// xxx.ets
@Entry
@Component
struct ColumnExample {
  build() {
    Column({ space: 5 }) {
      // Set the vertical spacing between two adjacent child components to 5.
      Text('space').width('90%')
      Column({ space: 5 }) {
        Column().width('100%').height(30).backgroundColor(0xAFEEEE)
        Column().width('100%').height(30).backgroundColor(0x00FFFF)
      }.width('90%').height(100).border({ width: 1 })

      // Set the alignment mode of the child components in the horizontal direction.
      Text('alignItems(Start)').width('90%')
      Column() {
        Column().width('50%').height(30).backgroundColor(0xAFEEEE)
        Column().width('50%').height(30).backgroundColor(0x00FFFF)
      }.alignItems(HorizontalAlign.Start).width('90%').border({ width: 1 })

      Text('alignItems(End)').width('90%')
      Column() {
        Column().width('50%').height(30).backgroundColor(0xAFEEEE)
        Column().width('50%').height(30).backgroundColor(0x00FFFF)
      }.alignItems(HorizontalAlign.End).width('90%').border({ width: 1 })

      Text('alignItems(Center)').width('90%')
      Column() {
        Column().width('50%').height(30).backgroundColor(0xAFEEEE)
        Column().width('50%').height(30).backgroundColor(0x00FFFF)
      }.alignItems(HorizontalAlign.Center).width('90%').border({ width: 1 })

      // Set the alignment mode of the child components in the vertical direction.
      Text('justifyContent(Center)').width('90%')
      Column() {
        Column().width('90%').height(30).backgroundColor(0xAFEEEE)
        Column().width('90%').height(30).backgroundColor(0x00FFFF)
      }.height(100).border({ width: 1 }).justifyContent(FlexAlign.Center)

      Text('justifyContent(End)').width('90%')
      Column() {
        Column().width('90%').height(30).backgroundColor(0xAFEEEE)
        Column().width('90%').height(30).backgroundColor(0x00FFFF)
      }.height(100).border({ width: 1 }).justifyContent(FlexAlign.End)
    }.width('100%').padding({ top: 5 })
  }
}
```

<img src='/application-development/image-basic/image5.png'>

You can learn more about basic components [here](/application-development/basic-components/component-overview.md).

### Custom Component
In ArkUI, components are the visual elements of the interface, divided into built-in components provided by the framework and custom components created by developers. Relying solely on built-in components can lead to rigid, hard-to-maintain designs. Custom components help improve code reusability, separate UI from business logic, and support version upgrades. They offer key features such as:
- **Combinable**: Combine built-in and custom components with shared properties and methods.

- **Reusable**: Easily reused across different parts of the app.

- **Data-driven updates**: Maintain internal state and update the UI when state changes.

#### Create a Custom Component

##### Basic Usage of Custom Component
The following example shows the basic usage of a custom component.
```ts
 // xxx.ets
@Component
struct HelloComponent {
  @State message: string = 'Hello, World!';

  build() {
    // The HelloComponent custom component combines the <Row> and <Text> built-in components.
    Row() {
      Text(this.message)
        .onClick(() => {
          // The change of the state variable message drives the UI to be re-rendered. As a result, the text changes from "Hello, World!" to "Hello, ArkUI!".
          this.message = 'Hello, ArkUI!';
        })
    }
  }
}
```
On `Previewer`, click `Hello, World!`, the text will change into `Hello, ArkUI!`.
<div style="text-align:center">
    <img src='/application-development/image-basic/image6.png' width=40%>
    <img src='/application-development/image-basic/image7.png'
    width=40%>
</div> 

> **NOTE**
>
> To reference the custom component in another file, use the keyword **export** to export the component and then use **import** to import it to the target file.

Multiple **HelloComponent** instances can be created in **build()** of other custom components. In this way, **HelloComponent** is reused by those custom components.


```ts
@Entry
@Component
struct ParentComponent {
  build() {
    Column() {
      Text('ArkUI message')
      HelloComponent({ message: 'Hello World!' });
      Divider()
      HelloComponent({message: 'Hello, World!'});
    }
  }
}
```
<div style="text-align:center">
    <img src='/application-development/image-basic/image8.png' width=60%>
</div> 

##### Basic Structure of a Custom Component
Basic structure are listed below:
- **struct**
The definition of a custom component must start with the \@Component struct followed by the component name, and then component body enclosed by curly brackets. No inheritance is allowed. You can omit the **new** operator when instantiating a struct.

  > **NOTE**
  >
  > The name or its class or function name of a custom component must be different from that of any built-in components.

- **@Component**
The \@Component decorator can decorate only the structs declared by the **struct** keyword. When being decorated by \@Component, a struct has the componentization capability. You must implement the **build** function for it to describe the UI. Each struct can be decorated by only one \@Component. \@Component can accept an optional parameter of the Boolean type.

  > **NOTE**
  >
  > This decorator can be used in ArkTS widgets since API version 9.
  > 
  > An optional parameter of the Boolean type can be used in the \@Component since API version 11.

  ```ts
  @Component
  struct MyComponent {
  }
  ```
- **The build Function**
The **build** function is used to define the declarative UI description of a custom component. Every custom component must define a **build** function.

  ```ts
  @Component
  struct MyComponent {
    build() {
    }
  }
  ```

- **@Entry**
A custom component decorated with \@Entry is used as the default entry component of the page. Only one component can be decorated with \@Entry in a single page. The \@Entry decorator accepts an optional parameter of type **LocalStorage**.

  > **NOTE**
  >
  > This decorator can be used in ArkTS widgets since API version 9.
  >
  > Since API version 10, the \@Entry decorator accepts an optional parameter of type **LocalStorage** or type **EntryOptions**.
  >
  > This decorator can be used in atomic services since API version 11.

  ```ts
  @Entry
  @Component
  struct MyComponent {
  }
  ```

- **@Reusable**
Custom components decorated by \@Reusable can be reused.

  > **NOTE**
  >
  > This decorator can be used in ArkTS widgets since API version 10.

  ```ts
  @Reusable
  @Component
  struct MyComponent {
  }
  ```

##### Rules for Custom Component Parameters

As can be learnt from preceding examples, a custom component can be created from a build method. During the creation, the custom component's parameters are initialized based on the decorator rules.

```ts
@Component
struct MyComponent {
  private countDownFrom: number = 0;
  private color: Color = Color.Blue;

  build() {
  }
}

@Entry
@Component
struct ParentComponent {
  private someColor: Color = Color.Pink;

  build() {
    Column() {
      // Create an instance of MyComponent and initialize its countDownFrom variable with the value 10 and its color variable with the value this.someColor.
      MyComponent({ countDownFrom: 10, color: this.someColor })
    }
  }
}
```
In the following example, a function in the parent component is passed to the child component and called there.

```ts
@Entry
@Component
struct Parent {
  @State cnt: number = 0
  submit: () => void = () => {
    this.cnt++;
  }

  build() {
    Column() {
      Text(`${this.cnt}`)
      Son({ submitArrow: this.submit })
    }
  }
}

@Component
struct Son {
  submitArrow?: () => void

  build() {
    Row() {
      Button('add')
        .width(80)
        .onClick(() => {
          if (this.submitArrow) {
            this.submitArrow()
          }
        })
    }
    .height(56)
  }
}
```
Click the button defined in `Son`, `Text` result will be updated in `Parent`.
<div style="text-align:center">
    <img src='/application-development/image-basic/image9.png' width=40%>
    <img src='/application-development/image-basic/image10.png' width=40%>
</div> 

##### Rules in build Function
Whatever declared in build() are called UI descriptions. UI descriptions must comply with the following rules:
- For an \@Entry decorated custom component, exactly one root component is required under **build()**. This root component must be a container component. **ForEach** is not allowed at the top level. For an \@Component decorated custom component, exactly one root component is required under **build()**. This root component is not necessarily a container component. **ForEach** is not allowed at the top level.
  ```ts
  @Entry
  @Component
  struct MyComponent {
    build() {
      // Exactly one root component is required, and it must be a container component.
      Row() {
        ChildComponent() 
      }
    }
  }
  
  @Component
  struct ChildComponent {
    build() {
      // Exactly one root component is required, and it is not necessarily a container component.
      Image('test.jpg')
    }
  }
  ```

- Local variable declaration is not allowed. The following example should be avoided:

  ```ts
  build() {
    // Avoid: declaring a local variable.
    let num: number = 1;
  }
  ```

- `console.info` can be used in the UI description only when it is in a method or function. The following example should be avoided:

  ```ts
  build() {
    // Avoid: using console.info directly in UI description.
    console.info('print debug log');
  }
  ```

- Creation of a local scope is not allowed. The following example should be avoided:

  ```ts
  build() {
    // Avoid: creating a local scope.
    {
      // ...
    }
  }
  ```

- Only methods decorated by \@Builder can be called. The parameters of built-in components can be the return values of TS methods.

  ```ts
  @Component
  struct ParentComponent {
    doSomeCalculations() {
    }

    calcTextValue(): string {
      return 'Hello World';
    }

    @Builder doSomeRender() {
      Text(`Hello World`)
    }

    build() {
      Column() {
        // Avoid: calling a method not decorated by @Builder.
        this.doSomeCalculations();
        // Prefer: Call an @Builder decorated method.
        this.doSomeRender();
        // Prefer: Pass the return value of a TS method as the parameter.
        Text(this.calcTextValue())
      }
    }
  }
  ```

- The **switch** syntax is not allowed. If conditional judgment is required, use the **if** statement. Refer to the code snippet below.

  ```ts
  build() {
    Column() {
      // Avoid: using the switch syntax.
      switch (expression) {
        case 1:
          Text('...')
          break;
        case 2:
          Image('...')
          break;
        default:
          Text('...')
          break;
      }
      // Correct usage: Use if.
      if(expression == 1) {
        Text('...')
      } else if(expression == 2) {
        Image('...')
      } else {
        Text('...')
      }
    }
  }
  ```

- Expressions are not allowed except for the **if** component. Refer to the code snippet below.

  ```ts
  build() {
    Column() {
      // Avoid: expressions.
      (this.aVar > 10) ? Text('...') : Image('...')

      // Positive example: Use if for judgment.
      if(this.aVar > 10) {
        Text('...')
      } else {
        Image('...')
      }
    }
  }
  ```

- Directly changing a state variable is not allowed. The following example should be avoided:

  ```ts
  @Component
  struct MyComponent {
    @State textColor: Color = Color.Yellow;
    @State columnColor: Color = Color.Green;
    @State count: number = 1;
    build() {
      Column() {
        // Avoid: directly changing the value of count in the <Text> component.
        Text(`${this.count++}`)
          .width(50)
          .height(50)
          .fontColor(this.textColor)
          .onClick(() => {
            this.columnColor = Color.Red;
          })
        Button("change textColor").onClick(() =>{
          this.textColor = Color.Pink;
        })
      }
      .backgroundColor(this.columnColor)
    }
  }
  ```
In ArkUI state management, UI re-render is driven by state.
<div style="text-align:center">
    <img src='/application-development/image-basic/image11.png' width=40%>
</div> 
 Therefore, do not change any state variable in the **build()** or \@Builder decorated method of a custom component. Otherwise, loop rendering may result.

##### Universal Style of a Custom Component
The universal style of a custom component is configured by the chain call.
```ts
@Component
struct ChildComponent {
  build() {
    Button(`Hello World`)
  }
}

@Entry
@Component
struct MyComponent {
  build() {
    Row() {
      ChildComponent()
        .width(200)
        .height(300)
        .backgroundColor(Color.Red)
    }
  }
}
```
<div style="text-align:center">
    <img src='/application-development/image-basic/image12.png' width=40%>
</div> 

> **NOTE**
>
> When ArkUI sets styles for custom components, an invisible container component is set for **ChildComponent**. These styles are set on the container component instead of the **Button** component of **ChildComponent**. As seen from the rendering result, the red background color is not directly applied to the button. Instead, it is applied to the container component that is invisible to users where the button is located.

#### Page and Custom Component Lifecycle

Before we dive into the page and custom component lifecycle, it would be helpful to learn the relationship between custom **components** and **pages**.

- Custom component: \@Component decorated UI unit, which can combine multiple built-in components for component reusability and invoke component lifecycle callbacks.

- Page: UI page of an application. A page can consist of one or more custom components. A custom component decorated with `@Entry` is used as the entry component of the page. Exactly one component is decorated with \@Entry in a single source file. Only components decorated by \@Entry can invoke the lifecycle callbacks of a page.


The following lifecycle callbacks are provided for a page, that is, a custom component decorated with \@Entry:


- **onPageShow**: Invoked each time the page is displayed, for example, during page redirection or when the application is switched to the foreground.

- **onPageHide**: Invoked each time the page is hidden, for example, during page redirection or when the application is switched to the background.

- **onBackPress**: Invoked when the user clicks the **Back** button.


The following lifecycle callbacks are provided for a custom component decorated with \@Component:


- **aboutToAppear**: Invoked when the custom component is about to appear. Specifically, it is invoked after a new instance of the custom component is created and before its **build** function is executed.

- **aboutToDisappear**: Invoked when the custom component is about to be destroyed. Do not change state variables in the **aboutToDisappear** function as doing this can cause unexpected errors. For example, the modification of the **@Link** decorated variable may cause unstable application running.


The following figure shows the lifecycle of a component (page) decorated with \@Entry.


<div style="text-align:center">
    <img src='/application-development/image-basic/image13.png'>
</div>

The following example shows when the lifecycle callbacks are invoked:

```ts
// Index.ets
import router from '@ohos.router';

@Entry
@Component
struct MyComponent {
  @State showChild: boolean = true;
  @State btnColor:string = "#FF007DFF"

  // Only components decorated by @Entry can call the lifecycle callbacks of a page.
  onPageShow() {
    console.info('Index onPageShow');
  }
  // Only components decorated by @Entry can call the lifecycle callbacks of a page.
  onPageHide() {
    console.info('Index onPageHide');
  }

  // Only components decorated by @Entry can call the lifecycle callbacks of a page.
  onBackPress() {
    console.info('Index onBackPress');
    this.btnColor ="#FFEE0606"
    return true // The value true means that the page executes its own return logic instead of the , and false (default) means that the default return logic is used.
  }

  // Component lifecycle
  aboutToAppear() {
    console.info('MyComponent aboutToAppear');
  }

  // Component lifecycle
  aboutToDisappear() {
    console.info('MyComponent aboutToDisappear');
  }

  build() {
    Column() {
      // When this.showChild is true, create the Child child component and invoke Child aboutToAppear.
      if (this.showChild) {
        Child()
      }
      // When this.showChild is false, delete the Child child component and invoke Child aboutToDisappear.
      Button('delete Child')
      .margin(20)
      .backgroundColor(this.btnColor)
      .onClick(() => {
        this.showChild = false;
      })
      // Push to the page and execute onPageHide.
      Button('push to next page')
        .onClick(() => {
          router.pushUrl({ url: 'pages/page' });
        })
    }

  }
}

@Component
struct Child {
  @State title: string = 'Hello World';
  // Component lifecycle
  aboutToDisappear() {
    console.info('[lifeCycle] Child aboutToDisappear')
  }

  aboutToAppear() {
    console.info('[lifeCycle] Child aboutToAppear')
  }

  build() {
    Text(this.title).fontSize(50).margin(20).onClick(() => {
      this.title = 'Hello ArkUI';
    })
  }
}
```
```ts
// page.ets
@Entry
@Component
struct page {
  @State textColor: Color = Color.Black;
  @State num: number = 0

  onPageShow() {
    this.num = 5
  }

  onPageHide() {
    console.log("page onPageHide");
  }

  onBackPress() {// If the value is not set, false is used.
    this.textColor = Color.Grey
    this.num = 0
  }

  aboutToAppear() {
    this.textColor = Color.Blue
  }

  build() {
    Column() {
      Text (`num: ${this.num}`)
        .fontSize(30)
        .fontWeight(FontWeight.Bold)
        .fontColor(this.textColor)
        .margin(20)
        .onClick(() => {
          this.num += 5
        })
    }
    .width('100%')
  }
}
```

In the preceding example, the **Index** page contains two custom components. One is **MyComponent** decorated with \@Entry, which is also the entry component (root node) of the page. The other is **Child**, which is a child component of **MyComponent**. Only components decorated by \@Entry can call the page lifecycle callbacks. Therefore, the lifecycle callbacks of the **Index** page – **onPageShow**, **onPageHide**, and **onBackPress**, are declared in **MyComponent**. In **MyComponent** and its child components, component lifecycle callbacks – **aboutToAppear** and **aboutToDisappear** –  are also declared.


- The initialization process of application cold start is as follows: MyComponent aboutToAppear -> MyComponent build -> Child aboutToAppear -> Child build -> Child build execution completed -> MyComponent build execution completed -> Index onPageShow

- When **delete Child** is clicked, the value of **this.showChild** linked to **if** changes to **false**. As a result, the **Child** component is deleted, and the **Child aboutToDisappear** callback is invoked.


- When **push to next page** is clicked, the **router.pushUrl** API is called to jump to the next page. As a result, the **Index** page is hidden, and the **Index onPageHide** callback is invoked. As the called API is **router.pushUrl**, which results in the Index page being hidden, but not destroyed, only the **onPageHide** callback is invoked. After a new page is displayed, the process of initializing the lifecycle of the new page is executed.

- If **router.replaceUrl** is called, the **Index** page is destroyed. In this case, the execution of lifecycle callbacks changes to: Index onPageHide -> MyComponent aboutToDisappear -> Child aboutToDisappear. As aforementioned, a component is destroyed by directly removing it from the component tree. Therefore, **aboutToDisappear** of the parent component is called first, followed by **aboutToDisappear** of the child component, and then the process of initializing the lifecycle of the new page is executed.

- When the **Back** button is clicked, the **Index onBackPress** callback is invoked, and the current **Index** page is destroyed.

- When the application is minimized or switched to the background, the **Index onPageHide** callback is invoked. As the current **Index** page is not destroyed, **aboutToDisappear** of the component is not executed. When the application returns to the foreground, the **Index onPageShow** callback is invoked.


- When the application exits, the following callbacks are executed in order: Index onPageHide -> MyComponent aboutToDisappear -> Child aboutToDisappear.

#### More Usage
- [Custom Component Layout](/application-development/custom-component-layout.md)  
- [Freezing a Custom Component](/application-development/freezing-custom-component.md)

## State Management
In previous examples, most of the pages built are static pages, which are delivered to the end user without having to be processed. If you are building dynamic, interactive pages, you need to handle **state management**.

  **Figure 1:** State managed UI 

<div style="text-align:center">
    <img src='/application-development/image-basic/v1.gif'>
</div>


In the preceding example, the interaction between the user and the application triggers an update in the text state, which in turn triggers re-rendering of the UI. As a result, the **Hello World** text changes to **Hello ArkUI**.


In the declarative UI framework, the UI is the execution result of the application state. You build a UI model in which the application runtime state is a parameter. When the parameter is changed, the UI as the return result is updated accordingly. This process of UI re-rendering caused by the application runtime state changes is called the state management mechanism in ArkUI.


Custom components have variables. A variable must be decorated by a decorator whenever the re-rendering of the UI depends on this variable. Otherwise, the UI is rendered only at initialization and will not be updated. The following figure shows the relationship between the state and view (UI).

<div style="text-align:center">
    <img src='/application-development/image-basic/image14.png'>
</div>


- View (UI): UI rendering, which is visual representation of the UI description in the **build** method and \@Builder decorated method.

- State: data that drives the UI to re-render. State data is changed by invoking the event method of the component. The change of the state data triggers the re-rendering of the UI.

### Basic Concepts

- State variable: a variable decorated by a state decorator. Its value change will trigger UI re-renders. Example: @State num: number = 1, where @State is a state decorator and **num** is a state variable.

- Regular variable: a variable that is not decorated by a state decorator and is usually used for auxiliary calculation. Its value change will not trigger UI re-renders. In the following example, the **increaseBy** variable is a regular variable.

- Data source/Synchronization source: original source of a state variable, which can be synchronized to different state data. Generally, it is the data passed from the parent component to the child component. In the following example, the data source is **count: 1**.

- Named parameter mechanism: a mechanism where the parent component passes state variables to the child component by specifying parameters. It is the primary means of passing synchronization parameters from the parent component to the child component. Example: CompA: ({ aProp: this.aProp }).

- Initialization from the parent component: a process where the parent component uses the named parameter mechanism to pass specified parameters to the child component. The default value used in local initialization will be overwritten by the value passed from the parent component. Example:

  ```ts
  @Component
  struct MyComponent {
    @State count: number = 0;
    private increaseBy: number = 1;

    build() {
    }
  }

  @Component
  struct Parent {
    build() {
      Column() {
        // Initialization from the parent component: The named parameter specified here will overwrite the default value defined locally.
        MyComponent({ count: 1, increaseBy: 2 })
      }
    }
  }
  ```

- Child component initialization: a capability to pass state variables to the child component to initialize the corresponding state variables therein. The example is the same as above.

- Local initialization: a process where a value is assigned to a variable as its default value in the variable declaration. Example: \@State count: number = 0.


## Decorator Overview

ArkUI provides a diverse array of decorators. You can use these decorators to observe state variables changes within a component or globally and pass the changes between different component levels (for example, between parent and child components or grandparent and grandchild components). According to the scope of the state variable, decorators can be roughly classified into the following types:


- Decorators for managing the state of a component: implement state management at the component level by allowing for observation of state changes within a component and changes at different component levels. The observation is limited to state changes in the same component tree, that is, on the same page.

- Decorators for managing the state of an application: implement global state management of an application by allowing for observation of state changes on different pages or even different UIAbility components.


According to the data transfer mode and synchronization type, decorators can also be classified into the following types:


- Decorators that allow for one-way (read-only) transfer

- Decorators that allow for two-way (mutable) transfer


The following figure illustrates the decorators. For details, see [Component State Management](arkts-state.md) and [Application State Management](arkts-application-state-management-overview.md). You can use these decorators at your disposal to implement linkage between data and the UI.


![en-us_image_0000001502704640](figures/en-us_image_0000001502704640.png)


In the preceding figure, the decorators in the Components area are used for state management at the component level, while others are used for state management at the application level. You can use [@StorageLink](arkts-appstorage.md#storagelink)/[@LocalStorageLink](arkts-localstorage.md#localstoragelink) to implement two-way synchronization of the application and component state, and [@StorageProp](arkts-appstorage.md#storageprop)/[@LocalStorageProp](arkts-localstorage.md#localstorageprop) to implement one-way synchronization.


Decorators for [component state management](arkts-state.md):


- [\@State](arkts-state.md): An \@State decorated variable holds the state of the owning component. It can be the source of one- or two-way synchronization with child components. When the variable changes, the dependent component will be updated. 

- [\@Prop](arkts-prop.md): An \@Prop decorated variable can create one-way synchronization with a variable of its parent component. \@Prop decorated variables are mutable, but changes are not synchronized to the parent component.

- [\@Link](arkts-link.md): An \@Link decorated variable creates two-way synchronization with a variable of its parent component. When the @Link decorated variable has its value changed, its source is updated as well; when the source updates, the @Link decorated variable will do as well.

- [\@Provide/\@Consume](arkts-provide-and-consume.md): Variables decorated by \@Provide/\@Consume are used for data synchronization across component levels. The components can be bound to the variables through aliases or attribute names. Data does not need to be passed through the named parameter mechanism.

- [\@Observed](arkts-observed-and-objectlink.md): \@Observed is a class decorator. You can use it to decorate the class that has multiple levels of nested objects or arrays to be observed. Note that \@Observed must be used with \@ObjectLink for two-way synchronization or with \@Prop for one-way synchronization.

- [\@ObjectLink](arkts-observed-and-objectlink.md): An \@ObjectLink decorated variable is used with an \@Observed decorated class of the parent component for two-way data synchronization. It is applicable in scenarios involving multiple levels of nested objects or arrays in the class.

> **NOTE**
>
> Only [\@Observed/\@ObjectLink](arkts-observed-and-objectlink.md) can be used to observe changes of nested attributes. Other decorators can be used to observe changes of attributes at the first layer only. For details, see the "Observed Changes and Behavior" part in each decorator section.


Decorators for [application state management](arkts-state.md):


- [AppStorage](arkts-appstorage.md): a special [LocalStorage](arkts-localstorage.md) singleton instance. It is an application-wide database bound to the application process and can be linked to components through the [@StorageProp](arkts-appstorage.md#storageprop) and [@StorageLink](arkts-appstorage.md#storagelink) decorators.

- AppStorage is the hub for application state. Data that needs to interact with components (UI) is stored in AppStorage, including [PersistentStorage](arkts-persiststorage.md) and [Environment](arkts-environment.md) data. The UI accesses the data through the decorators or APIs provided by AppStorage.

- LocalStorage: an in-memory "database" for the application state declared by the application and typically used to share state across pages. It can be linked to the UI through the [@LocalStorageProp](arkts-localstorage.md#localstorageprop) and [@LocalStorageLink](arkts-localstorage.md#localstoragelink) decorators.


### Other State Management Features

[\@Watch](arkts-watch.md): listens for the changes of state variables.


[$$operator](arkts-two-way-sync.md): provides a TS variable by-reference to a built-in component so that the variable value and the internal state of that component are kept in sync.

## Event Binding



## Rendering Control




# Start Sample: Controlling Fan
We will use an example of controlling a fan to quick understand the knowledge.  

>[To do]: Add image about the application UI

