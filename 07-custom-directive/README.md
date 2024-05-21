# Create Angular Custom Directive

### Install Dependencies

-   Change directory to `calab`:
    ```
    cd calab
    ```
-   Install dependencies by running the following command:
    ```
    npm install
    ```

### Create a new Directive and Implement it's logic

-   Create a new `IsAuth` directive using CLI:
    ```
    npx -p @angular/cli ng generate directive is-auth
    ```
- Open `src/app/is-auth.directive.ts` file and do the following:
    - Import TemplateRef, and ViewContainerRef from @angular/core.
    - Update current `constructor` with following parameters:
        ```
        constructor(private templateRef: TemplateRef<any>, private viewContainer: ViewContainerRef) { 
        }
        ```

### Implement @Input property 

- Open `src/app/is-auth.directive.ts` file and do the following:
    - Import Input from @angular/core.
    - Define an input property `appIsAuth` with a setter. This allows you to pass a condition to the directive from the template.
        ```
        @Input() set appIsAuth(condition: boolean) {
            if (condition) {
            this.viewContainer.createEmbeddedView(this.templateRef);
            } else {
            this.viewContainer.clear();
            }
        }
        ```
        - Use the setter to conditionally create or clear the embedded view in the ViewContainerRef based on the provided condition.

### Apply the Directive using Long-form syntax
- Open `src/app/is-auth.directive.html` file and do the following:
    - Inside `<div class="content">` insert the following

    ```
    <!-- Long-form syntax: -->
    <ng-template [appIsAuth]="true">
        <p>You have access to privileged information.</p>
    </ng-template>
    ```
    - In this example, the content within the <p> will only be rendered if the appIsAuth property in the component is true. Otherwise, the content will not be displayed. 


### Apply the Directive using Short-form syntax
- Open `src/app/is-auth.directive.html` file and do the following:
    - Inside `<div class="content">` insert the following

    ```
    <!-- Shorthand syntax: -->
    <p *appIsAuth="true">You have access to privileged information.</p>
    ```

    - In this example, the content within the <p> will only be rendered if the appIsAuth property in the component is true. Otherwise, the content will not be displayed. 

### Start The Application

-   Start Angular Development Server:
    ```
    npx -p @angular/cli ng serve  --host 0.0.0.0 
    ```
- Inspect the Rendered Screen, you should see title `calab` being reversed.