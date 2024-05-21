# Communication Between Angular Components

### Install Dependencies

-   Change directory to `calab`:
    ```
    cd calab
    ```
-   Install dependencies by running the following command:
    ```
    npm install

### Create Child Component

-   Create a new `Child` component using CLI:
    ```
    npx -p @angular/cli ng generate component child
    ```
-   Open `src/app/child/child.component.ts` and add the following code:
    ```
    import { Component, EventEmitter, Input, Output } from '@angular/core';
    @Component({
        selector: 'app-child',
        standalone: true,
        imports: [],
        templateUrl: './child.component.html',
        styleUrl: './child.component.css'
    })
    export class ChildComponent {
        @Input() message: string | undefined;
        @Output() messageEvent = new EventEmitter<string>();

        sendMessage() {
            this.messageEvent.emit('Message from child to parent');
        }
    }
    ```
-   Open `src/app/child/child.component.html` and replace current html content with the following. Mention that we will cover Templates in more depth in next Topic:
    ```
    <h3>Child Component</h3>
    <p>{{ message }}</p>
    <button (click)="sendMessage()">Send Message to Parent</button> 
    ```


### Create Prent Component

-   Create a new `Parent` component using CLI:
    ```
    npx -p @angular/cli ng generate component parent
    ```
- Open `src/app/parent/paret.component.ts` and add the following code:
    ```
    import { Component } from '@angular/core';
    import { ChildComponent } from '../child/child.component';

    @Component({
        selector: 'app-parent',
        standalone: true,
        imports: [ChildComponent],
        templateUrl: './parent.component.html',
        styleUrl: './parent.component.css'
    })
    export class ParentComponent {
        parentMessage = "Message from parent to child";
        childMessage: string | undefined;

        receiveMessage($event: any) {
            this.childMessage = $event;
        }
    }
    ```
-   Open `src/app/parent/parent.component.html` and replace current html content with the following:
    ```
    <h2>Parent Component</h2>
    <app-child-component [message]="parentMessage" (messageEvent)="receiveMessage($event)"></app-child-component>
    <p>{{ childMessage }}</p>
    ```


### Inject Parent component into AppComponent

- Inside `src/app/app.component.ts` update `imports` to include `ParentComponent`:
    ```
    imports: [RouterOutlet, ParentComponent],
    ```

- Open `src/app/app.component.html` template and add the following element after the `<div class="divider"...`
    ```
    <app-parent></app-parent>
    ```

### Start The Application

-   Start Angular Development Server:
    ```
    npx -p @angular/cli ng serve  --host 0.0.0.0 
    ```