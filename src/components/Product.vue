<template>
    <div class="product-align">
        <slot></slot>
    </div>
</template>
<style>
.product-align {
    display: flex;
    justify-content: flex-start;
    align-content: center;
    align-items: center;
    margin-top: 8px;
    padding: 8px 0;
    border-bottom: 1px solid lightgray;
}
</style>