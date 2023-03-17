<template>
  <div id="app">
    <h4 class="bg-success text-white text-center p-2">
      Lista zastrzyków użytkownika {{ name }}
    </h4>
    <div class="container-fluid p-4">
      <div class="row" v-if="filteredInjections.length == 0">
        <div class="col text-center">
          <b>Nie masz zastrzyków do zrobienia. Wspaniale!</b>
        </div>
      </div>
      <template v-else>
        <div class="row">
          <div class="col font-weight-bold">Zastrzyk</div>
          <div class="col-2 font-weight-bold">Wykonano?</div>
        </div>
        <div class="row" v-for="i in filteredInjections" v-bind:key="i.action">
          <div class="col">{{ i.action }}</div>
          <div class="col-2 text-center">
            <input type="checkbox" v-model="i.done" class="form-check-input" />
            <!-- {{ i.done }} -->
          </div>
        </div>
      </template>
      <div class="row py-2">
        <div class="col">
          <input v-model="newInjectionText" class="form-control" />
        </div>
        <div class="col-2">
          <button class="btn btn-primary" v-on:click="addNewInjection">Dodaj</button>
        </div>
      </div>
      <div class="row bg-secondary py-2 mt-2 text-white">
        <div class="col text-center">
          <input type="checkbox" v-model="hideCompleted" class="form-check-input" />
          <label class="form-check-label font-weight-bold">
            Ukryj wykonane zastrzyki
          </label>
        </div>
        <div class="col text-center">
          <button class="btn btn-sm btn-warning" v-on:click="deleteCompleted">
            Usuń wykonane
          </button>
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
        injections: [],
        hideCompleted: true,
        newInjectionText: "",
      }
    },
    computed: {
      filteredInjections() {
        return this.hideCompleted ?
          this.injections.filter(i => !i.done) : this.injections
      }
    },
    methods: {
      addNewInjection() {
        this.injections.push({
          action: this.newInjectionText,
          done: false
        });
        this.storeData();
        this.newInjectionText = "";
      },
      storeData() {
        localStorage.setItem("injections", JSON.stringify(this.injections));
      },
      deleteCompleted() {
        this.injections = this.injections.filter(i => !i.done);
        this.storeData();
      }
    },
    created() {
      let data = localStorage.getItem("injections");
      if (data != null) {
        this.injections = JSON.parse(data);
      }
    }
  }
</script>