<template>
  <b-modal :id="id" title="Confirm Deletion" ref="modal" @ok="submit">
    <slot></slot>
  </b-modal>
</template>

<script>
export default {
  props: {
    id: String,
    okFnc: Function,
  },
  methods: {
    submit() {
      this.okFnc();
    },
  },
};
</script>
