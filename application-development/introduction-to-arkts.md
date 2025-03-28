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

[ArkTS Basics](/application-development/arkts-basics/index.md)  

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

#### Custom Component Layout

## State Management



## Event Binding



## Rendering Control




# Start Sample: Controlling Fan
We will use an example of controlling a fan to quick understand the knowledge.  

>[To do]: Add image about the application UI

