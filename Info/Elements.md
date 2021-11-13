# The elements of Angular App

## Modules

Angular organizes components in Modules, in a Angular app exists almost 1 module, it called *AppModule*.

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

- declarations
In the prop declarations we register the Components of our app. Here we have to put all the component used in this module.

- imports
there is the dependencies of this module (usually other modules used in this module)

- providers
are used for the DI

- bootstrap
indicate where is the app-root component

## Components

Any component is registered with a module in order to be recognized by Angular app.

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'my-app';
}
```

### Generate new component

```cms
ng generate component <your_component_name>
```

- <your_component_name> is the name of the component
  - folder name, if you have need of a folder insert in the component name, for example: users/user

### Class variable

In the parent component we use:

```typescript
<post-details postTitle="my title"></post-details>
```

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'post-details',
  templateUrl: './post-details.component.html',
  styleUrls: ['./post-details.component.css']
})
export class PostDetailsComponent implements OnInit {
  listName: string; // internal variable
  @Input() postTitle: string; // from the parent component

  constructor() {
    this.listName = 'List title';
  }

  ngOnInit(): void {

  }
}
```

### Selector

We can defined a selector in a Component for matching html tag with.

```typescript
selector: 'app-root'
```

### Template

The html content of the component is called *template* and is linked by the prop *templateUrl*. It's the relative path to the file.

```typescript
templateUrl: './app.component.html'
```

In the template file we define *interpolation*. That's the system to retrieve value from Angular app to html.

```typescript
<span>{{ title }} app is running!</span>
```

### Model (optional)

represent the entities of the app, use the extention *<your_class_name>.model.ts* (for example *post.model.ts*)

```typescript
export class Post {
  title: string;
  text?: string;
  date: Date;
  author?: string;

  constructor(title: string, date: Date) {
    this.title = title;
    this.date = new Date();
  }
}
```



## Services

It uses for isolated and grouped common part of application in a single point

```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class MyService {
  
  constructor() {

  }
}
```

- providedIn
  - root : singleton
  - any : instantiate any time

### Generate new service (Injectable)

```cms
ng generate service <your_service_name>
```

- <your_service_name> is the name of the service
  - folder name, if you have need of a folder insert in the service name, for example: users/user

### Use service in component

- Include service in AppModule

```Typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';

import { MyService } from './services/my.service';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule
  ],
  providers: [
    MyService
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

then use in component

```typescript
import { Component } from '@angular/core';
import { MyService } from './services/my.service';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'my-app';

  constructor(private myService: MyService) {

  }
}
```

### An example of service with http calls

- Include service in AppModule

```Typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { HttpClientModule } from '@angular/common/http';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';

import { MyService } from './services/my.service';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    HttpClientModule
  ],
  providers: [
    MyService
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

- create service

```typescript
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Injectable({
  providedIn: 'root'
})
export class MyService {
  
  constructor(private http: HttpClient) {

  }

  getData(id: string = '1') {
    return this.http.get('https://your_url/');
  }
}
```

then use in component

```typescript
import { Component } from '@angular/core';
import { MyService } from './services/my.service';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit {
  title = 'my-app';

  constructor(private myService: MyService) {

  }

  ngOnInit(): void {
    // return an observable
    this.myService.getData(1)
      .subscribe(res => console.log({res}));
  }
}
```




## Guards

It uses for isolated and grouped common part of application in a single point

```typescript
import { Injectable } from '@angular/core';
import { CanActivate, ActivatedRouteSnapshot, UrlTree } from '@angular/router';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class MyGuard implements CanActivate {
  
  canActivate(
    next: ActivatedRouteSnapshot,
    state: RouterStateSnapshot
    ) : Observable<boolean | UrlTree> | Promise<boolean | UrlTree> | boolean | UrlTree {
      return true;
    }
  
}
```

- providedIn
  - root : singleton
  - any : instantiate any time

### Generate new guard (Injectable)

```cms
ng generate guard <your_guard_name>
```

- <your_guard_name> is the name of the guard
  - folder name, if you have need of a folder insert in the guard name, for example: users/user
