## Setting Up Routing and 404 in Angular 17

### 1. Generate Components
Let's create three components: `HomeComponent`, `AboutComponent`, and `PageNotFoundComponent`.

```bash
ng generate component home
ng generate component about
ng generate component page-not-found
```

### 2. Create Routing Module
Generate a routing module:

```bash
ng generate module app-routing --module=app
```

### 3. Define Routes
In `app-routing.module.ts`, import the necessary modules and define routes:

```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';
import { PageNotFoundComponent } from './page-not-found/page-not-found.component';

const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'about', component: AboutComponent },
  { path: '**', component: PageNotFoundComponent } // Wildcard route for 404
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

### 4. Import Routing Module
In `app.module.ts`, import and import the `AppRoutingModule`:

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';
import { PageNotFoundComponent } from './page-not-found/page-not-found.component';

@NgModule({
  declarations: [
    AppComponent,
    HomeComponent,
    AboutComponent,
    PageNotFoundComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

### 5. Component Content
For simplicity, let's add some basic content to each component:

**home.component.html:**
```html
<h1>Home</h1>
```

**about.component.html:**
```html
<h1>About</h1>
```

**page-not-found.component.html:**
```html
<h1>404 - Page Not Found</h1>
```

### Explanation

* We've defined three routes:
  - `''`: This maps to the `HomeComponent` and will be the default route.
  - `'about'`: This maps to the `AboutComponent`.
  - `'**'`: This is a wildcard route that matches any URL that doesn't match the previous routes, directing users to the `PageNotFoundComponent`.

### Running the Application
Start the development server:

```bash
ng serve
```

Now, you can access the following URLs:

* `http://localhost:4200`: This will load the `HomeComponent`.
* `http://localhost:4200/about`: This will load the `AboutComponent`.
* Any other URL will load the `PageNotFoundComponent`.

**Additional Notes:**

* You can customize the 404 page with more informative content or error handling logic.
* For more complex routing scenarios, consider using child routes, route parameters, and guards.
* Angular provides additional features for routing, such as lazy loading and redirects, which you can explore based on your application's requirements.

