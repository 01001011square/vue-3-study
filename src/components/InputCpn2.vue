<template>
  <div class="input-wrap">
    <input type="text" :value="targetVal" @input="updateValue">
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, SetupContext } from 'vue'
export default defineComponent({
  name: 'InputCpn2',
  props:{
    modelValue: String
  },
  setup (props, { emit }: SetupContext) {
    const targetVal = ref('hello')
    const updateValue = (e: KeyboardEvent) => {
      targetVal.value = (e.target as HTMLInputElement).value
      emit('update:modelValue', targetVal.value)
    }
    return {
      targetVal,
      updateValue
    }
  }
})
</script>

<style lang="less" scoped>
  .input-wrap {
    margin: 0 auto;
    padding: 20px;
    background: lightsteelblue;
    input {
      height: 30px;
      width: 200px;
      outline: 0;
      margin-top: 20px;
    }
  }
</style>