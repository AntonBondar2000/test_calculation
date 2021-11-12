<template>
  <div class="home">
    <OrdinaryCredit/>
  </div>
</template>

<script>
// @ is an alias to /src
import OrdinaryCredit from '@/components/OrdinaryCredit.vue'

export default {
  name: 'Home',
  components: {
    OrdinaryCredit
  }
}
</script>
