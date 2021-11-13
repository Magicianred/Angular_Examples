# Reactive form

We create a form in component and the use it in template. We have FormGroup and FormControl.
FormControl is the single input, FormGroup is a collection (or subcollection) of FormControl.

## component 

```typescript
import { Component, OnInit } from '@angular/core';
import { FormBuilder, FormGroup } from '@angular/forms';

@Component({
    selector: 'my-reactive-form',
    templateUrl: './my-reactive-form.component.html',
    styleUrls: ['./my-reactive-form.component.css']
})
export class MyReactiveForm implements OnInit {
    form: FormGroup;

    constructor(fb: FormBuilder) { 
        this.form = fb.group({
            username: 'my-username',
            email: 'my-email@email.it',
            password: '1234Prova',
        });
    }

    ngOnInit(): void {

    }

    onSubmit(formValue: any) {
        console.log({formValue})
    }
}
```

## template

Use the attribute *[formGroup]* for bind the FormGroup create in the component.
Use the attribute *[formControl]* for bind the right FormControl.

```html
<form [formGroup]="form" [ngSubmit]="onSubmit(form.value)">
    <label for="username">Username</label>
    <input type="text" id="username" name="username" [formControl]="form.controls['username']">

    <label for="email">Email</label>
    <input type="email" id="email" name="email" [formControl]="form.controls['email']">

    <label for="password">Password</label>
    <input type="password" id="password" name="password" [formControl]="form.controls['password']">
</form>
```
