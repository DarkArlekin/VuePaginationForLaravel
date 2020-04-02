# Vue pagination for PHP framework Laravel

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run library-build
```

## Usage

### Install package
```
npm install
```

### Import component
```scss
@import '~@ilegionxs/vue-pagination-for-laravel/dist/vue-pagination-for-laravel.css';
```

#### In Vue component
The component name can be any valid.
```js
import Pagination from '@ilegionxs/vue-pagination-for-laravel';
```

#### Global
```js
Vue.component('vue-pagination', require('@ilegionxs/vue-pagination-for-laravel').default);
```

### Add tag with attributes
The attribute "v-bind" should be valid [laravel pagination](https://laravel.com/docs/6.x/pagination).
The attribute "update" should be valid method get data.
```vue
<Pagination v-bind="users"
            @update="getData"></Pagination>
```
