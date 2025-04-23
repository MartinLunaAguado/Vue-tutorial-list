<script setup>
const props = defineProps({
  msg: String
})
</script>

<template>
    <li>
        <span>{{ msg || 'No props passed yet' }}</span>
    </li>
</template>