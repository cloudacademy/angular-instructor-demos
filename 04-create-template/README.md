# Ceate Angular Template

## 1. Setup Project

### Install Dependencies

1. Change directory to `calab`:

    ```.sh
    cd calab
    ```
2. Install dependencies by running the following command:

    ```.sh
    npm install
    ```

## 2. Create Component and Temlate

### 2.1 Create a new Component and a Template

1. Create a new `CustomInputComponent` component using CLI:

    ```.sh
    npx -p @angular/cli ng generate component custom-input
    ```

### 2.2 Inject CustomInput Component into AppComponent

1. Inside `src/app/app.component.ts` do the following:
    - Import `CustomInputComponent`:

    ```.js
    import { CustomInputComponent } from './custom-input/custom-input.component'; 
    ```

    - Update `imports` to include `CustomInputComponent`:

    ```.js
    imports: [RouterOutlet, CustomInputComponent],
    ```

2. Open `src/app/app.component.html` template and add the following element after the `<div class="divider"...`

    ```.html
    <app-custom-input></app-custom-input>
    ```

### 2.3 Start The Application

1. Start Angular Development Server if not yet started:

    ```.bash
    npx -p @angular/cli ng serve
    ```
    > _Otherwise refresh the browser tab to see updated view._

## 3. Data Binding Examples

### 3.1 Text Interpolation Example

1. Open `src/app/custom-input/custom-input.component.html` and replace current html content with the following:

    ```.html
    <p>{{value}}</p>
    ```

2. Open `src/app/custom-input/custom-input.component.ts` and add the following code:

    ```.js
    export class CustomInputComponent {
        value: string = "My Default Value"
    }
    ```

    > _Open your Angular application in Browser and see the result._

### 3.2 Event Binding Example
1. Open `src/app/custom-input/custom-input.component.html` and add the following line just above `<p>`:

    ```.html
    <input type="text" (input)="onInputChange($event)">
    ```

2. Open `src/app/custom-input/custom-input.component.ts` and add the following code inside CustomInputComponent class:

    ```.js
    onInputChange(event: any) {
        this.value = event.target.value;
    }
    ```
    
    > _Open your Angular application in Browser and see the result.
    Enter any value into the TextInput box and see how value chages on a screen._


### 3.3 Property Binding Example
1. Open `src/app/custom-input/custom-input.component.html` and update current HTML:
    - add value property to `<input>` element:

        ```.html
        <input type="text" [value]="value" (input)="onInputChange($event)">
        ```
        
    > _Open your Angular application in Browser (refresh page if needed) and see "My Default Value" being pre populated in  TextInput box._


### 3.4 Two Way Binding Example

1. Open `src/app/custom-input/custom-input.component.html` and remove current `<p>{{value}}</p>` from Template.:

2. Open `src/app/custom-input/custom-input.component.ts` and update to the following code:

    ```.js
    import { Component, EventEmitter, Input, Output } from '@angular/core';
        @Component({
            selector: 'app-custom-input',
            standalone: true,
            imports: [],
            templateUrl: './custom-input.component.html',
            styleUrl: './custom-input.component.css'
        })
        export class CustomInputComponent {
            @Input() value: string | undefined;
            @Output() valueChange = new EventEmitter<string>();

            onInputChange(event: any) {
                this.value = event.target.value;
                this.valueChange.emit(this.value);
            }
        }
    ```
3. Open `src/app/app.component.ts` and just below title variable add the following:

    ```.js
    inputValue: string = 'initial value';
    ```

4. Open `src/app/app.component.html` template and update/add the following element below the `<div class="divider"...`

    ```.html
    <app-custom-input [(value)]="inputValue"></app-custom-input>
    <p>Input value: {{ inputValue }}</p>
    ```

    > _Open your Angular application in Browser (refresh page if needed) and see how default value is set initialy, but later updated when 
    new value is typed into TextInput box._


### 3.5 Start The Application

1. Start Angular Development Server if not yet started:

    ```.bash
    npx -p @angular/cli ng serve
    ```
    > _Otherwise refresh the browser tab to see updated view._
