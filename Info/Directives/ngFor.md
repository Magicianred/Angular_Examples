# ngFor

Use it for loop

## PostsList

```ts
import { Component } from '@angular/core';

@Component({
  selector: 'posts-list',
  templateUrl: './posts-list.component.html',
  styleUrls: ['./posts-list.component.css']
})
export class PostsListComponent implements OnInit {
  posts: List<Post>;

  constructor() {
    this.posts = [];
  }

  ngOnInit(): void {

  }
}
```

In the template

The attribute that represent the prop of the child component it will be used in square parenthesis.

```html
<div>
    <h1>Posts list</h1>
    <div *ngFor="let post of posts">
        <post-details [postTitle]={post.title}></post-details>
    </div>
</div>
```