Angular-learning
## Angular Architecture
- Components
- Templates => Displays of the component
- Services => 
- Dependency Injection => How we can let the components call code in the service
- Directives =>  way to give more funtionality to the html elements
- Pipes => can be used to format the data
- Modules => Angular groups of other pieces e.g. Admin module,Users module,Pricing module
- One-way Data flow => 
- Zone.js and change detection => 
- Rendering Targets
## New in Angular 14
- standalone components
- Typed forms
- ng completion , specify title direcrtly in the route


## What is a component
- Component = Template + Class(Properties+Methods) + Metadata

  `Template`<br/>
  - View Layout => create with HTML, Includes binding and directives

  `Class`<br/>
  - Code supporting the view
  - Created with Typescript

  `Metadata`<br/>
  - Extra data for Angular
  - Defined with a decorator
 

## Directives, Templates and Interpolation

  `Directives`<br/>
  - Custom HTML element or attribute used to power up and extend our HTML
  - Angular also has built-in directives 

  `Interpolation`<br/>
  - One way data binding from class to template
  - <h1>{{name}}}<h1>

## Data bindlings & Pipes
Below lines illustrate the follow of data binding between components and DOM

`Data binding`<br/>
- Poperty Binding `Component => (properties) => DOM`
  <img [src]='product.imageUrl'>
- Interpolation
   {{example}}
- Event binding `DOM => (events) => Component`
  <button (click='toggleImage()')>
- Two-Way Binding
  <input [(ngmodel)]='listFilter'/>    => dont forger to import forms module to use ngmodel

`pipes`<br/>
- Transform bound properties before display  {{product.productCode | lowercase }}
- Built-in pipes: data,number,decimal,json etc

`custom pipes`<br/>
```typescript
import { Pipe, PipeTransform } from "@angular/core";

@Pipe({name:'convertToSpaces'})
export class convertToSpacesPipe implements PipeTransform{
    transform(value: string,character: string): string {
        return value.replace(character," ")
    }
}
```
The above snippet can be used as pipe e.g.:- `{{ product.productCode | lowercase | convertToSpaces:'-' }}`

## Change Detection(google)

## Component Lifecycle (onInit,onChanges,onDestroy)
- A lifecycle hook is an interface
- we implement to write code that is executed when the life cycle of a component occurs

## Getters and setters (in component classes)

```typescript
    private _listFilter: string = '';

    get listFilter(): string {
        return this._listFilter;
    }

    set listFilter(value: string) {
        this._listFilter = value;
    }
```
## Nested Components 
- @Input()  => data from ?
- @Output() => Event emitter => data from nested component to the container

## Services and Dependency injection

 `Service`<br/>
  - Registering service ? Root Injector ( available throughout application) | Component Injector (service only availabe to that component and its child nested componenets)
  - set the `providedIn` property for the service
```typescript
@Injectable({
    providedIn:'root'      //<==  service is availabe through out the application
})
export class ProductService {
  getProducts():IProducts[]{
}
}
```
## Retrive data using http

Observable 
- unline an array it doesn't retain items
- emitted items can be observed over time
- events => `next`|`error`|`complete`

## Navigation and routing

### How Routing Works
- Configure a route for each component
- Define options/actions
- Tie a route to each option/action
- Activate the route based on user action
- Activating a route displays the component's view

```html
<nav class='navbar navbar-expand navbar-light bg-light'>
  <a class='navbar-brand'>{{pageTitle}}</a>
  <ul class='nav nav-pills'>
    <li><a class='nav-link' routerLinkActive='active' routerLink='/welcome'>Home</a></li>
    <li><a class='nav-link' routerLinkActive='active' routerLink='/products'>Product List</a></li>
  </ul>
  </nav>
  <div class='container'>
  <router-outlet></router-outlet>
  </div>
```

`app.module.ts` file with routing paths<br/>
```typescript
@NgModule({
  declarations: [
    AppComponent,
    ProductListComponent,
    convertToSpacesPipe,
    StartComponent,
    ProductDetailComponent,
    WelcomeComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,  // <== may be used for ngmodel (google out)
    HttpClientModule,
    RouterModule.forRoot([{path:'products',component:ProductListComponent},
    {path:'products/:id',component:ProductDetailComponent},
    {path:'welcome',component:WelcomeComponent},
    {path:'',redirectTo:'welcome',pathMatch:'full'},
    {path:'**',redirectTo:'welcome',pathMatch:'full'}
  ])
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }
```
### Routing additional techniques

Reading parameters from a route
- Snapshot - Read the parameter one time
- Observable - Read emitted parameters as they change
- Specified string is the route parameter name
```typescript
<a [routerLink]="['/products', product.productId]">
                  {{ product.productName }}
 </a>
```
`Activating route with a code`
```typescript
onBack():void{
    this.router.navigate(['/products'])
}
```
`protecting routes with gaurds`<br/>
- can activate => guard navigation to a route 
- can deactivate => guard navigation from a route 
- resolve => pre-fetch data before activating a route 
- canload => prevents asynchronous routing
```typescript
export class ProductDetailGuard implements CanActivate {

  constructor(private router: Router) {}
  
  canActivate(
    route: ActivatedRouteSnapshot,
    state: RouterStateSnapshot): Observable<boolean | UrlTree> | Promise<boolean | UrlTree> | boolean | UrlTree {
    const id = Number(route.paramMap.get('id'));
    if (isNaN(id) || id < 1) {
      alert('Invalid product id');
      this.router.navigate(['/products']);
      return false;
    }
    return true;
  }

}
```
