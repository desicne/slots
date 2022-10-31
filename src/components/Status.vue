<template>
    <div class="fixed-size">
        <div class="circle" :style="circleColor">
        </div>
    </div>
</template>
<script>
export default {
    props: ['status'],
    computed: {
        circleColor() {
            return {
                background: this.status
            }
        }
 }
}
</script>
<style>
.circle {
    width: 8px;
    height: 8px;
    margin-top: 8px;
    margin-left: calc(50% - 4px);
    border-radius: 50%;
}
</style>