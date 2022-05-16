<template>
    <div>
        {{ foo }}=={{hi}}
    </div>
</template>

<script>
import { inject } from "vue";
export default {
    props: ['hi'],
    setup() {      

        const foo = inject('foo');

        return { foo}
    }
}
</script>

<style lang="scss" scoped>
</style>