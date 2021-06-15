<template>
  <Navbar @myData="getData"/>
  <Events @addEvent="addEvent" events="myData.myEvents"/>
  <Alert/>
</template>

<script lang="ts">
import {Options, Vue} from 'vue-class-component';
import Register from './components/Register.vue';
import Navbar from './components/Navbar.vue'
import Alert from "./components/Alert.vue";
import Events from "./components/Events.vue"
import {DataStorage} from "@/data.interface";

const storage = window.localStorage;
@Options({
  components: {
    Register,
    Navbar,
    Alert,
    Events
  },
})

export default class App extends Vue {
  myData: DataStorage = { name: '', password: '', myEvents :[] }

  getData(data : DataStorage) {
    this.myData = data
  }
  addEvent(newEvent : any){
    if(this.myData.myEvents === undefined){
      this.myData.myEvents = []
    }
    this.myData.myEvents.push(newEvent as never)
    storage.setItem(this.myData.name, JSON.stringify(this.myData))
  }
}
</script>

<style>

</style>
