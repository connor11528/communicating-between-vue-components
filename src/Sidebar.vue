<template>
    <div>
        <h1>Sidebar</h1>
        <input type="number" step="0.0001" class="form-control" v-model="latitude">
        <input type="number" step="0.0001" class="form-control" v-model="longitude">
        <button @click="addMarker" class="btn btn-danger">Add marker</button>
        <button @click="clearMarkers" class="btn btn-default">Clear markers</button>
    </div>
</template>
<script>

  export default {
    data(){
      return {
        latitude: EventBus.sanfrancisco[0],
        longitude: EventBus.sanfrancisco[1]
      };
    },
    methods: {
      addMarker(){
        EventBus.$emit('add-marker', {
          latitude: this.latitude,
          longitude: this.longitude
        });
      },
      clearMarkers(){
        EventBus.$emit('clear-markers');
      }
    }
  }
</script>