<script setup lang="ts">
import { Codemirror } from 'vue-codemirror'

import { oneDark } from '@codemirror/theme-one-dark'
import type { Paste } from '~/composables/types'

const { paste } = defineProps<{ paste: Paste }>()
const emits = defineEmits(['setCode', 'setType', 'setExpiredDays'])

function setCode(code: string) {
  emits('setCode', code)
}

const languagesFunction = languages[paste.type as keyof typeof languages]
const extensions = [oneDark]

if (languagesFunction)
  extensions.push(languagesFunction)
</script>

<template>
  <codemirror
    :model-value="paste.data"
    placeholder="Code goes here..."
    :style="{ height: '400px', width: '900px', textAlign: 'left' }"
    :autofocus="true"
    :indent-with-tab="true"
    :tab-size="2"
    :extensions="extensions"
    @change="setCode"
  />
</template>

