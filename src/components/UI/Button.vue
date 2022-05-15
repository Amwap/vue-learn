<template>
    <button class="btn"> <slot></slot> </button>    
</template>
    
<script>
export default {
    name: "Button"
}
</script>
<style scoped>
.btn{
    padding: 10px 15px;
    background: none;
    color: teal;
    border: 1px solid teal;
    transition: 0.3s;
}
.btn:hover{
    background: teal;
    color: white;
    transition: 0.3s;
}
</style>