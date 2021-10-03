# The elements of Angular App

## Modules

Angular organizes components in Modules, in a Angular app exists almost 1 module, it called *AppModule*.

```ts
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
In the prop declarations we register the Components of our app

## Components

Any component is registered with a module in order to be recognized by Angular app.

```ts
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

### Selector

We can defined a selector in a Component for matching html tag with.

```ts
selector: 'app-root'
```

### Template

The html content of the component is called *template* and is linked by the prop *templateUrl*. It's the relative path to the file.

```ts
templateUrl: './app.component.html'
```

In the template file we define *interpolation*. That's the system to retrieve value from Angular app to html.

```ts
<span>{{ title }} app is running!</span>
```

