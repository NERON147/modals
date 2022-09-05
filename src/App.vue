<template>
  <div class="wrapper">


    <div class="wrapper-content">
      <section>
        <div class="container">
          <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Show First modal</button>

         <modal 
         title="First modal" 
         v-show="modalFirst"
         @close="modalFirst = !modalFirst">
         <div slot="body">
          <p>Text</p>
          <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Well done</button>
         </div>
         </modal>

         <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Show First modal</button>

         <modal 
         title="First modal" 
         v-show="modalFirst"
         @close="modalFirst = !modalFirst">
         <div slot="body">
          <p>Text</p>
          <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Well done</button>
         </div>
         </modal>
         
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import modal from '@/components/Modal.vue'

export default {
components: {
  modal
},
data () {
  return {
    modalFirst: false
  }
}
}
</script>

<style>

</style>