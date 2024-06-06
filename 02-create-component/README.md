# Create a New Angular Component

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

## 2. Create Component

### 2.1 Create Angular Component
1. Create a new component using CLI:

    ```.sh
    npx -p @angular/cli ng generate component my-component
    ```

2. Import `MyComponentComponent` into `src/app/app.component.ts`:

    ```.js
    import { MyComponentComponent } from './my-component/my-component.component';
    ```

3. Inside `src/app/app.component.ts` update `imports` to include `MyComponentComponent`:

    ```.js
    imports: [RouterOutlet, MyComponentComponent],
    ```

4. Open `src/app/app.component.html` template and add the following element after the `<div class="divider"...`

    ```.html
    <app-my-component></app-my-component>
    ```

### 2.2 Start The Application

1. Start Angular Development Server if not yet started:

    ```.bash
    npx -p @angular/cli ng serve 
    ```
    > _Otherwise refresh the browser tab to see updated view._
