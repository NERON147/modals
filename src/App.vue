<template>
  <div class="wrapper">
    <div class="wrapper-content">
      <section>
        <div class="container">
          <button class="btn btnPrimary" @click="modalFirst = !modalFirst">
            Show First modal
          </button>

          <modal
            title="First modal"
            v-show="modalFirst"
            @close="modalFirst = false"
          >
            <div slot="body">
              <p>Text</p>
              <button class="btn btnPrimary" @click="modalFirst = !modalFirst">
                Well done
              </button>
            </div>
          </modal>

          <!-- second modal -->
          <button
            class="btn btnPrimary"
            @click="modalSecond.show = !modalSecond.show"
          >
            Show modal width form
          </button>

          <modal
            title="Modal with form"
            v-show="modalSecond.show"
            @close="modalSecond.show = false"
          >
            <div slot="body">
              <form @submit.prevent="submitSecondForm">
                <label>Name:</label>
                <input type="text" v-model="modalSecond.name" />

                <label>Email:</label>
                <input type="email" v-model="modalSecond.email" />

                <button class="btn btnPrimary">Well done</button>
              </form>
            </div>
          </modal>
            <!-- modal validate -->
            <button
            class="btn btnPrimary"
            @click="modalValidate = !modalValidate"
          >
            Show modal width form + validate
          </button>
          <modalValidate v-show='modalValidate' @close='modalValidate = false'/>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import modal from "@/components/Modal.vue";
import modalValidate from "@/components/ModalValidate.vue";

export default {
  components: {
    modal,
    modalValidate,
  },
  data() {
    return {
      modalFirst: false,
      modalSecond: {
        show: false,
        name: "",
        email: "",
      },
      modalValidate: false,
    };
  },
  methods: {
    submitSecondForm() {
      console.log({
        name: this.modalSecond.name,
        email: this.modalSecond.email,
      })
      this.modalSecond.name = ''
      this.modalSecond.email = ''
      this.modalSecond.show = false
    }
  }
};
</script>

<style>
</style>