<template>
  <div>
    <div v-html-safe="message"></div>
  </div>
</template>
<script>
import Vue from 'vue'
import VueSecureHTML from 'vue-html-secure'

Vue.use(VueSecureHTML)

export default {
  /*
  data() {
    return {
      message:
        'Modifiers are special postfixes denoted by a dot, which indicate that a directive should be bound in some special way. For example, the <code>.prevent</code> modifier tells the <code>v-on</code> directive to call <code>event.preventDefault()</code> on the triggered event:',
    }
  },
  */
  props: {
    message: {
      type: String,
      default: '',
    },
  },
}
</script>
