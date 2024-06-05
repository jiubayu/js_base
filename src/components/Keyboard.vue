<template>
    <div>
        <p>选择的键</p>
        <textarea ref="text">{{ key }}</textarea>
    </div>
</template>

<script>
    export default {
       name: 'Keyboard',
       data(){
        return {
            key: ''
        }
       },
       mounted() {
        document.addEventListener('keydown', (e) => {
            // console.log( e.key)
            this.key = e.key;
        })
       }
    }
</script>

<style lang="scss" scoped>

</style>