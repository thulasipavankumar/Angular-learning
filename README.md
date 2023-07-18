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
