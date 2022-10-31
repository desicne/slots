<template>
    <div class="flex">
        <input 
            type="text" 
            :placeholder="placeholder"
            v-model="name">
        <div 
            class="button"
            :class="{ 'blue-button': active }"
            @click="$emit('action', name)">
            <slot></slot>
        </div>
    </div>
</template>
<script>
export default {
    props: [ 'active', 'placeholder' ],
    data() {
        return {
            name: ''
        }
    }
}
</script>
<style scoped>
.flex {
    display: flex;
    align-content: center;
    justify-content: space-between;
    margin-bottom: 4px;
}
input {
    margin-top: 4px;
    padding: 10px 12px;
    border-radius: 4px;
    border: 1px solid lightgray;
    height: fit-content;
    width: -webkit-fill-available;
    outline: none;
}
.button {
    display: inline-block;
    padding: 8px 16px;
    border-radius: 4px;
    margin: 4px;
    margin-left: 12px;
    color: white;
    background: #387364;
    width: -webkit-fill-available;
    text-align: center;
    font-size: 14px;
}
.blue-button {
    background: #375673;
    width: auto;
}
</style>