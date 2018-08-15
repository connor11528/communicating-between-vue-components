<template>
    <div>
        <h1>Map is here</h1>
        <div id="map" class="h-250"></div>
    </div>
</template>

<style scoped>
    #map {
        margin: 0 auto;
        background: gray;
    }
    .h-250 {
        height:250px;
    }
</style>
<script>
  import Vue from 'vue';

  export default {
    props: {
      'latitude': {
        type: Number,
        default() {
          return EventBus.sanfrancisco[0]
        }
      },
      'longitude': {
        type: Number,
        default() {
          return EventBus.sanfrancisco[1]
        }
      },
      'zoom': {
        type: Number,
        default() {
          return 14
        }
      },
    },
    mounted() {
      this.$markers = [];
      this.$map = new google.maps.Map(document.getElementById('map'), {
        center: new google.maps.LatLng(this.latitude, this.longitude),
        zoom: this.zoom
      });
      Vue.nextTick().then(()=>{
        this.clearMarkers();
      });
    },
    created(){
      EventBus.$on('clear-markers', ()=>{
        this.clearMarkers();
        this.$markers = [];
      });
      EventBus.$on('add-marker', (data)=>{
        let marker     = this.makeMarker(data.latitude, data.longitude);
        this.$markers.push(marker);
      });
    },
    data(){
        return {};
    },
    methods: {
      makeMarker(latitude, longitude) {
        return new google.maps.Marker({
          position: new google.maps.LatLng(latitude, longitude),
          icon: null,
          map: this.$map,
          title: null,
        });
      },
      clearMarkers(){
        for( let i = 0; i < this.$markers.length; i++ ){
          this.$markers[i].setMap(null);
        }
      }
    }
  }
</script>