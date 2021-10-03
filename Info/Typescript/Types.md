# Types in Typescript

## String

```ts
var title: string = 'This is the title';
var description: string = `This is the description of ${title}`;
```

## Number 

## Boolean

## Array

```ts
var titles: string[] = ['This is the title', 'another title'];
var ages: number[] = [5, 10, 15, 20];
```

## Any

```ts
var title = any;
var categories = any[] = [1, 'second', true];
```

## Custom types

Defines the possible values

```ts
type CategoryType = 'Normal' | 'Special';
const category: CategoryType = 'Normal';
```

## Enum

```ts
enum CategoryEnum = { Normal, Special };
const category: CategoryEnum = CategoryEnum.Normal;
```

## Void

```ts
function counter() : void {
    count++;
}
```