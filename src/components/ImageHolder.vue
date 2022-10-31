<template>
    <div class="fixed-size">
        <img v-if="image" :src="image" :alt="title" class="fixed-size">
        <div v-else></div>
    </div>
</template>
<script>
export default {
    props: ['image', 'title']
}
</script>