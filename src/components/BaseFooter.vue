<template>
  <footer>
    <section v-html="copy"></section>
    <button @click="send">clickme</button>
    <button>clickme</button>
  </footer>
</template>

<script>
export default {
  setup(props,{emit}) {
    const copy = `Copyright &copy; 2022 www.cvit.edu.cn All rights reserved.`;
    function send(){
      emit('ok',"我是来自BaseFooter");
    }
    return { copy,send };
  },
};
</script>

<style scoped>
footer > section {
  text-align: center;
}
</style>
