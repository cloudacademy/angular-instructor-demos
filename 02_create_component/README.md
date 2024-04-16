# Create a New Angular Component

### Install Dependencies

-   Change directory to `calab`:
    ```
    cd calab
    ```
-   Install dependencies by running the following command:
    ```
    npm install
    ```

### Create Angular Component
-   Create a new component using CLI:
    ```
    npx -p @angular/cli ng generate component my-component
    ```

- Import `MyComponentComponent` into `src/app/app.component.ts`:
    ```
    import { MyComponentComponent } from './my-component/my-component.component';
    ```

- Inside `src/app/app.component.ts` update `imports` to include `MyComponentComponent`:
    ```
    imports: [RouterOutlet, MyComponentComponent],
    ```

- Open `src/app/app.component.html` template and add the following element after the `<div class="divider"...`
    ```
    <app-my-component></app-my-component>
    ```

-   Start Angular Development Server:
    ```
    npx -p @angular/cli ng serve  --host 0.0.0.0 
    ```