# Create Angular Custom Pipe

### Install Dependencies

-   Change directory to `calab`:
    ```
    cd calab
    ```
-   Install dependencies by running the following command:
    ```
    npm install
    ```

### Create a new Pipe and Implement it's logic

-   Create a new `Reverse` pipe using CLI:
    ```
    npx -p @angular/cli ng generate pipe reverse
    ```
- Open `src/app/reverse.pipe.ts` file and replace current `transform` function with the following code:
    ```
    transform(value: string, ...args: unknown[]): unknown {
        return value.split("").reverse().join("");;
    }
    ```

### Inject ReversePipe into AppComponent

- Inside `src/app/app.component.ts` update `imports` to include `Reverse`:
    ```
    import {ReversePipe} from './reverse.pipe'
    ...
    imports: [RouterOutlet, ReversePipe],
    ```

### Start The Application

-   Start Angular Development Server:
    ```
    npx -p @angular/cli ng serve  --host 0.0.0.0 
    ```
- Inspect the Rendered Screen, you should see title `calab` being reversed.