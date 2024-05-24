<template>
  <form @submit.prevent="submitFeedback">
    <UInput v-model="feedback.title" size="xl" placeholder="Add a title" required />
    <UTextarea v-model="feedback.description" size="xl" placeholder="Describe your request" class="mt-3" />
    <UInput v-model="feedback.email" size="xl" type="email" placeholder="you@example.com" icon="i-heroicons-envelope" class="mt-3" />
    <div class="flex justify-between w-full gap-3 mt-4 bottom-3">
      <UButton color="white" variant="solid" icon="i-heroicons-chevron-left" @click="emit('backToList')" />
      <UButton type="submit" icon="i-heroicons-paper-airplane">
        Submit
      </UButton>
    </div>
  </form>
</template>

<script lang="ts" setup>
const emit = defineEmits(['backToList', 'sendFeedback'])

const feedback = reactive({
  title: '',
  description: '',
  email: ''
})

const submitFeedback = () => {
  console.log(feedback)
  emit('sendFeedback')
}
</script>
