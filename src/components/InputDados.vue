<template>
  <q-input :type="type" :placeholder="placeholder" v-model="model" outlined/>
</template>

<script setup lang="ts">
interface Props {
  type?: 'text' | 'number' | 'date'
  placeholder?: string
}

withDefaults(defineProps<Props>(), {
  type: 'text',
  placeholder: ''
})

const model = defineModel<string | number | null>()
</script>
