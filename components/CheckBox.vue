<template>
  <div class="checkbox-container" @click="toggle">
    <input class="checkbox-input" type="checkbox" :isChecked="isChecked" />
    <span
      :id="id"
      role="checkbox"
      class="checkbox-checkbox"
      :class="{ checked: isChecked }"
    >
      <ph-check v-if="isChecked" class="icon" />
    </span>
    <label :for="id">{{ label }}</label>
  </div>
</template>

<script>
import { PhCheck } from 'phosphor-vue'

export default {
  name: 'check-box',
  components: {
    PhCheck,
  },
  props: {
    id: {
      type: String,
      required: true,
    },
    label: {
      type: String,
      required: false,
      default: null,
    },
    value: {
      required: false,
    },
    checked: {
      type: Boolean,
      required: true,
    },
  },
  data() {
    return {
      isChecked: this.checked,
    }
  },
  methods: {
    toggle(event) {
      event.preventDefault()
      console.log(this.value)
      this.isChecked = !this.isChecked
    },
  },
}
</script>

<style scoped>
.checkbox-container {
  display: flex;
  gap: 8px;
}
.checkbox-input {
  position: absolute;
  width: 0;
  height: 0;
  opacity: 0;
  pointer-events: none;
}
.checkbox-checkbox {
  border: 1px solid #a9b6c7;
  background-color: white;
  border-radius: 4px;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s;
  width: 20px;
  height: 20px;
}
.checked {
  background-color: #20c4f4;
  border-color: #20c4f4;
}
.icon {
  transform: scale(1.25);
  color: white;
}
</style>
