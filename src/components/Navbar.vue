<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
      <a class="navbar-brand" href="#">Challenge</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent"
              aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="#">Home</a>
          </li>
        </ul>
        <form class="d-flex" @submit.prevent="onSubmit" v-if="!isLogin">
          <input class="form-control me-2" type="text" placeholder="User" aria-label="user" name="user">
          <input class="form-control me-2" type="password" placeholder="Password" aria-label="password" name="password">
          <button class="btn btn-outline-success" type="submit">Submit</button>
        </form>
        <form class="d-flex" @submit.prevent="logout" v-if="isLogin">
          <button class="btn btn-outline-success" type="submit">Logout</button>
        </form>
      </div>
    </div>
  </nav>
</template>

<script lang="ts">
import {Vue} from "vue-class-component";
import {DataStorage} from '../data.interface'

const storage = window.localStorage;
export default class Register extends Vue {
  name = "Navbar"
  isLogin = false;
  myData: any | DataStorage ;

  onSubmit(event: any): void {
    const user = event.target['user'].value
    const password = event.target['password'].value
    if (storage.getItem(user) == null) {
      storage.setItem(user, JSON.stringify({name: user, password, myEvents: []}))
      alert("User:" + user + " registered")
    } else {
      const data: DataStorage = JSON.parse(storage.getItem(user) as string)
      if (data.password == password) {
        this.isLogin = true;
        this.myData = data
        console.log(this.myData)
        this.$emit("myData",this.myData)
      } else {
        alert("The username or password is wrong")
      }
    }


  }

  logout(): void {
    this.isLogin = false;
  }

}


</script>

<style scoped>

</style>
