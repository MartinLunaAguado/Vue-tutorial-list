<script setup>
const emit = defineEmits(['response'])




emit('response', 'hello from child')

const props = defineProps({
  msg: String
})
</script>

<template>
    <li>
        <span>{{ msg || 'No props passed yet' }}</span>
    </li>
    <li>        <slot> Fallback content </slot>
    </li>
</template>