<template>
  <div class="btn-group btn-group-sm mb-3 d-flex justify-content-center align-items-center" role="group" aria-label="Small button group">
    <button 
      type="button" 
      class="btn btn-outline-light"
      @click="emit('preview')"
      :disabled="start <= 0"
    >
      Preview
    </button>

    <button 
      type="button" 
      class="btn btn-outline-light"
      @click="nextActive"
      :disabled="end >= dataLength"
    >
      Next
    </button>
  </div>
</template>

<script setup>

  defineProps({
		start: Number,
		end: Number,
    dataLength: Number,
	})

  const emit = defineEmits([
		'preview',
		'next'
	])

  const nextActive = () => {
    console.log("next clicked")
    emit('next')
  }
</script>

<style lang="scss" scoped>

</style>