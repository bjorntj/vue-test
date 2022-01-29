<template>
  <app-link
      v-bind="$attrs"
      class="group flex items-center px-2 py-2 text-sm font-medium rounded-md"
      active-class="bg-gray-700 dark:bg-gray-600 text-white "
      inactive-class="text-gray-300 hover:bg-gray-600 dark:hover:bg-gray-800 hover:text-white"
  >
    <component
        :is="navicon"
        class="mr-3 flex-shrink-0 h-6 w-6"
        aria-hidden="true"
    />
    <slot />
  </app-link>
</template>

<script>
import AppLink from "@/components/AppLink.vue";

export default {
  props: ['navicon'],
  components: {
    AppLink
  }
}

</script>