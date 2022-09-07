<template>
  <modal title="Modal with form" @close="$emit('close')">
    <div slot="body">
      <form @submit.prevent="onSubmit">
        <div class="form-item" :class="{ errorInput: $v.name.$error }">
          <label>Name:</label>
          <p class="errorText" v-if="$v.name.required">Field is required!</p>
          <p class="errorText" v-if="$v.name.minLength">
            Name must have at least 4!
          </p>

          <input
            v-model="name"
            :class="{ error: $v.name.$error }"
            @change="$v.name.$touch()"
          />
        </div>

        <!-- email -->

        <div class="form-item" :class="{ errorInput: $v.email.$error }">
          <label>Email:</label>
          <p class="errorText" v-if="$v.email.required">Field is required!</p>
          <p class="errorText" v-if="$v.email.email">Email is not correct!</p>

          <input
            v-model="email"
            :class="{ error: $v.email.$error }"
            @change="$v.email.$touch()"
          />
        </div>

        <!-- password -->
        <div class="form-item" :class="{ errorInput: $v.password.$error }">
          <label>Password:</label>
          <p class="errorText" v-if="$v.password.required">
            Field is required!
          </p>
          <p class="errorText" v-if="$v.password.minLength">
            Password must have at least 6!
          </p>

          <input
            type="password"
            v-model="password"
            :class="{ error: $v.password.$error }"
            @change="$v.password.$touch()"
          />
        </div>

        <!-- repeat password -->

        <div class="form-item" :class="{ errorInput: $v.password.$error }">
          <label>Password:</label>
          <p class="errorText" v-if="$v.password.required">
            Field is required!
          </p>
          <p class="errorText" v-if="$v.password.minLength">
            Password must have at least 6!
          </p>

          <input
            type="password"
            v-model="passwordRepeat"
            :class="{ error: $v.password.$error }"
            @change="$v.password.$touch()"
          />
        </div>
        <p
          v-if="password != passwordRepeat"
          @change="$v.password.$touch()"
          style="color: red"
        >
          Password doesn't match
        </p>
        <!-- button -->

        <button class="btn btnPrimary">Well done</button>
      </form>
    </div>
  </modal>
</template>

<script>
import { required, minLength, email } from "vuelidate/lib/validators";

import modal from "@/components/Modal.vue";
export default {
  components: {
    modal,
  },
  data() {
    return {
      name: "",
      email: "",
      password: "",
      passwordRepeat: "",
    };
  },
  validations: {
    name: {
      required,
      minLength: minLength(4),
    },
    email: {
      required,
      email,
    },
    password: {
      required,
      minLength: minLength(6),
    },
  },
  methods: {
    onSubmit() {
      this.$v.$touch();
      if (this.password == this.passwordRepeat) {
        if (!this.$v.$invalid) {
          const user = {
            name: this.name,
            email: this.email,
            password: this.password,
          };
          console.log(user);
          this.name = "";
          this.email = "";
          this.password = "";
          this.passwordRepeat = "";
          this.$v.$reset();
          this.$emit("close");
        }
      }
    },
  },
};
</script>

<style lang="scss">
.form-item .errorText {
  display: none;
  margin-bottom: 8px;
  font-size: 13.4px;
  color: #e23737;
}

.form-item {
  &.errorInput .errorText {
    display: block;
  }
}

input.error {
  border-color: #e23737;
}
</style>