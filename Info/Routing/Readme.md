# Routing in Angular

## AppRoutingModule

in *app.module.ts* viene importato il modulo *AppRoutingModule* che si occupa della gestione del routing (che è una convenzione di Angular).

```Typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
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

in *app-routing.module* si creano effettivamente le rotte

```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';

const routes: Routes = [];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

nell'array *routes* andiamo a configurare le nostre rotte e poi lo passiamo a *RouterModule.forRoot(routes)*.

Per esempio:

```typescript
const routes: Routes = [
    { path: '', redirectTo: 'home', pathMatch: 'full' },
    { path: 'home', component: HomeComponent },
    { path: 'about', component: AboutComponent },
    { path: 'person/:id', component: PersonComponent },
    { path: 'private/:id', component: PrivateComponent, canActivate: [LoggedGuard] },
    { path: '**', component: 'pageNotFoundComponent' }
];
```

props:
 - path : indica il path a cui effettuare il match
    - indicando ** si ha un wildcard per tutte i path non trovati
 - redirectTo : indica un path al quale effettuare il redirect se il path è trovato
 - component : indica il componente che vogliamo visualizzare se il path è trovato
- pathMatch
    - 'full' results in a route hit when the remaining, unmatched segments of the URL match is the prefix path
    - 'prefix' tells the router to match the redirect route when the remaining URL begins with the redirect route's prefix path.

## router-outlet

è il placeholder dove devono essere renderizzati i componenti delle rotte

```html
<router-outlet></router-outlet>
```

## Navigazione con tag a

```html
<a [routerLink]="['/home']">
    Home
</a>
<a [routerLink]="['/person/1']">
    Person 1
</a>
```

### Recupero dei parametri nel path

```typescript
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

@Component({
  selector: 'person',
  templateUrl: './person.component.html',
  styleUrls: ['./person.component.css']
})
export class PersonComponent implements OnInit {
  title = 'Person';
  id: string;

  constructor(private route: ActivatedRoute) {
      route.params.subscribe((params) => {
          const { id } = params;
          this.id = id;
      })
  }

  ngOnInit(): void {

  }
}
```