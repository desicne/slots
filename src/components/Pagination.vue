<template>
    <div>
        Page <slot></slot> of {{ total }}
    </div>
</template>
<script>
export default {
    props: ['total']
}
</script>