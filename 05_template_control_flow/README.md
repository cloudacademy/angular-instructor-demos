# Angular Template Control Flow Demo

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

### Capture User Input
-   Open `src/app/custom-input/custom-input.component.html` and add replace current HTML with the following:
    ```
    <input type="text" (input)="onInputChange($event)">
    ```

-   Open `src/app/custom-input/custom-input.component.ts` and add the following code inside CustomInputComponent class:
    ```
    onInputChange(event: any) {
        this.value = event.target.value;
    }
    ```


