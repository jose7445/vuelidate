<template>
  <div>
    <b-form>
      <!-- ROW 5: CONTACT, Mails to notify -->
      <b-row class="mt-3">
        <b-col>
          <b-form-group id="input-group-contacts">
            <div class="d-flex align-items-center mb-1">
              <label for="input-contacts" class="mb-0"
                >Emails para notificaciones</label
              >
              <b-button
                @click="form.contacts.push('')"
                class="pr-3 pl-1 py-0 label ml-2 text-primary text-small d-flex align-items-center"
                size="sm"
                variant="outline-secondary"
                ><i class="pi pi-plus mr-1" style="font-size: 0.7rem"></i
                >+</b-button
              >
            </div>

            <b-col
              v-for="(email, index) in form.contacts"
              :key="index"
              cols="4"
              class="mt-3"
            >
              <div class="d-flex align-items-center">
                <b-form-input
                  id="input-contacts"
                  size="sm"
                  v-model="form.contacts[index]"
                  :state="isValidEmail(form.contacts[index], index)"
                >
                </b-form-input>

                <b-button
                  @click="form.contacts.splice(index, 1)"
                  size="md"
                  variant="light"
                  class="p-1 ml-1 text-secondary d-flex align-items-center"
                  ><i class="pi pi-times"></i
                ></b-button>
              </div>
              <b-form-invalid-feedback
                :state="isValidEmail(form.contacts[index], index)"
                >Correo incorrecto.</b-form-invalid-feedback
              >
            </b-col>
          </b-form-group>
        </b-col>
      </b-row>
      <b-button variant="danger" type="submit" @click="submit">Button</b-button>
    </b-form>
  </div>
</template>

<script>
import { useVuelidate } from "@vuelidate/core";
import { required, email } from "@vuelidate/validators";

export default {
  setup() {
    return { v$: useVuelidate() };
  },
  name: "HelloWorld",
  props: {
    msg: String,
  },

  data() {
    return {
      form: {
        contacts: [],
      },
    };
  },

  validations: {
    form: {
      contacts: {
        required,
        email,
      },
    },
  },
  computed: {},
  methods: {
    isValidEmail(email) {
      const regex = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
      const dirty = this.v$.contacts;
      return dirty ? regex.test(email) : null;
    },

    submit(e) {
      e.preventDefault();
      console.log("data");

      this.v$.form.$touch();
      console.log(this.v$.$errors);
      if (this.v$.$errors) {
        return;
      } else {
        alert.window("envado");
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
