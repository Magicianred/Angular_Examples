# The flow of Angular App

## Starting point

Angular app has *index.html* file as starting point

Locate in *src* folder of your project define the base structure of your app.

```html
<!doctype html>
    <html lang="en">
    <head>
    <meta charset="utf-8">
    <title>MyApp</title>
    <base href="/">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="icon" type="image/x-icon" href="favicon.ico">
    </head>
    <body>
    <app-root></app-root>
    </body>
</html>
```

An Angular application is always rendered inside the body tag and comprises a tree of components. When the Angular CLI finds a tag that is not a known HTML element, such as app-root, it starts searching through the components of the application tree.

## Bootstrapping

the process is defined in file *main.ts* of *src* folder.

```ts
import { enableProdMode } from '@angular/core';
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

import { AppModule } from './app/app.module';
import { environment } from './environments/environment';

if (environment.production) {
  enableProdMode();
}

platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));
```

