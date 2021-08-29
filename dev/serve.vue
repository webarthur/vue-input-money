<script>
import { defineComponent } from 'vue';
import InputMoney from '@/input-money.vue';

export default defineComponent({
  name: 'ServeDev',
  components: {
    InputMoney
  }
});
</script>

<template>
  <div id="app">
    <input-money />
  </div>
</template>
