<template>
  <GmapMap
      :center="center"
      :zoom="11.5"
      style="width: 1000px; height: 500px; margin: auto"
  >
    <GmapInfoWindow
        :options="infoWindowOptions"
        :position="infoWindowPosition"
        :opened="infoWindowOpened"
        @closeclick="handleInfoWindowClose"
    >
      <h2>{{ activeTour.title }}</h2>
      <p>{{ activeTour.address }}</p>
      <a :href="activeTour.link" target="_blank">{{ activeTour.link }}</a>
    </GmapInfoWindow>
    <GmapMarker
        :key="index"
        v-for="(m, index) in markers"
        :position="m.position"
        :title="m.title"
        :clickable="true"
        :draggable="false"
        @click="handleMarkerClicked(m)"
    ></GmapMarker>
  </GmapMap>
</template>
<script>
export default {
  name: 'GoogleMap',
  data () {
    return {
      center: {lat: -34.6, lng: -58.4},
      infoWindowOptions:{
        pixelOffset:{
          width: 0,
          height: -35
        }
      },
      activeTour:{

      },
      infoWindowOpened: false,
      markers: [{
        position: {lat: -34.583453, lng: -58.405544},
        title: "Patitas Al Rescate",
        address: "AV General Las Heras 3749, 1425 Palermo, Buenos Aires",
        link: "https://www.instagram.com/patitasalrescate/?hl=es-la"
      },
      {
      position: {lat: -34.584056, lng: -58.392806},
      title: "Colita Feliz",
      address: "Av. del Libertador 1473, Buenos Aires, Argentina",
      link: "https://www.instagram.com/_colitafeliz_/?hl=es"
      },
      {
        position: {lat: -34.616667, lng: -58.45},
        title: "Rescatando Huellitas",
        address: "Av. Jose Maria Moreno 1109, Buenos Aires, Argentina",
        link: "https://www.instagram.com/rescatando_huellitas_/?hl=es"
      },
      {
        position: {lat: -34.765191, lng: -58.377481},
        title: "Raza Callejera",
        address: "Bombero Ariño 802, Temperley, Provincia de Buenos Aires",
        link: "https://www.instagram.com/razacallejera/?hl=es"
      },
      {
        position: {lat: -34.4115221549301, lng: -58.66854054425489},
        title: "SOS Animal Tigre",
        address: "La Alameda Barrio Privado, Nordelta, Tigre",
        link: "https://www.instagram.com/sosanimaltigre/?hl=es"
      },
      {
        position: {lat: -34.56876763397825, lng: -58.4622145490992},
        title: "Salvando Patitas",
        address: "Cap. Gral. Ramón Freire 1882, CABA",
        link: "https://www.instagram.com/salvandoopatitas/?hl=es"
      },
      {
        position: {lat: -34.56917830711908, lng: -58.46112540695302},
        title: "Pichichos Al Rescate",
        address: "Delgado 1308, Colegiales, CABA",
        link: "https://www.instagram.com/pichichosalrescate/"
      },
      ]
    }
  },
  computed: {
    infoWindowPosition() {
      return {
        lat: parseFloat(this.activeTour.lat),
        lng: parseFloat(this.activeTour.lng)
      }
    },
  },
  methods: {
    handleMarkerClicked(m){
      this.activeTour = m;
      this.infoWindowOpened = true;
      this.center=m.position;
    },
    handleInfoWindowClose(){
      this.activeTour = {};
      this.infoWindowOpened = false;
    },
  }
}
</script>