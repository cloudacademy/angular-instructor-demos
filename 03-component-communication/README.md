# Communication Between Angular Components

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

## 2. Create Child and Parent Components

### 2.1 Create Child Component

1. Create a new `Child` component using CLI:

    ```.sh
    npx -p @angular/cli ng generate component child
    ```
2. Open `src/app/child/child.component.ts` and add the following code:

    ```.js
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
3. Open `src/app/child/child.component.html` and replace current html content with the following. Mention that we will cover Templates in more depth in next Topic:

    ```.html
    <h3>Child Component</h3>
    <p>{{ message }}</p>
    <button (click)="sendMessage()">Send Message to Parent</button> 
    ```


### 2.2 Create Prent Component

1. Create a new `Parent` component using CLI:

    ```.sh
    npx -p @angular/cli ng generate component parent
    ```
2. Open `src/app/parent/paret.component.ts` and add the following code:

    ```.js
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
3. Open `src/app/parent/parent.component.html` and replace current html content with the following:

    ```.html
    <h2>Parent Component</h2>
    <app-child [message]="parentMessage" (messageEvent)="receiveMessage($event)"></app-child>
    <p>{{ childMessage }}</p>
    ```


### 2.3 Inject Parent component into AppComponent

1. Inside `src/app/app.component.ts` do the following:
    - Import `ParentComponent`:

        ```.js
        import { ParentComponent } from './parent/parent.component';
        ```
    - Update `imports` to include `ParentComponent`:

        ```.js
        imports: [RouterOutlet, ParentComponent],
        ```

2. Open `src/app/app.component.html` template and add the following element after the `<div class="divider"...`

    ```.html
    <app-parent></app-parent>
    ```

### 2.4 Start The Application

1. Start Angular Development Server if not yet started:

    ```.bash
    npx -p @angular/cli ng serve
    ```
    > _Otherwise refresh the browser tab to see updated view._
