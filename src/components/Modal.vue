<template>
  <b-modal id="modal" :value="showModal" @input="$emit('input', $event)">
    <form ref="form" @submit.stop.prevent="handleSubmit">
      <b-form-group
        label="Name"
        label-for="name-input"
        invalid-feedback="Name is required"
      >
        <b-form-input id="name-input" required></b-form-input>
      </b-form-group>
    </form>
  </b-modal>
</template>

<script>
export default {
  props: {
    showModal: Boolean,
  },
};
</script>
