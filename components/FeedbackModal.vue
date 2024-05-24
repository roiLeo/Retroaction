<template>
  <UModal v-model="isOpen">
    <UCard>
      <template #header>
        <div class="flex items-center justify-between">
          <div v-if="!selectedOption">
            <p class="text-lg font-medium text-gray-600 dark:text-gray-50">Give us feedback</p>
            <p class="text-sm text-gray-500">Tell us how we could make the product more useful for you.</p>
          </div>
          <div v-else>
            <p class="text-lg font-medium text-gray-600 dark:text-gray-50">{{ selectedOption.icon }} {{ selectedOption.label }}</p>
          </div>
          <UButton color="gray" variant="ghost" icon="i-heroicons-x-mark-20-solid" class="-my-1 hover:bg-gray-100 dark:hover:bg-gray-700" @click="closeModal" />
        </div>
      </template>
      <div class="space-y-3" v-if="!selectedOption">
        <UButton v-for="button in buttonsList" :key="button" size="xl" color="gray" variant="solid" block @click="selectedOption = button">
          <template #leading>
            <div class="px-1 py-0.5 group-hover:shadow-none main-transition group-hover:dark:bg-white/10 dark:bg-white/5 bg-gray-100/40 group-hover:bg-gray-100/60 rounded-md">
              {{ button.icon }}
            </div>
          </template>
          <div class="flex justify-between w-full">
            {{ button.label }}
          </div>
          <template #trailing>
            <UKbd class="border-l">{{ button.kbd }}</UKbd>
          </template>
        </UButton>
        <!-- <div class="text-center">
          <p>Count: {{ count }}</p>
          <UButton @click="onSuccess">
            Click to emit a success event
          </UButton>
        </div> -->
      </div>
      <div v-else>
        <FeedbackForm @back-to-list="selectedOption = undefined" @send-feedback="onSuccess" />
      </div>
    </UCard>
  </UModal>
</template>

<script lang="ts" setup>
defineProps({
  count: {
    type: Number,
    default: 0
  }
})

const emit = defineEmits(['success'])

const isOpen = ref(false)
const selectedOption = ref()

const buttonsList = [
  { icon: '💡', label: 'Feature Request', kbd: 1 },
  { icon: '🐛', label: 'Bugs', kbd: 2 },
  { icon: '📥', label: 'Feedback', kbd: 3 },
  { icon: '🔗', label: 'Integrations', kbd: 4 },
  { icon: '🤔', label: 'Question', kbd: 5 },
]

const closeModal = async () => {
  const modal = useModal()
  modal.close()
  isOpen.value = false
}

const onSuccess = () => {
  console.log('yolo')
  closeModal()
  emit('success')
}
</script>
