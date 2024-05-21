# Create Angular Custom Directive

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

## 2. Create Directive

### 2.1 Create a new Directive and Implement it's logic

1. Create a new `IsAuth` directive using CLI:

    ```.sh
    npx -p @angular/cli ng generate directive is-auth
    ```
2. Open `src/app/is-auth.directive.ts` file and do the following:
    - Import TemplateRef, and ViewContainerRef from @angular/core.
    - Update current `constructor` with following parameters:

        ```.js
        constructor(private templateRef: TemplateRef<any>, private viewContainer: ViewContainerRef) { 
        }
        ```

### 2.2 Implement @Input property 

1. Open `src/app/is-auth.directive.ts` file and do the following:
    - Import Input from @angular/core.
    - Define an input property `appIsAuth` with a setter. This allows you to pass a condition to the directive from the template.

        ```.js
        @Input() set appIsAuth(condition: boolean) {
            if (condition) {
            this.viewContainer.createEmbeddedView(this.templateRef);
            } else {
            this.viewContainer.clear();
            }
        }
        ```
        > _Use the setter to conditionally create or clear the embedded view in the ViewContainerRef based on the provided condition._

## 3. Use Directive

### 3.1 Apply the Directive using Long-form syntax
1. Open `src/app/is-auth.directive.html` file and do the following:
    - Inside `<div class="content">` insert the following:

        ```.html
        <!-- Long-form syntax: -->
        <ng-template [appIsAuth]="true">
            <p>You have access to privileged information.</p>
        </ng-template>
        ```
        > _In this example, the content within the `<p>` will only be rendered if the appIsAuth property in the component is true. Otherwise, the content will not be displayed._


### 3.2 Apply the Directive using Short-form syntax
1. Open `src/app/is-auth.directive.html` file and do the following:
    - Inside `<div class="content">` insert the following

        ```.html
        <!-- Shorthand syntax: -->
        <p *appIsAuth="true">You have access to privileged information.</p>
        ```
        > _In this example, the content within the `<p>` will only be rendered if the appIsAuth property in the component is true. Otherwise, the content will not be displayed._

### 3.3 Start The Application

1. Start Angular Development Server if not yet started:

    ```.bash
    npx -p @angular/cli ng serve  --host 0.0.0.0 
    ```
    > _Otherwise refresh the browser tab to see updated view._

2. Inspect the Rendered Screen, you should see title `calab` being reversed.