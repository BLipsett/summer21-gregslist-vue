<template>
  <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">
            List yo car
          </h5>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <form @submit.prevent="addCar">
            <div class="mb-3">
              <label for="make" class="form-label"></label>
              <input type="text" class="form-control" id="make" placeholder="Make" v-model="state.carInfo.make">
            </div>
            <div class="mb-3">
              <label for="model" class="form-label"></label>
              <input type="text" class="form-control" id="model" placeholder="Model" v-model="state.carInfo.model">
            </div>
            <div class="mb-3">
              <label for="year" class="form-label"></label>
              <input type="number" class="form-control" id="year" placeholder="Year" v-model="state.carInfo.year">
            </div>
            <div class="mb-3">
              <label for="price" class="form-label"></label>
              <input type="number" class="form-control" id="price" placeholder="Price" v-model="state.carInfo.price">
            </div>
            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">
              Close
            </button>
            <button type="submit" class="btn btn-primary">
              Add Car
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive } from '@vue/reactivity'
import { carsService } from '../services/CarsService'
import Notification from '../utils/Notification'
import $ from 'jquery'
export default {
  setup() {
    const state = reactive({
      carInfo: {}
    })
    return {
      state,
      async addCar() {
        try {
          await carsService.addCar(state.carInfo)
          $('#exampleModal').modal('toggle')
        } catch (error) {
          Notification.toast(error)
        }
      }
    }
  }

}
</script>

<style>

</style>
