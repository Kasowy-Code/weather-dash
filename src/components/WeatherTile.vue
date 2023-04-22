<script setup>
defineProps({
  description: {
    type: String,
    required: true
  },
  value: {
    required: true
  },
  unit: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div>
    <slot class="iconContainer">
    </slot>
    <div class="infoContainer">
      <span class="description">{{ description }}</span>
      <h3>
        {{ value }} {{ unit }}
      </h3>
      </div>
  </div>
</template>
