<template>
  <div class="Filter_Wrapper">
    <div class="well">
      <h2 class="text-center">{{$t('filter.cinema')}}</h2>
      <label class="control-label">{{$t('filter.search')}}</label>
      <input
        class="form-control"
        :placeholder="$t('filter.search')"
        v-model="search"
      >

      <hr>

      <label class="control-label">{{$t('filter.rooms')}}</label>
      <select v-model="rooms" class="form-control">
        <option v-for="room in ['',5,10,15,20,25,30]" :value="room">{{room}}</option>
      </select>

      <hr>

      <label class="control-label">{{$t('filter.seats')}}</label>
      <select v-model="seats" class="form-control">
        <option v-for="seat in ['',100,200,300,400,500,600]" :value="seat">{{seat}}</option>
      </select>

      <hr>
      <button @click="clearFilter" class="btn btn-warning btn-block">{{$t('filter.clear')}}</button>




    </div>
  </div>
</template>

<script>
  import {mapGetters, mapMutations} from 'vuex';
  import cinemaTypes from '../../types/cinema';
    export default {
      name: "cinema-filter",
      methods: {
        ...mapMutations({
          //llamamos a las funciones que estan en el modulo cinema
          setSearch: cinemaTypes.mutations.setSearch,
          setRooms: cinemaTypes.mutations.setRooms,
          setSeats: cinemaTypes.mutations.setSeats,
          clearFilter: cinemaTypes.mutations.clearFilter,
        })
      },
      computed: {
        ...mapGetters({
          //llamamos a las funciones que estan en el modulo cinema
          query: cinemaTypes.getters.search,
          numberOfRooms: cinemaTypes.getters.rooms,
          numberOfSeats: cinemaTypes.getters.seats
        }),
        search: {
          get(){
            return this.query;
          },
          set(value) {
            this.setSearch(value)
          }
        },
        rooms: {
          get(){
            return this.numberOfRooms;
          },
          set(value) {
            this.setRooms(value)
          }
        },
        seats: {
          get(){
            return this.numberOfSeats;
          },
          set(value) {
            this.setSeats(value)
          }
        },
      }
    }
</script>

<style lang="scss" scoped>
  .Filter_Wrapper {
    margin-top: 0!important;
  }
</style>
