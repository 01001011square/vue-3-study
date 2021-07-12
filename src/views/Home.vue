<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" :name="name" :age="age" /> -->
    <Parent :a="a" :b="b" v-on:changeVal="changeVal"/>
    <p>{{a}}</p>
    <p>{{message}}</p>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
// import HelloWorld from '@/components/HelloWorld.vue'; // @ is an alias to /src
import Parent from '@/components/ParentCpn.vue'
import MixDemo from '@/mixins/MixDemo.vue'

export default defineComponent({
  name: 'Home',
  components: {
    // HelloWorld,
    Parent
  },
  mixins: [MixDemo],
  setup () {
    let name = ref('william')
    const age = 27
    let a = ref('a111')
    const b = 'b222'
    const changeVal = (val: string) => {
      a.value = val
    }
    return {
      name,
      age,
      a,
      b,
      changeVal
    }
  }
});
</script>
