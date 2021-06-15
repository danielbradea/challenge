<template>
  <div class="container">
    <div class="row">
      <div class="col-5">
        <form @submit.prevent="onSubmit">
          <div class="form-group">
            <label for="inputName">Event name</label>
            <input type="text" class="form-control" id="inputName" aria-describedby="name"
                   placeholder="Enter event name" name="name">
          </div>
          <div class="form-group">
            <label for="inputDateStart">Start Date</label>
            <input type="datetime-local" class="form-control" id="inputDateStart" placeholder="Data" name="start">
          </div>
          <div class="form-group">
            <label for="inputDateEnd">End Date</label>
            <input type="datetime-local" class="form-control" id="inputDateEnd" placeholder="Data" name="end">
          </div>
          <div class="form-group form-check">
            <input type="checkbox" class="form-check-input" id="check" name="check">
            <label class="form-check-label" for="check">Recurrence</label>
          </div>
          <button type="submit" class="btn btn-primary">Submit</button>
        </form>
      </div>
      <div class="col" v-if="events > 0">
        <div class="list-group" v-for="(ev, index) in events" :key="index">
          <a href="#" class="list-group-item list-group-item-action flex-column align-items-start " >
            <div class="d-flex w-100 justify-content-between">
              <h5 class="mb-1">{{ ev.name }}</h5>
              <small></small>
            </div>
            <p class="mb-1"></p>
            <small></small>
          </a>
        </div>
      </div>
    </div>
  </div>

</template>

<script lang="ts">
import {Vue} from "vue-class-component";
import {Prop} from 'vue-property-decorator'

export default class Events extends Vue{
  @Prop()
  events!: []

  onSubmit(event : any): void{
    const nameEvent = event.target['name'].value
    const startDate = event.target['start'].value
    const endDate = event.target['end'].value
    const recurrent = event.target['check'].checked

    this.$emit("addEvent", {name: nameEvent, startDate, endDate, recurrent: recurrent})
  }
}
</script>

<style scoped>

</style>
