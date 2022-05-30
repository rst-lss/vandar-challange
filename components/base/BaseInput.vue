<template>
  <v-text-field
    class="base-input"
    :value="value"
    v-bind="$attrs"
    persistent-placeholder
    solo
    flat
    dense
    @input="$emit('input', $event)"
  >
    <!-- passing slot from parent to v-text-field component -->
    <template v-for="(index, name) in $slots" #[name]>
      <slot :name="name"></slot>
    </template>
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

<style scoped lang="scss">
.base-input {
  position: relative;
  direction: rtl;

  &::v-deep .v-input__slot {
    border: 1px solid #d5d5d5;
  }

  &::v-deep .v-text-field__details {
    position: absolute;
    margin: 2px 0 0;
    left: 100%;
    z-index: 999;

    .v-messages__message {
      background-color: #f44336;
      color: #fff;
      padding: 10px;
      border-radius: 6px;
      text-align: center;
      white-space: nowrap;
      position: relative;

      &::after {
        content: '';
        position: absolute;
        top: 40%;
        right: 100%;
        border: 5px;
        border-color: transparent #f44336 transparent transparent;
        border-style: solid;
      }
    }
  }
}
</style>
