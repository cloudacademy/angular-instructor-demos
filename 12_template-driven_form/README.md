# Angular Template-driven Form Demo

### Install Dependencies

-   Change directory to `calab`:
    ```
    cd calab
    ```
-   Install dependencies by running the following command:
    ```
    npm install
    ```

## Create a Form Component

### Create a New Component

-   Create a new component using CLI and name it `OrderForm`:
    ```
    npx -p @angular/cli ng generate component components/order-form 
    ```
- Import `OrderForm` into `src/app/app.component.ts`:
    ```
    import { MyComponentComponent } from './my-component/my-component.component';
    ```

- Inside `src/app/app.component.ts` update `imports` to include `OrderForm`:
    ```
    imports: [RouterOutlet, OrderFormComponent],
    ```

- Open `src/app/app.component.html` template and add the following element after the `<div class="divider"...`
    ```
    <app-order-form></app-order-form>
    ```


## Setup Template-driven Form in OrderFormComponent

### Update Component

- Open `src/app/components/order-form/order-form.component.ts` file and do the following:
    -  Update `imports` to include `FormsModule`:
        ```
        @Component({
            ...
            imports: [FormsModule],
            ...
        })
        ```
### Create The Form Template
-  Open `src/app/components/order-form/order-form.component.html` file and do the following:
    - Create a form template.
        ```
        <form>
            <label for="product">Product:</label>
            <input type="text" id="product" name="product" required>
            <label for="quantity">Quantity:</label>
            <input type="text" id="quantity" name="quantity" required>
            <button type="submit">Submit</button>
        </form>
        ```
-  Open `src/app/components/order-form/order-form.component.css` file and do the following:
    - Add some style.
        ```
        /* Style inputs */
        input, select {
            width: 100%;
            padding: 12px 20px;
            margin: 8px 0;
            display: inline-block;
            border: 1px solid #ccc;
            border-radius: 4px;
            box-sizing: border-box;
        }

        /* Style the submit button */
        button[type=submit] {
            width: 100%;
            background-color: #04AA6D;
            color: white;
            padding: 14px 20px;
            margin: 8px 0;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }

        /* Add a background color to the submit button on mouse-over */
        button[type=submit]:hover {
            background-color: #45a049;
        }

        .ng-valid[required], .ng-valid.required  {
            border-left: 5px solid #42A948; /* green */
        }
        .ng-invalid:not(form)  {
            border-left: 5px solid #a94442; /* red */
        }
        ```

### Data Bind With ngModel

- Create a new class inside `src/app/components/order-form/` representing an Order Model.
    ```
    export class Order {
        constructor(
            public product: string,
            public quantity?: number,
        ) {}
    }
    ```

- Open `src/app/components/order-form/order-form.component.ts` file and do the following:
    -  Declare a model that you want to bind to the template:
        ```
          order = new Order('');
        ```
        - default product set to empty string.
-  Open `src/app/components/order-form/order-form.component.html` file and do the following:
    - update a form template with the following:
        ```
        <form>
            <label for="product">Product:</label>
            <input type="text" id="product" name="product" required [(ngModel)]="order.product">
            <label for="quantity">Quantity:</label>
            <input type="text" id="quantity" name="quantity" required [(ngModel)]="order.quantity">
            <button type="submit">Submit</button>
        </form>
        ```

### Submitting the Form

- Open `src/app/components/order-form/order-form.component.ts` file and do the following:
    -  Create an onSubmit() callback method, allowing you to process the captured form data as needed:
        ```
        onSubmit(){
            console.log(this.order);
        }
        ```

-  Open `src/app/components/order-form/order-form.component.html` file and do the following:
    - Add an ngSubmit event listener to the form tag with the onSubmit() callback method:
        ```
        <form (ngSubmit)="onSubmit()">
        ...

        ```

## Template-driven Form Validation

### Show And Hide Validation Error Messages
-  Open `src/app/components/order-form/order-form.component.html` file and do the following:
    - Add a local reference to the input `#product="ngModel"`
        ```
        <input type="text" id="product" name="product" required [(ngModel)]="order.product" #product="ngModel">
        ```
    - Add a conditional error message to product
        ```
        <div [hidden]="product.valid || product.pristine">
            Product name is required
        </div>        
        ```


### Start The Application

-   Start Angular Development Server if not yet started:
    ```
    npx -p @angular/cli ng serve  --host 0.0.0.0 
    ```
- Otherwise refresh the browser tab to see updated view.