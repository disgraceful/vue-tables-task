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
      <b-form-group label="Name" label-for="name-input">
        <b-form-input
          id="name-input"
          :state="validateState('name')"
          v-model.trim="$v.name.$model"
        ></b-form-input>
        <b-form-invalid-feedback id="input-1-live-feedback">{{
          getErrorMsg("name")
        }}</b-form-invalid-feedback>
      </b-form-group>

      <b-form-group label="Surname" label-for="surname-input">
        <b-form-input
          id="surname-input"
          :state="validateState('surname')"
          v-model.trim="$v.surname.$model"
        ></b-form-input>
        <b-form-invalid-feedback id="input-1-live-feedback">{{
          getErrorMsg("surname")
        }}</b-form-invalid-feedback>
      </b-form-group>

      <b-form-group label="Email" label-for="email-input">
        <b-form-input
          id="email-input"
          :state="validateState('email')"
          v-model.trim="$v.email.$model"
        ></b-form-input>
        <b-form-invalid-feedback id="input-1-live-feedback">{{
          getErrorMsg("email")
        }}</b-form-invalid-feedback>
      </b-form-group>
    </form>
  </b-modal>
</template>

<script>
import { required, minLength, email } from "vuelidate/lib/validators";
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

  validations: {
    name: {
      required,
      minLength: minLength(4),
    },
    surname: {
      required,
      minLength: minLength(4),
    },
    email: {
      required,
      email,
    },
  },

  computed: {
    isEdit() {
      return this.user && this.mode == "edit";
    },
  },
  methods: {
    validateState(propName) {
      const { $dirty, $error } = this.$v[propName];
      return $dirty ? !$error : null;
    },

    getErrorMsg(propName) {
      const error = this.$v[propName];
      if (!error.required) {
        return `${propName} is required!`;
      }

      if (error.minLength !== undefined && !error.minLength) {
        return `${propName} must be 4 symbols or longer!`;
      }

      if (error.email !== undefined && !error.email) {
        return `Please enter valid email!`;
      }
    },
    resetModal() {
      this.name = this.isEdit ? this.user.name : "";
      this.surname = this.isEdit ? this.user.surname : "";
      this.email = this.isEdit ? this.user.email : "";
      this.$v.$reset(); //reset valdiation errors
    },

    validateForm() {
      this.$v.name.$touch();
      this.$v.surname.$touch();
      this.$v.email.$touch();
      if (
        this.$v.name.$anyError ||
        this.$v.surname.$anyError ||
        this.$v.email.$anyError
      ) {
        return false;
      }
      return true;
    },

    submit(event) {
      event.preventDefault();
      if (!this.validateForm() || !this.okFnc) {
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
