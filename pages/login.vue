<template>
  <v-container fluid class="ma-0 pa-0">
    <v-parallax class="ma-0 pa-0" height="900" src="/images/bg1.jpeg">
      <v-row center >
        <v-col class="col-md-6 offset-md-3 pt-10" cols="12" sm="6">
          <!-- {{ errors }} -->
          <strong class="ma-2 pa-2 mt-10 pt-10 text-h6">Login : </strong>

        </v-col>
      </v-row>
    </v-parallax>
  </v-container>
</template>

<script>
import Vue from "vue";
import NProgress from "nprogress";
import "nprogress/nprogress.css";
import { validationMixin, Vuelidate } from "vuelidate";
import { required, email, minLength } from "vuelidate/lib/validators";

Vue.use(Vuelidate);

export default {
  loading: {
    color: "blue",
    height: "20px"
  },

  mixins: [validationMixin],
  validations: {
    email: { required, email },
    password: { required, minLength: minLength(6) }
  },
  mounted() {
    this.$nextTick(() => {
      this.$nuxt.$loading.start();
      setTimeout(() => this.$nuxt.$loading.finish(), 2000);
    });
  },
  data: () => ({
    alert: "d-none",
    error_msg: "",
    loading: false,
    email: null,
    password: "",
    form: {
      email: "",
      password: ""
    },

    show1: false,
    rules: {
      required: value => !!value || "Required.",
      min: v => v.length >= 6 || "Min 6 characters"
    }
  }),
  computed: {
    emailErrors() {
      const errors = [];
      if (!this.$v.email.$dirty) return errors;
      !this.$v.email.email && errors.push("Must be valid e-mail");
      !this.$v.email.required && errors.push("E-mail is required");
      return errors;
    },
    passwordErrors() {
      const passerrors = [];
      if (!this.$v.password.$dirty) return passerrors;
      !this.$v.email.required && passerrors.push("Password is required");
      return passerrors;
    }
  },

  methods: {

  }
};
</script>

