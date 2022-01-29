<!-- eslint-disable -->
<template>
<!--  <a v-if="isExternalLink" v-bind="$attrs" :href="to" target="_blank">
    <slot />
  </a>-->
  <router-link
      v-bind="$props"
      custom
      v-slot="{ isActive, href, navigate }"
  >
    <a
        v-bind="$attrs"
        :href="href"
        @click="navigate"
        :class="isActive ? activeClass : inactiveClass"
    >
      <slot />
    </a>
  </router-link>
</template>

<script >
import { RouterLink } from 'vue-router'
/*import { computed } from "vue";*/

export default {
  name: 'AppLink',
  inheritAttrs: false,

  props: {
    // add @ts-ignore if using TypeScript
    ...RouterLink.props,
    inactiveClass: String,
  },

  /*setup(props) {
    const isExternalLink = computed(() => typeof this.to === 'string' && this.to.startsWith('http'))

    return {
      isExternalLink
    }
  }*/
}
</script>
