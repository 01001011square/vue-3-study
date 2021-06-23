<template>
  <div class="parent">
    <p>This is Parent</p>
    <p>Info: {{ a }}</p>
    <ChildCpn v-bind="$attrs">
      <template v-slot:child-slot>
        <p>parent-cover: {{a}}</p>
      </template>
      <template v-slot:default="slotProps">
        <p>{{slotProps.item}}</p>
      </template>
    </ChildCpn>
    <InputCpn v-model="message" @input="inputHandler"></InputCpn>
    <p>{{ message || 'default'}}</p>
    <p v-show="txtShow">You can see me when you type 7 first</p>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, SetupContext } from 'vue'
import ChildCpn from '@/components/ChildCpn.vue'
import InputCpn from '@/components/InputCpn.vue'

export default defineComponent({
  name: 'Parent',
  props: {
    a: String
  },
  components: {
    ChildCpn,
    InputCpn
  },
  inheritAttrs: false,
  setup (props, {attrs}:SetupContext) {
    console.log(attrs)
    const txtShow = ref(false)
    const message = ref('default')
    const inputHandler = (val: string) => {
      if (val === '7') {
        txtShow.value = true
      }
      if (val === '') {
        txtShow.value = false
      }
    }
    return {
      message,
      txtShow,
      inputHandler
    }
  }
})
</script>

<style lang="less">
.parent {
  margin: 0 auto;
  padding: 20px;
  width: 400px;
  background: lightblue;
}
</style>