# Back end code

## use cors

```ts
    import * as cors from 'cors';

    const app = express();
    app.use(cors());
```

## Add classBody Middleware function in app./middleware.ts

```ts
import { classNameHeader, getPetClass, petNameHeader } from '@pets/classes';


export function classBody(req, res, next) {
  const className = req.get(classNameHeader);
  const animalName = req.get(petNameHeader);
  if (className) {
    req.body = getPetClass(className, animalName);
  }
  next();
}

```

## back end post to api in main.ts

```ts
app.post('/api', classBody, (req, res) => {
  const intro = req.body.introduction(); // In back end app code, no action, taken, but class is instantiated.
  console.log(intro);
  res.status(204).send();
});
```

## Back end get to api

```ts
app.get('/api', (req, res) => {
  const types = ['Dog', 'Cat', 'Duck'];
  const names = ['Tom', 'Jerry', 'Tim', 'Frank', 'Eric'];
  const type = types[Math.floor(Math.random() * types.length)];
  const name = names[Math.floor(Math.random() * names.length)];
  console.log(`Sending back a ${type} named ${name}`);
  res.status(200).send({ name, type });
});
```
