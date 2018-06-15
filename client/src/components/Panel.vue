<template>
  <div class="white elevation-2">
    <v-toolbar class="cyan" dark flat dense>
      <v-toolbar-title>{{title}}</v-toolbar-title>
      <v-spacer></v-spacer>
      <slot name="add"></slot>
    </v-toolbar>

    <div class="pl-4 pr-4 pt-2 pb-2">
      <slot>
        no slot content defined
      </slot>
    </div>
  </div>
</template>

<script>
export default {
  props: [
    'title'
  ]
}
</script>

<style>

</style>
