<template>
  <v-text-field
    class="base-input"
    :value="value"
    v-bind="$attrs"
    placeholder="نام"
    persistent-placeholder
    solo
    flat
    dense
    @input="$emit('input', $event)"
  >
  </v-text-field>
</template>

<script>
export default {
  name: 'BaseInput',
  props: {
    value: {
      type: [String, Number],
      default: '',
    },
  },
}
</script>

