<template>
  <div>
    {{msg}}===={{count}}
    <button @click="add()">{{count}}</button>
    <div>{{people.name}}{{people.age}}</div>
    <p>{{len}}</p>
    <sub-comp :hi="msg"></sub-comp>
  </div>
</template>

<script>
import {ref,reactive,computed,provide} from 'vue'
import SubComp from './components/SubComp.vue'

export default {
  setup () {
    let msg="Hello World!";
    msg="Hello Vue3.x";
    let count=ref(1);
    let people={name:'Linda',age:30}
    people=reactive(people);
    people.age=40;   
    let mydata=[4,5,6,7,8];
    let len=computed(()=>mydata.length);
    provide('foo', 'bar');
    // console.log(count);
    function add(){
        count.value++;
    }
    return {msg,count,add,people,len}
  }
  ,
  components:{
    SubComp,
  }
}
</script>

<style lang="scss" scoped>

</style>

<style lang="scss" scoped>

</style>