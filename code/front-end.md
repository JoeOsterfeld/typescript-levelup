# Front end code

## Http Interceptor Code

```ts
return next.handle(request).pipe(
  map((event: any) => {
    if (event instanceof HttpResponse && event.body && event.body.type) {
        const className = event.body.type;
        const name = event.body.name;
        const classInstance = getPetClass(className, name);
        return event.clone({ body: classInstance });
    } else {
        return event;
    }
  })
);
```

## App module

```ts
{ provide: HTTP_INTERCEPTORS, useClass: PetsHttpInterceptor, multi: true}
```

## app.component.ts

```ts
  apiUrl = 'http://localhost:3333/api';
  pets: Pet[] = [];

  constructor(
    private http: HttpClient
  ) {

  }

  createPet() {
    const petClassName = prompt('Enter "Dog", "Cat" or "Duck"');
    if (petClassName) {
      const name = prompt('Enter pet name');
      this.pets.push(getPetClass(petClassName, name));
    }
  }

  sendPet(pet: Pet) {
    this.http.post(
      this.apiUrl,
      pet,
      {
        headers: {
          [classNameHeader]: pet.type,
          [petNameHeader]: pet.name
        }
      }).subscribe();
  }

  getPet() {
    this.http.get(this.apiUrl).subscribe((pet: Pet) => {
      this.pets.push(pet);
    });
  }
```

## app.component.html

```html
<header>
  <span>Pets!</span>
</header>

<main>
  <br><br>
  <button (click)="createPet()">Create Pet</button>
  <button (click)="getPet()">Get a pet from the server</button>
  <br><br>
  <div class="pet" *ngFor="let pet of pets">
    {{pet.name}} ({{pet.type}})
    <button (click)="pet.speak()">Speak</button>
    <button (click)="sendPet(pet)">Send to server</button>
    <div *ngFor="let greeting of pet.greetings">
      {{greeting}}
    </div>
  </div>
  <br><br>
</main>
```

## styles.scss

```scss
:root {
  --primary-color: #FF9F17;
}

* {
  font-family: sans-serif;
  font-size: 24px;
}

html, body, header {
  margin: 0;
  padding: 0;
  text-align: center;
}

h1 {
  margin: 0;
  padding: 0;
}

header {
  background-color: var(--primary-color);
  color: black;
  text-align: left;
  height: 50px;
  font-size: 30px;
  padding-left: 20px;
  span {
    padding-top: 4px;
  }
}

main {
  max-width: 1000px;
  margin: auto;
  text-align: left;
}

button {
  background-color: var(--primary-color);
  color: black;
  padding: 6px 12px;
  font-size: large;
  border-radius: 3px;
  outline: none;
  margin: 0 6px 6px 0;
}

.pet {
  > div {
    margin-left: 20px;
  }
}
```