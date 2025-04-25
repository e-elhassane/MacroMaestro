<template>
  <div class="modal">
    <h3>Set Action for {{ keyLabel }}</h3>
    <label>Action</label>
    <input v-model="action" placeholder="e.g. Send, Hello" />

    <label>Modifier (optional)</label>
    <select v-model="modifier">
      <option value="">None</option>
      <option value="Shift">Shift</option>
      <option value="Ctrl">Ctrl</option>
      <option value="Alt">Alt</option>
    </select>

    <button @click="save">Save</button>
  </div>
</template>

<script>
export default {
  props: ['keyLabel'],
  data() {
    return {
      action: '',
      modifier: ''
    }
  },
  methods: {
    save() {
      this.$emit('save', {
        key: this.keyLabel,
        action: this.action,
        modifier: this.modifier
      })
    }
  }
}
</script>