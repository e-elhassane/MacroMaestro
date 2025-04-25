<template>
  <button class="key" @click="$emit('click')">{{ label }}</button>
</template>

<script>
export default {
  props: ['label']
}
</script>