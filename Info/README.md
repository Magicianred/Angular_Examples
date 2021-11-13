# Info on Angular

[Documentazione ufficiale](https://angular.io/docs)  

## Install CLI

Install node.js and npm, then:

```cmd
npm install -g @angular/cli@latest
```

## Create a new project

Open your cmd, go to the folder where put your new application, run:

```cmd
ng new <name_of_app>
```

- <name_of_app> is the name of your application, will be create a folder with that name

## file /src/index.html

It's the file that start the application angular and give the HTML structure.

- <app-root></app-root> it's the placeholder where the angular app take place

## file /src/app/app.component.ts

It's the main component of your angular app

- app.component.html it's the HTML template of the component app
- app.component.css it's the stylesheet of the component app

## file tslint.json

Rules of tslint

## fle tsconfig.json

Configuration file of typescript

## file angular.json

Configuration file of Angular

- projects/<name_app>/architect/build/index

It's the path of the file index.html for the app

- projects/<name_app>/architect/build/main

It's the path of the file with the entry point of javascript/typescript angular app

- projects/<name_app>/architect/build/styles

Array of string for include css path files (when import bootstrap, bulma, other css framework, you have to include here the reference)



## Input prop

In the parent component we use:

```ts
<post-details postTitle="my title"></post-details>
```

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'post-details',
  templateUrl: './post-details.component.html',
  styleUrls: ['./post-details.component.css']
})
export class PostDetailsComponent implements OnInit {
  @Input() postTitle: string; // from the parent component

  constructor() {
  }

  ngOnInit(): void {

  }
}
```

## Event click (and template variable - with #)

In the parent component we use a button (with type button for avoid submit and refresh page):

```ts
<input class="input" type="text" placehoder="param 1" #param1>
<input class="input" type="text" placehoder="param 2" #param2>
<button type="button" (click)="onClick(param1, param2)">Do click</button>
```

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'post-details',
  templateUrl: './post-details.component.html',
  styleUrls: ['./post-details.component.css']
})
export class PostDetailsComponent implements OnInit {
  @Input() postTitle: string; // from the parent component

  constructor() {
  }

  ngOnInit(): void {

  }

  onClick(param1: HTMLInputElement, param2: HTMLInputElement) {
      console.log('param1', param1.value);
      console.log('param2', param2.value);
  } 
}
```

## Emit event

In the component we use:

```ts
<post-details (newTodo)="onAddPost($event)"></post-details>
```

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'post-details',
  templateUrl: './post-details.component.html',
  styleUrls: ['./post-details.component.css']
})
export class PostDetailsComponent implements OnInit {
  @Input() postTitle: string; // from the parent component
  @Output() newPost: EventEmitter<Post> = new EventEmitter<Post>();

  constructor() {
  }

  ngOnInit(): void {

  }

  onClick(param1: HTMLInputElement, param2: HTMLInputElement) {
      console.log('param1', param1.value);
      console.log('param2', param2.value);
  }

  onAddPost(post: Post) {
      const newPost: post = {
          title: 'New post',
          text: 'text of new post',
          date: new Date()
      };
      this.newPost.emit(newPost);
  }
}
```




