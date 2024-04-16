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

-   Start Angular Development Server:
    ```
    npx -p @angular/cli ng serve  --host 0.0.0.0 
    ```


    ```
    <app-my-component></app-my-component>
    ```

    ```
    import { MyComponentComponent } from './my-component/my-component.component';
    ```

    ```
    imports: [RouterOutlet, MyComponentComponent],
    ```
