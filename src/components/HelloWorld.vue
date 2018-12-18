<template>
  <div class="hello">
<select2/>
<select21/>
<bdsrc/>
  </div>
</template>

<script>
import select2 from '@/components/select2'
import select21 from '@/components/select21'
import bdsrc from '@/components/bdsrc'
export default {
  name: 'HelloWorld',
  components:{
    select2,
    bdsrc,
    select21
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
