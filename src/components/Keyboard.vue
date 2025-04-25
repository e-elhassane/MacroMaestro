<template>
  <div class="keyboard">
    <Key
      v-for="key in keys"
      :key="key.label"
      :label="key.label"
      @click="handleClick(key)"
    />
  </div>
</template>

<script>
import Key from './Key.vue'

export default {
  components: { Key },
  data() {
    return {
      keys: [
        { label: 'A' }, { label: 'B' }, { label: 'C' }, { label: 'D' },
        { label: 'E' }, { label: 'F' }, { label: 'G' }
      ]
    }
  },
  methods: {
    handleClick(key) {
      this.$emit('key-selected', key)
    }
  }
}
</script>