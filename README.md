# mhp

## Overview
1. Building, Running and Testing the Project
2. Business Recommendation
3. Architecture
4. Recommendations for Scaling
5. Feature Recommendations

## 1. Building, Running and Testing the Project

In order to build and run the project following commands have to be executed in the project
directory:

1. `yarn install`
2. `yarn build`
3. `yarn start`

In order to test the project run following command:

`yarn test`



## 2. Business Recommendation
As there were no given frames for the project I recommend following approaches for
following use cases:

* __Money and/or time constraints:__  To save time (and thus money) rather use
a UI libary such as react-md, bootstrap, etc.; In general keep Stack lean to reduce time expenses.

* __Focus on product leadership and/or enterprise solutions:__ In order to create a high quality product components 
can be created individually. An external UI library is limited in customization and also includes unnecessary functions, thus
performance and design can be impaired. For bigger projects also see the section 'Recommendations for Scaling'.


As I had no constraints I went for a lean stack (to keep time expense small), but created individualized 
components (for being freely creative in design).


## 3. Architecture

### 3.1 Stack

| Technology       | Purpose       |
|------------------| :-----------: |
| Yarn  | Package manager |
| Webpack v4  | Build process and bundling |
| Babel  | Build process and bundling |
| Axios  | API |
| React v16  | UI Components |
| React Router v4 | Clientside routing |
| PropTypes | Typesafety |
| Redux | Data flow |
| Redux Actions | Lean and reusable actions |
| Redux Saga | Side effects and business logic |
| Scss | stylesheets |
| Lodash | utility |
| Jest | unit testing |
| Enzyme | unit testing (components) |

### 3.2 Layer
[logo]: architecture.png "Architecture"
![alt text][logo]

* __UI Components:__ User Interface
* __Redux Actions:__ Declarative layer for global state changes (get data)
* __Redux Sagas:__ Layer for any kind of side effects and business logic
* __Redux Reducers:__ Layer to update state
* __Redux global state:__ data tree


### 3.3 Explanation
* __Rule 1 - Fetched data get transformed in sagas:__ Fetched data from apis get transformed in sagas in order to match the structure of the UI components.
As an advantage this keeps maintenance very easy as well as the app resilient. If data structures returned from an api change,
these data structures can be adjusted at one place in order to match component patterns again. (Instead of 
having to search through all components in order to adjust.)

* __Rule2 - Each saga has only one responsibility:__ In order to engender highly reusable code, each saga has one purpose. The fetched data
is transformed in a way that it is highly reusable. (For sequences: arrays, for quick access: hashmaps),

* __Rule3 - Every component gets a respective classname:__ Every component needs to have the same classname
as its respective component name. This serves maintenance purposes as well.

* __Rule4 - Components are differentiated by component and view:__ Conmponents are seperated after their degree of reusability.
Entire pages / views can be found in /views and global reusable components respectively in /components and can be 
accessed via the aliases 'Views' and 'Components'.

* __Rule5 - Each component gets its own directory:__ If a component includes more than 1 file it ought to have its own directory.

* Genral styles - css / variables

## 4. Recommendations for Scaling

* __Scaling up the project:__ In case that the project will increase in team size and codebase, i
highly recommend the usage of further technology to support code quality, such as Typescript/ Flow, creating webpack 
configs for different environments (dev, prod) and collecting test coverage from unit tests (e.g. istanbulJs).

* __Scaling up data load:__ In case of increase of loaded data, in Sagas at least chunking and 
lazy loading/ pagination should be implemented. Also for longer list views lazy rendering/ pagination should be 
implemented to avoid browser crashes.


## 5. Feature Recommendations
I recommend to implement following features as well in order to guaranty a better user experience:

* Snackbar or notifications: Especially for error handling. (Currently errors are caught and global state is being
respectively resetted, but user does not receive any feedback about it).

* Filtering and sorting in table: Especially for plethora of data user experience can be enhanced by implementing filter
and sort functionalities into table.