<script lang="ts">
import { defineComponent } from 'vue'
export default defineComponent({
  data() {
    return {
      message: 'Hello from mixin'
    }
  },
  created() {
    console.log(this.$data);
  }
})
</script>