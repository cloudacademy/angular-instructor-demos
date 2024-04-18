# Ceate Angular Template

### Install Dependencies

-   Change directory to `calab`:
    ```
    cd calab
    ```
-   Install dependencies by running the following command:
    ```
    npm install

### Create a new Component and  Template

-   Create a new `CustomInputComponent` component using CLI:
    ```
    npx -p @angular/cli ng generate component my-component
    ```

### Inject CustomInput Component into AppComponent

- Inside `src/app/app.component.ts` update `imports` to include `CustomInputComponent`:
    ```
    imports: [RouterOutlet, CustomInputComponent],
    ```

- Open `src/app/app.component.html` template and add the following element after the `<div class="divider"...`
    ```
    <app-custom-input></app-custom-input>
    ```

### Start The Application

-   Start Angular Development Server:
    ```
    npx -p @angular/cli ng serve  --host 0.0.0.0 
    ```

### Text Interpolation Example

-   Open `src/app/custom-input/custom-input.component.html` and replace current html content with the following:
    ```
    <p>{{value}}</p>
    ```

-   Open `src/app/custom-input/custom-input.component.ts` and add the following code:
    ```
    export class CustomInputComponent {
        value: string = "My Default Value"
    }
    ```

    Open your Angular application in Browser and see the result.

### Event Binding Example
-   Open `src/app/custom-input/custom-input.component.html` and add the following line just above `<p>`:
    ```
    <input type="text" (input)="onInputChange($event)">

    ```

-   Open `src/app/custom-input/custom-input.component.ts` and add the following code inside CustomInputComponent class:
    ```
    onInputChange(event: any) {
        this.value = event.target.value;
    }
    ```
    
    Open your Angular application in Browser and see the result.
    Enter any value into the TextInput box and see how value chages on a screen.


### Property Binding Example
-   Open `src/app/custom-input/custom-input.component.html` and update current HTML:
    - add value property to `<input>` element:
        ```
        <input type="text" [value]="value" (input)="onInputChange($event)">
        ```
        
    Open your Angular application in Browser (refresh page if needed) and see "My Default Value" being pre populated in  TextInput box.


### Two Way Binding Example

-   Open `src/app/custom-input/custom-input.component.html` and remove current `<p>{{value}}</p>` from Template.:

-   Open `src/app/custom-input/custom-input.component.ts` and update to the following code:
    ```
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
-   Open `src/app/app.component.ts` and just below title variable add the following:
    ```
    inputValue: string = 'initial value';
    ```

- Open `src/app/app.component.html` template and update/add the following element below the `<div class="divider"...`
    ```
    <app-custom-input [(value)]="inputValue"></app-custom-input>
    <p>Input value: {{ inputValue }}</p>
    ```

    Open your Angular application in Browser (refresh page if needed) and see how default value is set initialy, but later updated when 
    new value is typed into TextInput box.
