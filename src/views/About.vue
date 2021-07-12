<template>
  <div class="about">
    <h1>This is an about page: {{ txtData }}</h1>
    <InputCpn v-model="txtData"></InputCpn>
    <p>{{message}}</p>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue'
import InputCpn from '@/components/InputCpn2.vue' 
import MixDemo from '@/mixins/MixDemo.vue'

export default defineComponent({
  components: {
    InputCpn
  },
  mixins: [MixDemo],
  setup () {
    const txtData = ref('about')
    return {
      txtData
    }
  }
})
</script>
