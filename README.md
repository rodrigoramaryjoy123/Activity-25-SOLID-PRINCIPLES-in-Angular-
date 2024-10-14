# Activity-25-SOLID-PRINCIPLES-in-Angular-

Applying SOLID Principles in Angular
We are going to start with the most vague concept that is the least obvious in terms of how we should actually apply it to our Angular development: SOLID principles. The reason it is vague and not immediately obvious is because these principles have been established generically for Object Oriented Programming, not specifically for Angular applications. These principles pre-date Angular by ten years or so.

The fact that these SOLID principles are still touted and advocated for approximately 20 years after their inception should speak to their importance and long term staying power. The SOLID acronym stands for:

Single-responsibility principle
Open-closed principle
Liskov substitution principle
Interface segregation principle
Dependency inversion principle
Don’t worry if this all sounds like a bit much, it isn’t really important to understand all of these right away. We will use some of these concepts quite heavily, and others we may barely touch. Regardless, it is a good idea to just be aware of the existence of these concepts, study them over time, and consider where you might be able to improve your code by using these principles.

We will dedicate the rest of this lesson to covering the basic idea behind each of these principles, and providing examples in an Angular context where useful.

Single-responsibility principle
We will use this concept quite heavily, and we will save most of the discussion of this principle for our next lesson on smart and dumb components which embodies this concept well.

The general idea with this principle is that each class should have one responsibility. In an Angular context, whether that class is a component, directive, pipe, service, or anything else - it should have one responsibility.

Determining what a “responsibility” is, is part of the fun vagueness of these principles that can make them hard to apply. What is a “responsibility”? For example, imagine a service that manages the data/state for todos in an application. That service might:

Load todos
Create todos
Delete todos
Edit todos
Is this four different responsibilities? Should we really break this up into four different services each with just one responsibility? No, we absolutely should not do that. We are probably looking at how to define the “responsibility” here in too strict of a sense. Instead, we could say the responsibility of this service is to: manage the data related to todos. This would then fit the definition of having a single responsibility.

What if that service also managed settings related to how to display those todos? Maybe we have options like the ability to show/hide completed todos. We could probably re-work our definition of:

Manage the data related to todos
To include this additional responsibility, but really this is probably better defined as two separate responsibilities:

Manage the data related to todos
Manage preferences supplied by the user
And should be handled with two different services: a TodoService and a SettingsService each with one responsibility.

As I mentioned before, we also might not always want to apply this principle. Maybe one of our components, or a service, technically has two or three responsibilities. This doesn’t necessarily mean we have to break those classes up into multiple classes that each have one responsibility. That might be an unnecessary or premature optimisation that we don’t need. In the example above, maybe there is just one single setting related to displaying todos. We might decide rather than creating a separate service for just that one setting, we will just add it in to the TodoService. Later, if we introduce more settings, maybe we will refactor it out into its own service then.

Whilst we might not always strictly adhere to the principles, it is good to be aware of the fact that a particular class might be doing more than is optimal, and to consider whether a refactor might be useful.

In the next lesson, we will explore this concept more in relation to smart and dumb components.

Open-closed principle
This is another principle that applies quite well to Angular. This principle states that an entity should be open for extension, but closed for modification. In other words, when creating new features we should incorporate/extend/build on top of existing entities, not modify those existing entities.

Again, this is one of those things that needs to be taken in context and applied where appropriate. For example, let’s consider a simple ButtonComponent:

@Component({
    selector: 'app-button',
    template: `
        <button>Hi</button>
    `
})
export class ButtonComponent {}
It’s a button that say’s “Hi”, fantastic. Now let’s say our requirements have changed - not only do we want a button that says “Hi”, we want to be able to configure its colour!

We could modify our component to this by accepting an input:


Ionic is a popular framework for building cross-platform mobile applications using web technologies like HTML, CSS, and JavaScript. Understanding its application architecture is essential for effective development. Here are the core components of an Ionic application:

1. Components
Components are the building blocks of any Ionic application. Each component encapsulates its own functionality and user interface.

Example: Creating a Simple Component

typescript
Copy code
import { Component } from '@angular/core';

@Component({
  selector: 'app-home',
  template: `
    <ion-header>
      <ion-toolbar>
        <ion-title>Home</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content>
      <h1>Welcome to Ionic!</h1>
      <ion-button (click)="showAlert()">Click Me</ion-button>
    </ion-content>
  `
})
export class HomeComponent {
  showAlert() {
    alert('Button clicked!');
  }
}
2. Pages
In Ionic, pages represent different views of the application. Each page is a component, but it usually has its own routing configuration.

Example: Page Routing

typescript
Copy code
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';

const routes: Routes = [
  { path: '', component: HomeComponent },
  { path: 'about', component: AboutComponent }, // Another page component
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule {}
3. Services
Services are used to encapsulate business logic and data handling. They can be injected into components and other services, promoting code reuse.

Example: User Service

typescript
Copy code
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root',
})
export class UserService {
  private users = [{ name: 'John' }, { name: 'Jane' }];

  getUsers() {
    return this.users;
  }
}
4. Modules
Modules are a way to organize related components, directives, pipes, and services in an Angular application. Each module can encapsulate its own features and dependencies.

Example: Feature Module

typescript
Copy code
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { UserProfileComponent } from './user-profile/user-profile.component';

@NgModule({
  declarations: [UserProfileComponent],
  imports: [CommonModule],
  exports: [UserProfileComponent]
})
export class UserProfileModule {}
5. Routing
Ionic uses Angular's routing system to navigate between pages. The router manages the application state and URL.

Example: Setting Up Routing in Ionic

typescript
Copy code
import { NgModule } from '@angular/core';
import { PreloadAllModules, RouterModule, Routes } from '@angular/router';

const routes: Routes = [
  { path: '', redirectTo: 'home', pathMatch: 'full' },
  { path: 'home', loadChildren: () => import('./home/home.module').then(m => m.HomeModule) },
];

@NgModule({
  imports: [RouterModule.forRoot(routes, { preloadingStrategy: PreloadAllModules })],
  exports: [RouterModule]
})
export class AppRoutingModule {}


