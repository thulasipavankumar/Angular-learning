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
