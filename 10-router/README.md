# Angular Router Demo

### Install Dependencies

-   Change directory to `calab`:
    ```
    cd calab
    ```
-   Install dependencies by running the following command:
    ```
    npm install
    ```

## Setup Application for Routing

### Create Two New Components

-   Create a new component using CLI and name it `First`:
    ```
    npx -p @angular/cli ng generate component components/first
    ```
-   Create another component using CLI and name it `Second`:
    ```
    npx -p @angular/cli ng generate component components/second
    ```

## Define and Use Your Routes

### Define Routes In Routes Array

- Open `src/app/app.routes.ts` file and do the following:
    - Import previously created components.
        ```
        import {FirstComponent} from './components/first/first.component';
        import {SecondComponent} from './components/second/second.component';
        ```
    - Define each route as an JavaScript object and add it to `Routes` array:
        ```
        { path: 'first-component', component: FirstComponent},
        { path: 'second-component', component: SecondComponent}
        ```

### Use Defined Routs In an Application

- Open `src/app/app.component.ts` file and do the following:
    - Import `RouterLink` from the `@angular/router`.
- Open `src/app/app.component.html` file and do the following:
    - Just below `<div class="divider"...` Use a routerLink attributes to add routes to selected elements:
        ```
         <nav>
            <ul>
                <li><a routerLink="/first-component/MyName" >First Component</a></li>
                <li><a routerLink="/second-component">Second Component</a></li>
            </ul>
        </nav>
        ```

### Start The Application

-   Start Angular Development Server if not yet started:
    ```
    npx -p @angular/cli ng serve  --host 0.0.0.0 
    ```
- Otherwise refresh the browser tab to see updated view.


## Bind Route Info to Component Inputs

### Enable Route Processing

- Open `src/app/app.config.ts` file and do the following:
    - Import `withComponentInputBinding` from the `@angular/router`.
    - update `provideRouter` method with the following:
        ```
          providers: [provideRouter(routes, withComponentInputBinding())]
        ```

### Update the component to have an Input matching the name of the parameter

-   Open `src/app/components/first/first.component.ts` and add the following code:
    ```
    @Component({
        selector: 'app-first',
        standalone: true,
        imports: [],
        templateUrl: './first.component.html',
        styleUrl: './first.component.css'
    })
    export class FirstComponent {
          @Input() name = '';
    }
    ```

### Update path in router array to include path parameter or query string.

- Open `src/app/app.routes.ts` file and do the following:
    - Update `first-component` path with the filowing:
        ```
        { path: 'first-component/:name', component: FirstComponent},
        { path: 'second-component', component: SecondComponent}
        ```
- Open `src/app/app.component.html` file and do the following:
    - Update a First Component's routerLink attribute to include name path parameter.:
        ```
        <li><a routerLink="/first-component/John" >First Component</a></li>
        ```

### Start The Application

-   Start Angular Development Server if not yet started:
    ```
    npx -p @angular/cli ng serve  --host 0.0.0.0 
    ```
- Otherwise refresh the browser tab to see updated view.

## Nesting Routes

### Create child components

- Create a new component using CLI and name it `FirstChild`:
    ```
    npx -p @angular/cli ng generate component components/first-child
    ```
- Add Styling to first child component:
    - Open `src/app/components/first-child/first-child.component.ts` and add replace current code with the following:
        ```
        <div class="container">
            <p>first-child works!</p>
        </div>
        ```
    - Open `src/app/components/first-child/first-child.component.html` and add the following css:
        ```
        .container {
            background-color: bisque;
            height: 100px;
        }
        ```
    
- Create another component using CLI and name it `SecondChild`:
    ```
    npx -p @angular/cli ng generate component components/second-child
    ```
- Add Styling to second child component:
    - Open `src/app/components/second-child/second-child.component.ts` and add replace current code with the following:
        ```
        <div class="container">
            <p>second-child works!</p>
        </div>
        ```
    - Open `src/app/components/second-child/second-child.component.html` and add the following css:
        ```
        .container {
            background-color:cadetblue;
            height: 100px;
        }
        ```

### Set Up Child Routes

- Open `src/app/app.routes.ts` file and do the following:
    - Import `FirstChildComponent` and `SecondChildComponent`.
    - Place child routes in a children array within the parent route:
        ```
        { path: 'second-component', component: SecondComponent, children: [
            {path: 'first-child', component: FirstChildComponent},
            {path: 'second-child', component: SecondChildComponent}
            ] 
        },
        ```

### Update Parent

- Open `src/app/components/second/second.component.ts` and add do the following:
    - import `RouterOutlet` and `RouterLink` from `@angular/router`. 
- Open `src/app/components/second/second.component.html` and add do the following:
    - Use a routerLink attributes to add routes to selected elements:
        ```
        <nav>
            <ul>
                <li><a routerLink="first-child">First Child</a></li>
                <li><a routerLink="second-child">Second Child</a></li>
            </ul>
        </nav>
        <router-outlet></router-outlet>
        ```
### Start The Application

-   Start Angular Development Server if not yet started:
    ```
    npx -p @angular/cli ng serve  --host 0.0.0.0 
    ```
- Otherwise refresh the browser tab to see updated view.