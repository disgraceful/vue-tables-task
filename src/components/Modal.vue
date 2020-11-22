<template>
  <b-modal
    :id="id"
    title="Add User"
    ref="modal"
    @show="resetModal"
    @hidden="resetModal"
    @ok="submit"
  >
    <form ref="form">
      <b-form-group
        label="Name"
        label-for="name-input"
        invalid-feedback="Name is required"
      >
        <b-form-input id="name-input" v-model="name" required></b-form-input>
      </b-form-group>
      <b-form-group
        label="Surname"
        label-for="surname-input"
        invalid-feedback="Surname is required"
      >
        <b-form-input
          id="surname-input"
          v-model="surname"
          required
        ></b-form-input>
      </b-form-group>
      <b-form-group
        label="Email"
        label-for="email-input"
        invalid-feedback="Email is required"
      >
        <b-form-input id="email-input" v-model="email" required></b-form-input>
      </b-form-group>
    </form>
  </b-modal>
</template>

<script>
export default {
  props: {
    id: { type: String, required: true },
    mode: String,
    okFnc: Function,
    user: Object,
  },
  data() {
    return {
      name: "",
      surname: "",
      email: "",
    };
  },

  computed: {
    isEdit() {
      return this.user && this.mode == "edit";
    },
  },
  methods: {
    resetModal() {
      console.log("form reset");
      this.name = this.isEdit ? this.user.name : "";
      this.surname = this.isEdit ? this.user.surname : "";
      this.email = this.isEdit ? this.user.email : "";
    },

    submit(event) {
      event.preventDefault();
      if (!this.$refs.form.checkValidity() || !this.okFnc) {
        console.log("not valid");
        return;
      } else {
        const newUser = {
          name: this.name,
          surname: this.surname,
          email: this.email,
        };
        this.okFnc(newUser);
        this.$nextTick(() => {
          this.$bvModal.hide(this.id);
        });
        console.log("sumbitted");
      }
    },
  },
  mounted() {
    this.resetModal();
  },
};
</script>
