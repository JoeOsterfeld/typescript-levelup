# Classes Lib Code

## ./libs/classes/src/lib/classes.ts

```ts
export const classNameHeader = 'pets-class';
export const petNameHeader = 'pets-name';

export class Pet {
  noise: string;
  type: string;
  name: string;
  greetings: string[] = [];

  constructor(obj: Partial<Pet>) {
    Object.entries(obj).forEach(([key, value]) => this[key] = value);
  }

  introduction() {
    return `Hi, I am a ${this.type} named ${this.name}. ${this.noise}!`;
  }

  speak() {
    this.greetings.push(this.introduction());
  }
}

export class Dog extends Pet {
  type = 'Dog';
  noise = 'Woof!';
}

export class Cat extends Pet {
  type = 'Cat';
  noise = 'Meow';
}

export class Duck extends Pet {
  type = 'Duck';
  noise = 'Quack';
}

```

## ./libs/classes/src/lib/helper-functions.ts

```ts
import * as PetsClasses from './classes';

export function getPetClass(type: string, name?: string) {
  return new PetsClasses[type]({ name });
}
```

## Export helper functions from libs/classes/src/index.ts

```ts
export * from './lib/helper-functions';
```