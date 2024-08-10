Lifecycle hooks in Angular are methods that allow you to tap into specific points in a component or directive's lifecycle. These hooks give you the ability to perform actions or execute code at various stages of a component's or directive's existence, from initialization to destruction.

Here's a brief overview of the main lifecycle hooks:

1. **`ngOnInit()`**: Called once, after the first `ngOnChanges()` (if there are any bindings) and before the component is rendered. Ideal for initializing component properties and fetching data.

2. **`ngOnChanges(changes: SimpleChanges)`**: Called before `ngOnInit()` and whenever an input property changes. It receives a `SimpleChanges` object that contains the previous and current values of the changed properties.

3. **`ngDoCheck()`**: Called during every change detection run. It's used for custom change detection logic.

4. **`ngAfterContentInit()`**: Called once after the component's content (ng-content) has been projected into the view.

5. **`ngAfterContentChecked()`**: Called after every check of the component’s content.

6. **`ngAfterViewInit()`**: Called once after the component's view and child views are initialized. Useful for interacting with child components and DOM elements.

7. **`ngAfterViewChecked()`**: Called after every check of the component’s view and child views.

8. **`ngOnDestroy()`**: Called just before the component or directive is destroyed. Ideal for cleanup logic, such as unsubscribing from observables or detaching event handlers.

Sure! Here are practical examples for each of the Angular lifecycle hooks:

1. **`ngOnInit()`**: 
   ```typescript
   import { Component, OnInit } from '@angular/core';

   @Component({
     selector: 'app-example',
     template: `<p>Data loaded: {{data}}</p>`
   })
   export class ExampleComponent implements OnInit {
     data: string;

     ngOnInit() {
       // Fetch data from a service
       this.data = 'Data fetched during initialization';
     }
   }
   ```

2. **`ngOnChanges(changes: SimpleChanges)`**:
   ```typescript
   import { Component, Input, OnChanges, SimpleChanges } from '@angular/core';

   @Component({
     selector: 'app-example',
     template: `<p>Input changed: {{inputValue}}</p>`
   })
   export class ExampleComponent implements OnChanges {
     @Input() inputValue: string;

     ngOnChanges(changes: SimpleChanges) {
       if (changes['inputValue']) {
         console.log('Input value changed:', changes['inputValue'].currentValue);
       }
     }
   }
   ```

3. **`ngDoCheck()`**:
   ```typescript
   import { Component, DoCheck } from '@angular/core';

   @Component({
     selector: 'app-example',
     template: `<p>Check log for changes</p>`
   })
   export class ExampleComponent implements DoCheck {
     ngDoCheck() {
       console.log('ngDoCheck called');
       // Perform custom change detection
     }
   }
   ```

4. **`ngAfterContentInit()`**:
   ```typescript
   import { Component, AfterContentInit } from '@angular/core';

   @Component({
     selector: 'app-example',
     template: `<ng-content></ng-content>`
   })
   export class ExampleComponent implements AfterContentInit {
     ngAfterContentInit() {
       console.log('Content projected into the view');
     }
   }
   ```

5. **`ngAfterContentChecked()`**:
   ```typescript
   import { Component, AfterContentChecked } from '@angular/core';

   @Component({
     selector: 'app-example',
     template: `<ng-content></ng-content>`
   })
   export class ExampleComponent implements AfterContentChecked {
     ngAfterContentChecked() {
       console.log('Content checked after projection');
     }
   }
   ```

6. **`ngAfterViewInit()`**:
   ```typescript
   import { Component, AfterViewInit, ViewChild, ElementRef } from '@angular/core';

   @Component({
     selector: 'app-example',
     template: `<div #myDiv>View content</div>`
   })
   export class ExampleComponent implements AfterViewInit {
     @ViewChild('myDiv') myDiv: ElementRef;

     ngAfterViewInit() {
       console.log('View initialized, accessing DOM:', this.myDiv.nativeElement.textContent);
     }
   }
   ```

7. **`ngAfterViewChecked()`**:
   ```typescript
   import { Component, AfterViewChecked } from '@angular/core';

   @Component({
     selector: 'app-example',
     template: `<p>View content</p>`
   })
   export class ExampleComponent implements AfterViewChecked {
     ngAfterViewChecked() {
       console.log('View checked after content change');
     }
   }
   ```

8. **`ngOnDestroy()`**:
   ```typescript
   import { Component, OnDestroy } from '@angular/core';

   @Component({
     selector: 'app-example',
     template: `<p>Component is about to be destroyed</p>`
   })
   export class ExampleComponent implements OnDestroy {
     ngOnDestroy() {
       console.log('Component is being destroyed');
       // Clean up logic such as unsubscribing from observables
     }
   }
   ```

Each of these examples demonstrates a specific lifecycle hook and how it can be used to perform tasks or respond to changes at different stages of a component's lifecycle.