

--- Since adding a routing to the existing app.module will give an error

```bash
$ ng g module app --routing true --flat
error! src/app/app.module.ts already exists.
```

--- Add the following code to  new file src/app/app-routing.module.ts

```Typescript
import { NgModule } from '@angular/core';
import {Routes, RouterModule, ExtraOptions} from '@angular/router';

const routes: Routes = [
  { path: 'pages', loadChildren: 'app/pages/pages.module#PagesModule' },
  { path: '', redirectTo: 'pages', pathMatch: 'full' },
  { path: '**', redirectTo: 'pages' },
];

const config: ExtraOptions = {
  useHash: true,
};

@NgModule({
  imports: [RouterModule.forRoot(routes, config)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

--- Import the routing.module to the app.module.ts file

```Typescript
@NgModule({
 imports: [
 ...<previous code>
  AppRoutingModule
]
...<other code>
```

--- Replace the app.component.html code to the below

```html
<router-outlet></router-outlet>
```

--- Create the pages Modules, Routing and Component

* Module plus Routing

```
$ ng g module pages --routing true
```

* Component (Simplified)

```
$ ng g component pages --inline-style true --inline-template true --spec false 
```

--- Let's create a fictitious Menu

* Add a new file called `pages-menu.ts` under `src/app/pages` with the following content:

```Typescript
import {NbMenuItem} from '@nebular/theme';

export const MENU_ITEMS: NbMenuItem[] = [
  {
    title: 'Dashboard',
    icon: 'nb-home',
    link: '/pages/dashboard',
    home: true,
  },
  {
    title: 'FEATURES',
    group: true,
  }
];

```