<template>
    <div>
        <h1>ListView</h1>
        <p>Marker count: {{ markers.length }}</p>
        <table class="table">
            <thead>
                <tr>
                    <th>Index</th>
                    <th>Latitude</th>
                    <th>Longitude</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="marker in markers">
                    <td>{{ marker.index }}</td>
                    <td>{{ marker.latitude }}</td>
                    <td>{{ marker.longitude }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<script>
    export default {
      created(){
        EventBus.$on('add-marker', (marker)=>{
          marker['index'] = this.index;
          this.index++;
          this.markers.push(marker);
        });
        EventBus.$on('clear-markers', ()=>{
          this.markers = [];
          this.index = 0;
        });
      },
      data(){
        return {
          index: 0,
          markers: []
        };
      }
    }
</script>