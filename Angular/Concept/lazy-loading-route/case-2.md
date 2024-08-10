Lazy loading routes in Angular helps improve application performance by loading feature modules only when they are needed. Here’s a live example demonstrating how to set up lazy loading in an Angular application using Angular 17 or later.

### Example: Lazy Loading Routes in Angular

#### 1. **Set Up Your Angular Project**

First, make sure you have an Angular project set up. If you don’t, you can create one using Angular CLI:

```bash
ng new my-angular-app
cd my-angular-app
```

#### 2. **Create Feature Modules**

Let’s create a feature module that will be lazily loaded. In this example, we’ll create a `UserModule` with a `UserComponent`.

```bash
ng generate module user --route user --module app.module
ng generate component user/user
```

**Explanation:**
- The `--route` flag specifies the route path for the module.
- The `--module` flag specifies where to declare the lazy-loaded module, typically `app.module`.

This command sets up lazy loading for the `UserModule` and adds a route to the `app-routing.module.ts`.

#### 3. **Configure Lazy Loading in Routing Module**

Angular CLI automatically sets up lazy loading for you when you use the `--route` flag, but let’s review how to manually configure it.

**File: `app-routing.module.ts`**

```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';

const routes: Routes = [
  { path: '', redirectTo: '/home', pathMatch: 'full' },
  {
    path: 'home',
    loadChildren: () => import('./home/home.module').then(m => m.HomeModule),
  },
  {
    path: 'user',
    loadChildren: () => import('./user/user.module').then(m => m.UserModule),
  },
  { path: '**', redirectTo: '/home' },
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule],
})
export class AppRoutingModule {}
```

**Explanation:**
- **`loadChildren`**: Specifies the path to the module to be loaded lazily. The function returns a promise that resolves to the module.
- **`import('./user/user.module').then(m => m.UserModule)`**: Dynamically imports the `UserModule` when the route is accessed.

#### 4. **Create the User Module**

You need to set up routing for the `UserModule` to define its internal routes.

**File: `user-routing.module.ts`**

```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { UserComponent } from './user.component';

const routes: Routes = [
  { path: '', component: UserComponent },
];

@NgModule({
  imports: [RouterModule.forChild(routes)],
  exports: [RouterModule],
})
export class UserRoutingModule {}
```

**File: `user.module.ts`**

```typescript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { UserRoutingModule } from './user-routing.module';
import { UserComponent } from './user.component';

@NgModule({
  declarations: [UserComponent],
  imports: [
    CommonModule,
    UserRoutingModule
  ],
})
export class UserModule {}
```

**Explanation:**
- **`UserRoutingModule`**: Configures routes specific to the `UserModule`.
- **`UserModule`**: Declares the `UserComponent` and imports the `UserRoutingModule`.

#### 5. **Create Home Module and Component (Optional)**

If you don’t have a home module, you can create one to complete the example.

```bash
ng generate module home --route home --module app.module
ng generate component home/home
```

**File: `home-routing.module.ts`**

```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HomeComponent } from './home.component';

const routes: Routes = [
  { path: '', component: HomeComponent },
];

@NgModule({
  imports: [RouterModule.forChild(routes)],
  exports: [RouterModule],
})
export class HomeRoutingModule {}
```

**File: `home.module.ts`**

```typescript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { HomeRoutingModule } from './home-routing.module';
import { HomeComponent } from './home.component';

@NgModule({
  declarations: [HomeComponent],
  imports: [
    CommonModule,
    HomeRoutingModule
  ],
})
export class HomeModule {}
```

#### 6. **Run Your Application**

Start your Angular application and navigate to different routes to see lazy loading in action.

```bash
ng serve
```

**Navigate to:**
- **`http://localhost:4200/home`**: Loads the `HomeComponent`.
- **`http://localhost:4200/user`**: Lazy loads the `UserModule` and displays the `UserComponent`.

### Conclusion

This example demonstrates how to set up lazy loading for feature modules in Angular. By using `loadChildren` in your routing configuration, Angular loads feature modules on demand, improving the initial load time and performance of your application.