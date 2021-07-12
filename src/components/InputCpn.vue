<template>
  <div class="input">
    <input type="text" v-model="value">
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, SetupContext, watch } from 'vue'
export default defineComponent({
  name: 'input-cpn',
  props: {
    modelValue: String
  },
  setup (props, {emit}: SetupContext) {
    const value = ref('')
    watch(() => value.value, (val: string) => {
      emit('update:modelValue', val) // 监听value，emit到父组件绑定的v-model，实现跨组件双向绑定
      emit('input', val) // 绑定input事件，并传值
    })
    return {
      value
    }
  }
})
</script>

<style lang="less" scoped>
.input {
  height: 100px;
  width: 100%;
  background: lightseagreen;
  input {
    height: 30px;
    width: 200px;
    outline: 0;
    margin-top: 20px;
  }
}
</style>