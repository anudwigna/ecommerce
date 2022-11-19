<template>
  <div>
    <p>HELLO</p>
    <button
    class="color-primary sf-button"
    :aria-disabled="false"
    :link="null"
    type="button"
    aria-label="button"
  >
    Shop now
  </button>
  <SfAlert message="Low in stock" type="danger" />
  </div>
</template>

<script>
import { SfAlert } from "@storefront-ui/vue";
export default {
  name: 'IndexPage',
  components:{
    SfAlert
  },
  mounted(){
  }
}
</script>
