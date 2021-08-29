# vue-input-money

Input field component to display a formatted currency value for [Vue 3](https://vuejs.org/).

[Live Demo](https://webarthur.github.io/vue-input-money/)

### Install via NPM
```sh
$ npm install vue-input-money
```

### Install via CDN
```html
<script src="https://unpkg.com/vue"></script>
<script src="https://unpkg.com/vue-input-money"></script>
<script>
  const app = Vue.createApp({
    data () {
      return {
        price: 1500000
      }
    }
  })
  app.use(InputMoney)
  app.mount('#app')
</script>
```

#### Register as Component
```js
import Vue from 'vue'
import InputMoney from 'vue-input-money'

export default {
  
  name: 'App',

  components: {
    InputMoney
  }

}
```

### Quick example

```vue
<template>
  <input-money v-model="price" />
</template>

<script>
import InputMoney from 'vue-input-money'

export default {

  name: 'App',

  components: {
    InputMoney
  },

  data: () => ({
    price: ''
  })

}
</script>
```

## License

InputMoney is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT)

