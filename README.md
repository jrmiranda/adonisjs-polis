# AdonisJs Polis
A simple AdonisJs package that allows you to use multi tenancy in your application.

## Instalation
1. Install package:
```
npm install --save @jrmiranda/adonisjs-polis
```
2. Register Polis provider inside `start/app.js` file:
```
const providers = [
  ...
  '@jrmiranda/polis/providers/PolisProvider'
  ...
]
```
3. Set up the middleware in `start/kernel.js` file:
```
const namedMiddleware = {
  ...
  tenant: 'Adonis/Middleware/TenantDetector'
  ...
}
```

## Usage
Add Polis trait to your multi tenant models:
```
const Model = use('Model')

class User extends Model {
  static boot () {
    super.boot()

    this.addTrait('TenantAware')
  }
}
```
And use Polis middleware in the related routes:
```
Route.group(() => {
  Route.post('/login', 'SessionController.create')
}).middleware(['tenant'])
```