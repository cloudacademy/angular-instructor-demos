# Angular Template Control Flow Demo

## 1. Setup Project

### 1.1 Install Dependencies

1. Change directory to `calab`:

    ```.sh
    cd calab
    ```
2. Install dependencies by running the following command:

    ```.sh
    npm install
    ```

## 2. Create Component and Template

### 2.1 Create a new Component and  Template

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


## 3. Capture User Input and Update View Based On Users Value

### 3.1 Capture User Input
1. Open `src/app/custom-input/custom-input.component.html` and replace current HTML with the following:

    ```.html
    <input type="text" (input)="onInputChange($event)">
    ```

2. Open `src/app/custom-input/custom-input.component.ts` and add the following code inside CustomInputComponent class:

    ```.js
    import { Component } from '@angular/core';

    @Component({
        selector: 'app-custom-input',
        standalone: true,
        imports: [],
        templateUrl: './custom-input.component.html',
        styleUrl: './custom-input.component.css'
    })
    export class CustomInputComponent {
        value: string = ''

        onInputChange(event: any) {
            this.value = event.target.value;
        }
    }
    ```

### 3.2 Add @if built-in control flow block

1. Open `src/app/custom-input/custom-input.component.html` and add the following code just below the `<input>` element:

    ```.html
    <div>
        @if (!value || value.length < 5) {
            Type at least 5 characters
        } @else {
            Perfect :)
        }
    </div>
    ```

### 3.3 Start The Application

1. Start Angular Development Server if not yet started:

    ```.bash
    npx -p @angular/cli ng serve
    ```
    > _Otherwise refresh the browser tab to see updated view._
