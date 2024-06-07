# Angular Reactive Form Demo

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

## 2. Create a Form Component

### 2.1 Create a New Component

1. Create a new component using CLI and name it `OrderForm`:

    ```.sh
    npx -p @angular/cli ng generate component components/order-form 
    ```
2. Import `OrderForm` into `src/app/app.component.ts`:

    ```.js
    import { OrderFormComponent } from './components/order-form/order-form.component';
    ```

3. Inside `src/app/app.component.ts` update `imports` to include `OrderForm`:

    ```.js
    imports: [RouterOutlet, OrderFormComponent],
    ```

4. Open `src/app/app.component.html` template and add the following element after the `<div class="divider"...`:

    ```.html
    <app-order-form></app-order-form>
    ```

### 2.2 Review Changes

1. Start Angular Development Server if not yet started:

    ```.bash
    npx -p @angular/cli ng serve
    ```
    > _Otherwise refresh the browser tab to see updated view._
2. You should see placeholder for `OrderForm` component rendered on a screen.
 

## 3. Setup Reactive Form in OrderFormComponent

### 3.1 Update Component

1. Open `src/app/components/order-form/order-form.component.ts` file and do the following:

    - Import `ReactiveFormsModule` and `FormControl`:
        ```.js
        import { FormControl, ReactiveFormsModule } from '@angular/forms';
        ```

    - Update `imports` to include `ReactiveFormsModule`:

        ```.js
        @Component({
            ...
            imports: [ReactiveFormsModule],
            ...
        })
        ```
    - Create FormControl instancess inside your OrderFormComponent.

        ```.js
        product = new FormControl('');
        quantity = new FormControl('');
        ```

2. Open `src/app/components/order-form/order-form.component.html` file and do the following:
    - Register controls in the template.

        ```.html
        <label for="product">Product: </label>
        <input id="product" type="text" [formControl]="product">

        <label for="quantity">Quantity: </label>
        <input id="quantity" type="text" [formControl]="quantity">
        ```
3. Open `src/app/components/order-form/order-form.component.css` file and do the following:
    - Add some style.

        ```.css
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

### 3.2 Review Changes

1. Start Angular Development Server if not yet started:

    ```.bash
    npx -p @angular/cli ng serve
    ```
    > _Otherwise refresh the browser tab to see updated view._
2. You should see `OrderForm` rendered on a screen.

## 4. Displaying a Form Control Value

### 4.1 Update Component

1. Open `src/app/components/order-form/order-form.component.ts` file and do the following:
    -  Subscribe to the valueChanges observable:

        ```.js
        ngOnInit() { 
            this.product.valueChanges.subscribe(data => console.log(`Product updated to ${data}`))
            this.quantity.valueChanges.subscribe(data => console.log(`Quantity updated to ${data}`))
        }
        ```
2. Open `src/app/components/order-form/order-form.component.html` file and do the following:
    - Access the current value directly through the value property.

        ```.html
        <p>Current Product: {{product.value}}</p>
        <p>Current Quantity: {{quantity.value}}</p>
        ```

### 4.2 Review Changes

1. Start Angular Development Server if not yet started:

    ```.bash
    npx -p @angular/cli ng serve
    ```
    > _Otherwise refresh the browser tab to see updated view._
2. Inspect developer console if using Chrome for any logs. You should see the following geting printed once values A and B typed in a form:
    ```.sh
    Product updated to A
    Quantity updated to B
    ```

## 5. Grouping Form Controls

### 5.1 Create A FormGroup Instance
1. Open `src/app/components/order-form/order-form.component.ts` file and do the following:
    -  Create a FormGroup instance. 
        - Import `FormGroup`:

            ```.js
            import { FormControl, FormGroup, ReactiveFormsModule } from '@angular/forms';
            ```

        - Replace current code in OrderFormComponent class with the following:

            ```.js
            orderForm = new FormGroup({
                product: new FormControl(''),
                quantity: new FormControl(''),
            });
            ```
2. Open `src/app/components/order-form/order-form.component.html` file and do the following:
    - Associate The FormGroup Model And View. Replace current HTML code with the following:

        ```.html
        <form [formGroup]="orderForm">
            <label for="product">Product: </label>
            <input id="product" type="text" formControlName="product">
            <label for="quantity">Quantity: </label>
            <input id="quantity" type="text" formControlName="quantity">
        </form>
        ```

### 5.2 Save form Data
1. Open `src/app/components/order-form/order-form.component.ts` file and do the following:
    -  create an onSubmit() callback method, allowing you to process the captured form data as needed:

        ```.js
        onSubmit() {
            // TODO: Use EventEmitter with form value
            console.warn(this.orderForm.value);
        }
        ```
2. Open `src/app/components/order-form/order-form.component.html` file and do the following:
    - Add an ngSubmit event listener to the form tag with the onSubmit() callback method:

        ```.html
        <form [formGroup]="orderForm" (submit)="onSubmit()">
            ...
        </form>
        ```
    - Use button within <form> element to trigger Submit event:

        ```.html
        <form [formGroup]="orderForm" (submit)="onSubmit()">
            ... // form elements
            <button type="submit">Submit</button>
        </form>
        ```

### 5.3 Review Changes

1. Start Angular Development Server if not yet started:

    ```.bash
    npx -p @angular/cli ng serve
    ```
    > _Otherwise refresh the browser tab to see updated view._
2. Inspect developer console if using Chrome for any logs. You should see the following geting printed once values A and B typed in a form and Submit button is clicked:
    ```.sh
    {product: 'A', quantity: 'B'}
    ```

### 5.4 Use FormBuilder Service
1. Open `src/app/components/order-form/order-form.component.ts` file and do the following:
    - Import `FormBuilder` and `FormArray`:

        ```.js
        import { FormBuilder, FormArray, ReactiveFormsModule } from '@angular/forms';
        ```

    -  Inject the `FormBuilder` service into your component using dependency injection:

        ```.js
        constructor(private formBuilder: FormBuilder){}
        ```
    - Replace FormGroup with FormBuilder:

        ```.js
        orderForm = this.formBuilder.group({
            product: [''],
            quantity: [''],
        });
        ```

### 5.5 Define A FormArray Control
1. Open `src/app/components/order-form/order-form.component.ts` file and do the following:
    - Add new property to your existing FormGroup:

        ```.js
        instructions: this.formBuilder.array([this.formBuilder.control('')])
        ``` 

    - Create a getter that provides an efficient way to access the values in your form array instance:

        ```.js
        get instructions() {
            return this.orderForm.get('instructions') as FormArray;
        }
        ```

    - Define a method to dynamically add an alias control to your form array:

        ```.js
        addInstruction(){
            this.instructions.push(this.formBuilder.control(''));
        }
        ```

2. Open `src/app/components/order-form/order-form.component.html` file and do the following:
    - Integrate the form model's interests into your template:

    ```.html
    <form [formGroup]="orderForm" (submit)="onSubmit()">
        ... //form controls
        <div formArrayName="instructions">
            <h2>Instructions</h2>
            <button type="button" (click)="addInstruction()">+ Add Instruction</button>
            @for (instruction of instructions.controls; track instruction; let i = $index) {
            <div>
                <label for="instruction-{{ i }}">Instruction:</label>
                <input id="instruction-{{ i }}" type="text" [formControlName]="i">
            </div>
            }
        </div>
        ... //submit button
    </form>
    ```

### 5.6 Review Changes

1. Start Angular Development Server if not yet started:

    ```.bash
    npx -p @angular/cli ng serve
    ```
    > _Otherwise refresh the browser tab to see updated view._
2. Your form should now allow you to add instructions.

## 6. Reactive Form Validation

### 6.1 Built-in Validators
1. Open `src/app/components/order-form/order-form.component.ts` file and do the following:
    - Import `Validators`:

        ```.js
        import { FormBuilder, FormArray, ReactiveFormsModule, Validators } from '@angular/forms';
        ```

    - Add required validators to product and quantity form controls. Update orderForm with the following:

        ```.js
        orderForm = this.formBuilder.group({
            product: ['', Validators.required],
            quantity: ['', Validators.required],
            instructions: this.formBuilder.array([this.formBuilder.control('')])
        });

        ``` 

### 6.2 Custom Validators
1. Open `src/app/components/order-form/order-form.component.ts` file and do the following:
    - Import `ValidatorFn`, `AbstractControl` and `ValidationErrors`:

        ```.js
        import { FormBuilder, FormArray, ReactiveFormsModule, Validators, ValidatorFn, AbstractControl, ValidationErrors } from '@angular/forms';
        ```

    - Create a new method that validates agains list of forbidden product names:

        ```.js
          forbiddenNameValidator(): ValidatorFn {
            return (control: AbstractControl): ValidationErrors | null => {
                const list = ['Lightsaber', 'Millennium Falcon'];
                const forbidden = list.includes(control.value);
                return forbidden ? {forbiddenName: {value: control.value}} : null;
            };
        }
        ```

    - Add forbiddenNameValidator to product form controls. 

        ```.js
        product: ['', [Validators.required, this.forbiddenNameValidator()]],
        ```


### 6.3 Review Changes

1. Start Angular Development Server if not yet started:

    ```.bash
    npx -p @angular/cli ng serve
    ```
    > _Otherwise refresh the browser tab to see updated view._