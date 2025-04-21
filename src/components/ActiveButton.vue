<!-- ActiveButton.vue -->
<script setup>
const props = defineProps({
  modelValue: Boolean
})

const emit = defineEmits(['update:modelValue'])

const toggle = () => {
  emit('update:modelValue', !props.modelValue)
}
</script>

<template>
  <button 
    @click="toggle"
    :class="{ 'active': modelValue }"
    class="toggle-btn"
  >
    <span class="slider"></span>
  </button>
</template>

<style scoped>
.toggle-btn {
  position: relative;
  width: 50px;
  height: 24px;
  border-radius: 12px;
  background: #ccc;
  border: none;
  cursor: pointer;
}

.toggle-btn.active {
  background: #42b983;
}

.slider {
  position: absolute;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: white;
  top: 2px;
  left: 2px;
  transition: transform 0.2s;
}

.toggle-btn.active .slider {
  transform: translateX(26px);
}
</style>