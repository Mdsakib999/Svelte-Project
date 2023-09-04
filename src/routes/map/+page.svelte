<script>
  import Nav from "../../components/nav.svelte";
  import { onMount } from 'svelte';
  import Map from 'ol/Map';
  import View from 'ol/View';
  import TileLayer from 'ol/layer/Tile';
  import GeoJSON from 'ol/format/GeoJSON';
  import VectorLayer from 'ol/layer/Vector';
  import VectorSource from 'ol/source/Vector';
  import { Fill, Style } from 'ol/style';
  import XYZ from 'ol/source/XYZ'; // Add this import

  let map;

  // Function to load and style the GeoJSON layer
  function loadGeoJSON() {
    const geoJSONURL =
      'https://api.maptiler.com/maps/ocean/style.json?key=2cQDUAas6s87tttcg6tW';

    const vectorSource = new VectorSource({
      format: new GeoJSON(),
      url: geoJSONURL,
    });

    const vectorLayer = new VectorLayer({
      source: vectorSource,
      style: new Style({
        fill: new Fill({
          color: 'rgba(0, 106, 78, 0.75)', // #006a4e with 0.75 opacity
        }),
      }),
    });

    map.addLayer(vectorLayer);
  }

  onMount(() => {
    // Create and configure the map
    map = new Map({
      target: 'map',
      layers: [
        new TileLayer({
          source: new XYZ({
            url: 'https://api.maptiler.com/maps/basic/{z}/{x}/{y}.png?key=2cQDUAas6s87tttcg6tW',
          }),
        }),
      ],
      view: new View({
        center: [0, 0],
        zoom: 2,
      }),
    });

    // Load and style the GeoJSON layer
    loadGeoJSON();
  });


</script>

<Nav></Nav>
<h1>this is Map</h1>



<div id="map"></div>


<style>
    /* Define a CSS class to style the map container */
    #map {
        width: 100%;
        height: 100vh;
    }
</style>