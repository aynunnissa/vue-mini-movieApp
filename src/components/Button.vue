<template>
    <button class="button" @click="clickButton"><slot></slot></button>
</template>

<script>
export default {
    name: 'Button',
    props: {
        clickButton: Function
    },
}
</script>

<style scoped>
    .button {
        border: none;
        border-radius: 10px;
        padding: 10px 15px;
        display: inline-flex;
        align-items: center;
        cursor: pointer;
    }
</style>