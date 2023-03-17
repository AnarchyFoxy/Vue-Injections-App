<template>
  <div id="app">
    <h4 class="bg-success text-white text-center p-2">
      Lista zastrzyków użytkownika {{ name }}
    </h4>
    <div class="container-fluid p-4">
      <div class="row">
        <div class="col font-weight-bold">Zastrzyk</div>
        <div class="col-2 font-weight-bold">Zakończono?</div>
      </div>
      <div class="row" v-for="i in filteredInjections" v-bind:key="i.action">
        <div class="col">{{ i.action }}</div>
        <div class="col-2 text-center">
          <input type="checkbox" v-model="i.done" class="form-check-input" />
          {{ i.done }}
        </div>
      </div>
      <div class="row bg-secondary py-2 mt-2 text-white">
        <div class="col text-center">
          <input type="checkbox" v-model="hideCompleted" class="form-check-input" />
          <label class="form-check-label font-weight-bold">
            Ukryj zakończone zastrzyki
          </label>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
  export default
  {
    name: 'app',
    data() {
      return {
        name: "Astryda",
        injections: [
          { action: "Pierwszy zastrzyk - 14 marca", done: true },
          { action: "Drugi zastrzyk - 20 marca", done: false },
          { action: "Trzeci zastrzyk - 24 marca", done: false },
          { action: "Czwarty zastrzyk - 30 marca", done: false }
        ],
        hideCompleted: true
      }
    },
    computed: {
      filteredInjections() {
        return this.hideCompleted ?
          this.injections.filter(i => !i.done) : this.injections
      }
    }
  }
</script>