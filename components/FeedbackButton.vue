<template>
  <div class="z-[1000000] block fixed right-4 -rotate-90 translate-x-2/4 -translate-y-2/4 top-[45%] bottom-auto">
    <UButton
      icon="i-heroicons-sparkles"
      size="lg"
      color="primary"
      variant="solid"
      label="Feedback"
      :trailing="false"
      @click="openFeedbackModal"
    />
  </div>
</template>

<script lang="ts" setup>
import { FeedbackModal } from '#components'

const toast = useToast()
const modal = useModal()
const count = ref(0)

const openFeedbackModal = () => {
  count.value += 1
  modal.open(FeedbackModal, {
    count: count.value,
    onSuccess () {
      toast.add({
        title: 'Success !',
        id: 'modal-success'
      })
    }
  })
}
</script>
