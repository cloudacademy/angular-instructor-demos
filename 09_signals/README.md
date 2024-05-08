# Angular Signals Demo

### Install Dependencies

-   Change directory to `calab`:
    ```
    cd calab
    ```
-   Install dependencies by running the following command:
    ```
    npm install
    ```

## Creating a Signal

### Create new Signal
- Open `src/app/app.component.ts` file and do the following:
    - Import signal form `'@angular/core'`.
    - Inside `constructor` of `AppComponent` create a new signal and assign it to a variable:
        ```
        const quantity = signal(0);
        ```
    
### Read value from the Signal
- Open `src/app/app.component.ts` file and do the following:
    - Import effect form `'@angular/core'`.
    - Inside `constructor` of `AppComponent`, just below Signal, call an effect and log the Signal value:
        ```
        effect(() => {
            console.log(`The current quantity is: ${quantity()}`);
        });
        ```

### Update Signal value
- Open `src/app/app.component.ts` file and do the following:
    - Inside `constructor` of `AppComponent`, just below the effect, set new value to the Signal:
        ```
        quantity.set(1);
        ```
    - Now use alternative approach to change value in Signal called `update`:
        ```
        quantity.update(value => value + 1);
        ```

## toSignal Example

### Create an Observable 
- Open `src/app/app.component.ts` file and do the following:
    - Import `Observable` form `rxjs`.
    - Replace code inside `constructor` of `AppComponent`to the following:
        ```
        let increasingQuantity = new Observable<number>(observer => {
            let curVal = 0;
            setInterval(() => observer.next(curVal +=1), 5000);
        });
        ```

### Convert Observable to Signal
- Continue working with `src/app/app.component.ts` file:
    - Import `toSignal` form `@angular/core/rxjs-interop`.
    - Just below previously declared Observable, add the following:
        ```
        let increasingQuantitySignal = toSignal(increasingQuantity, {initialValue: 0});
        ```

### Read value from the newly converted Signal
- Continue working with `src/app/app.component.ts` file:
    - Import effect form `'@angular/core'`.
    - Inside `constructor` of `AppComponent`, just below Signal, call an effect and log the Signal value:
        ```
        effect(() => {
            console.log(`The current quantity is: ${increasingQuantitySignal()}`);
        });
        ```

## toObservable Example

### Create a Signal 
- Open `src/app/app.component.ts` file and do the following:
    - Import `signal` form `@angular/core`.
    - Replace code inside `constructor` of `AppComponent`to the following:
        ```
        let quantity = signal(0);
        ```

### Convert Signal to Observable
- Continue working with `src/app/app.component.ts` file:
    - Import `toObservable` form `@angular/core/rxjs-interop`.
    - Just below previously declared Signal, add the following:
        ```
        let quantityObservable = toObservable(quantity);
        ```

### Subscribe to observable to get async updates
- Continue working with `src/app/app.component.ts` file:
    - Just below previously converted signal into observable add the following:
        ```
        quantityObservable.subscribe({
            next: (v) => console.log(`Subscriber: The current quantity is: ${v}`),
            error: (e) => console.error(e),
            complete: () => console.info('complete') 
        });        
        ```
