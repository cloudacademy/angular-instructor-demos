# Create Angular Custom Pipe

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

## 2. Create Pipe

### 2.1 Create a new Pipe and Implement it's logic

1. Create a new `Reverse` pipe using CLI:

    ```.sh
    npx -p @angular/cli ng generate pipe reverse
    ```
2. Open `src/app/reverse.pipe.ts` file and replace current `transform` function with the following code:

    ```.js
    transform(value: string, ...args: unknown[]): unknown {
        return value.split("").reverse().join("");
    }
    ```

### 2.2 Inject ReversePipe into AppComponent

1. Inside `src/app/app.component.ts` update `imports` to include `Reverse`:

    ```.js
    import {ReversePipe} from './reverse.pipe'
    ...
    imports: [RouterOutlet, ReversePipe],
    ```

1. Inside `src/app/app.component.html` use ReversePipe:

    ```.html
    <h1>Hello, {{ title | reverse }}</h1>
    ```

### 2.3 Start The Application

1. Start Angular Development Server if not yet started:

    ```.bash
    npx -p @angular/cli ng serve 
    ```
    > _Otherwise refresh the browser tab to see updated view._

 2. Inspect the Rendered Screen, you should see title `calab` being reversed.