## Basic interview question
 - What are lifecycle hooks in Angular?
 -  What is content projection?
 -  What is the difference between PROMISE & OBSERVABLES?
 -  What are some disadvantages of using Angular?
 -   What is a directive in Angular?
 -   What are decorators in Angular? 
 -   Mention some advantages of Angular
 -   What are the new updates with Angular10? 
     - Older versions of TypeScript not supported
     - Warnings about CommonJS imports 
     - Optional strict setting
     - NGCC Feature 
     - Updated URL routing
     - Deprecated APIs
     - Bug fixes
     - New Default Browser Configuration 
 - What are Pure Pipes? 
 - What are the new updates with Angular17 LTS?
 - What are the new updates with Angular18 Active?  
 - What are Impure Pipes?
 - What is an ngModule?
 - What are filters in Angular? Name a few of them.
 - What is the difference between AOT and JIT? 
 - Explain the @Component Decorator.
 - What are Promises and Observables in Angular? 
 - What are Template and Reactive forms?
 - What is Bootstrap? How is it embedded into Angular? 
 - What is Eager and Lazy loading? 
 - How does an Angular application work?
 - Angular by default, uses client-side rendering for its applications.
 - Explain the concept of dependency injection
 - Explain MVVM architecture.
 - What are RxJs in Angular?
 - What are router links?
 - What exactly is the router state?
 - What is Change Detection, and how does the Change Detection Mechanism work?
 - Create a TypeScript class with a constructor and a function   
 -  What are the differences between Angular decorator and annotation?
 -  What is an AOT compilation in Angular?
 -  What are the advantages of AOT?
 -  What are the three phases of AOT?
    - The three phases of AOT are:
       - code analysis
       - code generation
       - template type checking
- What are dynamic components?
- What are services in Angular?
  - Ans : A service in Angular is a term that covers broad categories of functionalities. A service is any value, function, or feature that an app needs. A service is typically used to accomplish a very narrow purpose such as HTTP communication, sending data to a cloud service, decoding some text, validating data, etc. A service does one thing and does it well. It is different from a component as it is not concerned with HTML or any other kind of presentation logic. Normally, a component uses multiple services to accomplish multiple tasks.
- What are pipes in Angular?
- How do you chain pipes?
- What are observables in Angular?
- What does Angular Material mean?
  - Angular Material is a UI component library that allows professionals to develop consistent, attractive, and completely functional websites, web pages, and web applications. It becomes capable of doing so by following modern principles of web designing, such as graceful degradation and browser probability.
- What is RxJS?
  - RxJS is a library, and the term stands for Reactive Extensions for JavaScript. It is used so that we can use observables in our JavaScript project, which enables us to perform reactive programming. RxJS is used in many popular frameworks such as Angular because it allows us to compose our asynchronous operations or callback-based code into a series of operations performed on a stream of data that emits values from a publisher to a subscriber. Other languages such as Java, Python, etc. also have libraries that allow them to write reactive code using observables.
- What is bootstrapping?
  - Angular bootstrapping, in simple words, allows professionals to initialize or start the Angular application. Angular supports both manual and automatic bootstrapping. Let’s briefly understand the two.

    - **Manual bootstrapping:** It gives more control to professionals about how and when they need to initialize the Angular app. It is extremely useful in places where professionals wish to perform other tasks and operations before Angular compiles the page.
    - **Automatic bootstrapping:** Automatic bootstrapping can be used to add the ng-app directive to the application’s root, often on the tag if professionals need Angular to automatically bootstrap the application. Angular loads the associated module once it finds the ng-app directive and, further, compiles the DOM.  
- What is the digest cycle process in Angular?
  - **The digest cycle** in Angular is the process in which the watch list is monitored to track changes in the watch variable value. In each digest cycle, there is a comparison between the present and the previous versions of the scope model values.   
- What are the distinct types of Angular filters?
    - Filters are a part of Angular that helps in formatting the expression value to show it to the user. They can be added to services, directives, templates, or controllers. You also have the option to create personalized filters as per requirements. These filters allow you to organize the data easily such that only the data that meets the respective criteria are displayed. Filters are placed after the pipe symbol ( | ) while used in expressions.

    - Various types of filters in Angular are mentioned below:

    - currency: It converts numbers to the currency format

    - filter: It selects a subset containing items from the given array

    - date: It converts a date into a necessary format

    - lowercase: It converts the given string into lowercase

    - uppercase: It converts the given string into uppercase

    -orderBy: It arranges an array by the given expression

    - json: It formats any object into a JSON string

    - number: It converts a number value into a string

    - limit: It restricts the limit of a given string or array to a particular number of elements or strings
-  What is multicasting in Angular?
   - In Angular, when we use the HttpClient module to communicate with a backend service and fetch some data, after fetching the data, we can broadcast it to multiple subscribers in one execution. This task of responding with data to multiple subscribers is called multicasting. It is specifically useful when we have multiple parts of our applications waiting for some data. To use multicasting, we need to use an RxJS subject. As observables are unicast, they do not allow multiple subscribers. However, subjects do allow multiple subscribers and are multicast.
- What are Angular building blocks?
    - The following building blocks play a crucial role in Angular:

    - **Components:** A component can control numerous views wherein each of the views is a particular part of the screen. All Angular applications have a minimum of one component called the root component. This component is bootstrapped in the root module, the main module. All the components include the logic of the application that is defined in a class, while the main role of the class is to interact with the view using an API of functions and properties.
    - **Data binding:** Data binding is the process in which the various sections of a template interact with the component. The binding markup needs to be added to the HTML template so that Angular can understand how it can connect with the component and template.
    - **Dependency injection:** It uses DI so that it can offer the necessary dependencies: mainly services, to the new components. The constructor parameters of a component inform Angular regarding the numerous services needed by the component, and DI provides a solution that gives the necessary dependencies to the new class instances.
    - **Directives:** Angular templates are dynamic, and directives help Angular understand how it can transform the DOM while manifesting the template.
    - **Metadata:** Classes have metadata attached to them with the help of decorators so that Angular will have an idea of processing the class.
    Modules: Module or NgModule is a block of code organized using the necessary capabilities set, having one specific workflow. All Angular applications have at least one module, the root module, and most of the applications have numerous modules.
    - **Routing:** The Angular router helps interpret the URL of a browser to get a client-generated experience and view. This router is bound to page links so that Angular can go to the application view as soon as the user clicks on it.
    - **Services:** Service is a vast category that ranges from functions and values to features that play a significant role in Angular applications.
    Template: The view of each component is linked with a template, and an Angular template is a type of HTML tag that allows Angular to get an idea of how it needs to render the component.
- Explain the MVVM architecture.
- Explain the different kinds of Angular directives.
- What are the different types of compilers used in Angular?
- What is server-side rendering in Angular?
- What is Angular Universal?
- What are HttpInterceptors in Angular?
- How does one share data between components in Angular?
  - There is not one but various methods to share data between components in Angular. They are mentioned below:
    - **Parent to Child:** via Input
    - **Child to Parent:** via Output() and EventEmitter
    - **Child to Parent:** via ViewChild
    - **Unrelated Components:** via a Service 
- What are the differences between Angular expressions and JavaScript expressions?
-  What is the difference between interpolated content and the content assigned to the innerHTML property of a DOM element?
-  What is ngcc?
-  What is folding?
   - In Angular, it might be possible while generating the code that some of the non-exported members are folded. This is called Folding, i.e. the process in which the evaluation of an expression is done by the collector, and the result is recorded in the .metadata.json, is known as Folding.


- What are macros?
- What is the state function?
- What is NgZone?
- What is NoopZone?
- A form with numerous inputs is experiencing sluggish responses, especially during data entry. How can you enhance the performance of the form so that the functionality or the user experience does not get affected?
- The Project involves fetching data from multiple APIs on a single page. Create a strategy to fetch and join this data in an organized manner. Also, ensure that there is minimal impact on user experience and performance of the code.
  - We can use “forkJoin” or “combineLatest” operators from the RxJS. These operators helps when we have multiple detectables that rely on each other for some calculations or determination.

## Angular Coding Interview Questions 

-  Create a custom pipe to convert strings to title case.
-  Build a reactive form with validation
-   Implement a service with HttpClient.
-   Use ngFor directive to display a list.
-   Create a directive to change the background color of an element.
-   
   

 
   

  


        
        

