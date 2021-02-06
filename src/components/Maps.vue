<template lang="html">
<div>
  <button class="button" v-on:click.once="setupLeafletMap() ">Where is Studio Ghibli Museum?</button>

<div id='mapContainer'>
  <img src="../assets/tenor_down.gif" alt="tenor gif">
</div>
  
</div>
</template>

<script>
import "leaflet/dist/leaflet.css"
import L from "leaflet"

export default {
 name: "maps",
 
  data() {
   return{
     center: [35.696190656717114, 139.57042410468455],
    //  icon: [{
    //    iconUrl: '../assets/vector-mountains.jpeg',
    //    iconSize: [38,95],
    //    iconAnchor:   [22, 94],
    //    popupAnchor:  [-3, -76]
    //  }]
   }},
 methods: {
   setupLeafletMap: function () {
     
    const mapDiv = L.map("mapContainer").setView(this.center, 13);
    // const icon = L.marker()
    //       .setLatLng([35.696190656717114, 139.57042410468455])
    //       .addTo(mapDiv);
    
    const popup = L.marker([35.6, 139.5]).addTo(mapDiv);
      // .setLatLng([35.696190656717114, 139.57042410468455])
      // .setContent("Studio Ghibli Museum - Tokyo")
      // .openOn(mapDiv);
    L.tileLayer(
       "https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}",
       {
         attribution:
           'Map data (c) <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery (c) <a href="https://www.mapbox.com/">Mapbox</a>',
         maxZoom: 18,
         
         id: "mapbox/satellite-v9",
         accessToken: ''
       }
     ).addTo(mapDiv);
   },
 },
};
</script>

<style lang="css" scoped>
#mapContainer {
 height: 312px;
 width: 418px;
}
.button {
    background-color: rgb(24, 171, 233);
    border-radius:8px;
    cursor:pointer; 
    padding: 4%;
    font-family:fantasy;
    font-size: 1.5em;
}
.button:hover {
	background-color:#782323;
}
.button:active {
	position:relative;
	top:1px;
}
</style>
