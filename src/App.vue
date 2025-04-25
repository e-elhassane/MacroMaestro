<template>
  <div id="app">
    <h1>Custom Keyboard AHK Generator</h1>
    <Keyboard @key-selected="openPicker" />
    <ActionPicker
      v-if="showPicker"
      :key-label="selectedKey"
      @save="saveAction"
    />
    <button @click="generateAHKScript">Download AHK Script</button>
  </div>
</template>

<script>
import Keyboard from './components/Keyboard.vue'
import ActionPicker from './components/ActionPicker.vue'

export default {
  components: { Keyboard, ActionPicker },
  data() {
    return {
      keyMappings: {},
      selectedKey: null,
      showPicker: false,
    }
  },
  methods: {
    openPicker(key) {
      this.selectedKey = key.label
      this.showPicker = true
    },
    saveAction(mapping) {
      this.keyMappings[mapping.key] = {
        action: mapping.action,
        modifier: mapping.modifier
      }
      this.showPicker = false
    },
    generateAHKScript() {
      let script = ''
      for (const [key, { action, modifier }] of Object.entries(this.keyMappings)) {
        script += `${key}::${action}\n`
        if (modifier) {
          const mod = this.getModifierSymbol(modifier)
          script += `${mod}${key}::${action}\n`
        }
      }
      const blob = new Blob([script], { type: 'text/plain' })
      const url = URL.createObjectURL(blob)
      const link = document.createElement('a')
      link.href = url
      link.download = 'custom_keys.ahk'
      link.click()
    },
    getModifierSymbol(mod) {
      const map = { Shift: '+', Ctrl: '^', Alt: '!' }
      return map[mod] || ''
    }
  }
}
</script>