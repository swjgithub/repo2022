<template>
    <footer>
        <section v-html="copy"></section>
    </footer>
</template>

<script>
export default {
    setup () {
        const copy=`Copyright &copy; 2022 www.cvit.edu.cn All rights reserved.`;

        return {copy}
    }
}
</script>

<style scoped>
   footer>section {
       text-align: center;
   }
</style>