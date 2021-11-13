# Form template

The Form template create the form inside the template (html) and then use it in component. We have FormGroup and FormControl.
FormControl is the single input, FormGroup is a collection (or subcollection) of FormControl.

## template

Declare a template variable *f* with value *ngForm* (create a FormGroup)
For each input set *id* and *name* and use *ngModel* directive (create a FormControl with name of the attribute *name*)

```html
<form #f="ngForm" [ngSubmit]="onSubmit(f.value)">
    <label for="username">Username</label>
    <input type="text" id="username" name="username" ngModel>

    <label for="email">Email</label>
    <input type="email" id="email" name="email" ngModel>

    <label for="password">Password</label>
    <input type="password" id="password" name="password" ngModel>
</form>
```

## component

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
    selector: 'my-form',
    templateUrl: 'my-form.component.html',
    styleUrls: ['./my-form.component.css']
})
export class MyFormComponent implements OnInit {

    constructor () { }

    ngOnInit() : void {

    }

    onSubmit(formValue: any) {
        console.log({formValue});
    }
}
```