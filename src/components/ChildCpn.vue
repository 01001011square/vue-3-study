<template>
  <div class="child">
    <p>This is Child</p>
    <p>Info: {{attrs}}</p>
    <button @click="childChangeVal">ChangeGrandVal</button>
    <slot name="child-slot">child: {{attrs.b}}</slot>
    <ul>
      <li v-for="(item, index) in items" :key="index">
        <slot :item="item"></slot>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { defineComponent, SetupContext } from 'vue'

export default defineComponent({
  name: 'Child',
  emits: ["changeVal"],
  setup (props, {attrs, emit}: SetupContext) {
    const childChangeVal = () => {
      emit('changeVal', 'c333')
    }
    return {
      attrs,
      childChangeVal,
      items: ['Feed a cat', 'Buy milk']
    }
  }
})
</script>

<style lang="less">
.child {
  margin: 20px;
  padding: 20px;
  background: lightcoral;
}
</style>