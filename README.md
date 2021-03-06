[![Angular 2 Style Guide](https://mgechev.github.io/angular2-style-guide/images/badge.svg)](https://github.com/mgechev/angular2-style-guide)
[![MIT license](http://img.shields.io/badge/license-MIT-brightgreen.svg)](http://opensource.org/licenses/MIT)
[![Dependency Status](https://david-dm.org/preboot/angular2-library-seed/status.svg)](https://david-dm.org/preboot/angular2-library-seed#info=dependencies) [![devDependency Status](https://david-dm.org/preboot/angular2-library-seed/dev-status.svg)](https://david-dm.org/preboot/angular2-webpack#info=devDependencies)

![nativescript-ng2-magic](https://cdn.filestackcontent.com/XXMT4f8S8OGngNsJj0pr?v=0)

Magically drop a [NativeScript](https://www.nativescript.org/) app into your existing [Angular2](https://angular.io/) web application and reuse all your code.*

*You will be adding NativeScript views, but you already knew that.*

* [Install](#install)
* [Usage](#usage)
* [Example](#example)
* [Supported seeds](#supported-seeds)

## Install

```
npm i nativescript-ng2-magic
```

## Usage

1. Use `Component` from `nativescript-ng2-magic` instead of `angular2/core`. [Why?](#why-different-component)
2. Use `templateUrl` with your components and use absolute paths. [Why?](#why-absolute-paths)
3. Point `MagicService.NATIVESCRIPT_VIEW_PATH` at a specific directory for your NativeScript views.
4. Create NativeScript views for each of your component's templates in that ^ directory. [How?](#how-to-create-nativescript-views)
5. [Run your truly *native* mobile app with NativeScript!](#run-for-first-time)

## Example

A sample root component, **app.component.ts**:

```
import {Component, MagicService} from 'nativescript-ng2-magic';
// can be any directory **relative** to your web src root
// in this repo, the web src root is `src/`
MagicService.NATIVESCRIPT_VIEW_PATH = './client/nativescript'; 

@Component({
  selector: 'app',
  templateUrl: './client/components/app.component.html'
})
export class AppComponent {}
```

#### What if using the router?

If your app is using the router, you will want to use the `MagicService.ROUTER_DIRECTIVES` from `nativescript-ng2-magic`. Here's an example of the root component above using routing:

```
import {Component, MagicService} from 'nativescript-ng2-magic';
import {RouteConfig} from 'angular2/router';
// can be any directory **relative** to your web src root
// in this repo, the web src root is `src/`
MagicService.NATIVESCRIPT_VIEW_PATH = './client/nativescript'; 

import {HomeComponent} from './components/home';
import {AboutComponent} from './components/about';

@Component({
  selector: 'app',
  templateUrl: './client/components/app.component.html',
  directives: [MagicService.ROUTER_DIRECTIVES]
})
@RouteConfig([
  { path: '/home',       component: HomeComponent,        name: 'Home', useAsDefault: true },
  { path: '/about',      component: AboutComponent,       name: 'About' }
])
export class AppComponent {}
```

### Run for first time!

You will need to have fully completed steps 1-4 above.

Run your app in the iOS Simulator with:

```
npm run start.ios
```

Run your app in an Android emulator with:

```
npm run start.android
```

Welcome to the wonderfully magical world of NativeScript!

## How to create NativeScript views

Based on our example above, assume `./client/components/app.component.html` looks like this:

```
<main>
  <div>This is my root component</div>
</main>
```

You would then create a new file in `./client/nativescript/client/components/app.component.html` like this:

```
<StackLayout>
  <Label text="This is my root component"></Label>
</StackLayout>
```

Notice how the `templateUrl` is expanded to match underneath `./client/nativescript` which is the path we chose to configure `MagicService.NATIVESCRIPT_VIEW_PATH`. 

You can [learn more about NativeScript view options here](https://docs.nativescript.org/ui/ui-views).

You can also install helpful view snippets for [VS Code here](https://marketplace.visualstudio.com/items?itemName=wwwalkerrun.nativescript-ng2-snippets) or [Atom Editor here](https://atom.io/packages/nativescript-ng2-atom-snippets).

You can [learn more here](http://angularjs.blogspot.com/2016/03/code-reuse-in-angular-2-native-mobile.html?m=1) about how this setup works and why.

## Supported Seeds

* [angular2-webpack-seed](https://github.com/NathanWalker/angular2-webpack-seed)

### Why different Component?

`Component` from `nativescript-ng2-magic` is identical to `Component` from `angular2/core`, except it automatically uses NativeScript views when your app runs in a NativeScript mobile app.

The library provides a custom `Decorator` under the hood.
Feel free to [check it out here](https://github.com/NathanWalker/nativescript-ng2-magic/blob/master/src/client/plugin/decorators/magic.component.ts) and it uses a [utility here](https://github.com/NathanWalker/nativescript-ng2-magic/blob/master/src/client/plugin/decorators/utils.ts).

You can see more elaborate use cases of this magic with [angular2-seed-advanced](https://github.com/NathanWalker/angular2-seed-advanced).

### Why absolute paths?

Relative paths won't work because the view path translation expands your component's templateUrl underneath the `NATIVESCRIPT_VIEW_PATH` you configure. It needs a full path to your components template to achieve it's magic.

## Requirements

* [Install NativeScript](http://docs.nativescript.org/start/getting-started#install-nativescript-and-configure-your-environment)
* Requires usage of `templateUrl` for your `Component`'s using absolute paths. 

# License

[MIT](/LICENSE)
