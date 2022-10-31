<template>
    <div class="min-width small-font mr-8">
        <slot></slot>
    </div>
</template>
<style>
.min-width {
    min-width: 60px;
}

.small-font {
    font-size: 14px;
}

.mr-8 {
    margin-right: 8px;
}
</style>