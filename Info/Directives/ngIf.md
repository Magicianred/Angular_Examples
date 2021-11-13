# ngIf

Use it when you want handle the conditional "visibility" (if it's insert in the DOM or not) of an element.

```html
<div>
    <p *ngIf="isNew">New arrivals!!!</p>
    <p>Product Title</p>
    <p>Product description</p>
    <p *ngIf="isNicePrice">Nice price!!!</p>
</div>
```