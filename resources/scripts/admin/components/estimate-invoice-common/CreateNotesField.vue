<template>
  <div class="mb-6">
    <div
      class="z-20 text-sm font-semibold leading-5 text-primary-400 float-right"
    >
      <SelectNotePopup :type="type" @select="onSelectNote" />
    </div>
    <label class="text-gray-800 font-medium mb-4 text-sm">
      {{ $t('invoices.notes') }}
    </label>
    <BaseCustomInput
      v-model="store[storeProp].notes"
      :content-loading="store.isFetchingInitialSettings"
      :fields="fields"
      class="mt-1"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import SelectNotePopup from '../SelectNotePopup.vue'

const props = defineProps({
  store: {
    type: Object,
    default: null,
  },
  storeProp: {
    type: String,
    default: '',
  },
  fields: {
    type: Object,
    default: null,
  },
  type: {
    type: String,
    default: null,
  },
})

function onSelectNote(data) {
  const currentNotes = props.store[props.storeProp].notes || ''
  const newNotes = data.notes || ''
  
  // Only append if new notes have content
  if (!newNotes.trim()) {
    return
  }
  
  // If there are existing notes, append with a separator
  if (currentNotes.trim()) {
    props.store[props.storeProp].notes = currentNotes + '\n\n' + newNotes
  } else {
    props.store[props.storeProp].notes = newNotes
  }
}
</script>
