<template>
  <div :style="'background-color:' + color">
    <span class="colorText" v-if="displayHex">
      {{color}}
    </span>
  </div>
</template>
s
<script>
export default {
  props: {
    color: {
      type: String
    },
    displayHex: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {

    }
  },
}
</script>

<style lang="scss">

  

</style>
