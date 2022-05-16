<template>
  <base-todo></base-todo>
  <base-footer></base-footer>
</template>

<script>
import BaseTodo from './components/BaseTodo.vue'
import BaseFooter from './components/BaseFooter.vue'
export default {
  components:{
    BaseTodo,BaseFooter
  },
  setup () {
    

    return {}
  }
}
</script>

<style>
@import url("./assets/base.css");


</style>