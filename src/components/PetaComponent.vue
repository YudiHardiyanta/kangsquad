<template>
    <v-container>
        <!-- V-Card untuk menampung peta -->
        <v-card>
            <v-card-title class="headline">Analisis Geospasial</v-card-title>
            <v-card-subtitle>Peta Interaktif untuk menganalisis perubahan countur tanah</v-card-subtitle>

            <!-- Tempat untuk peta -->
            <div id="map" style="height: 400px;">

            </div>
            <v-progress-linear v-if="loading" color="deep-purple-accent-4" height="6" indeterminate
                rounded></v-progress-linear>
            <v-card-actions>
                <v-select clearable label="Tahun Peta" v-model="tahun_peta" :items=list_tahun_peta
                    variant="outlined"></v-select>
            </v-card-actions>
        </v-card>

    </v-container>
</template>

<script setup>
//

import { onMounted, ref, watch } from 'vue';
import L, { LatLng } from 'leaflet'; // Mengimpor Leaflet
import 'leaflet/dist/leaflet.css'; // Mengimpor CSS Leaflet


const dialog = ref(false)
const tahun_peta = ref('2025')
const list_tahun_peta = ref(['2025', '2024', '2023', '2022', '2021', '2020'])
const loading = ref(false)

const id_sentinel = ref('WS_bfded7dd-03cb-41c5-89fd-3cdb7363ce0b')

const titik_tambang = ref([
    { 'name': 'Perusahaan 1', 'lat': '-0.5481493300137943', 'long': '117.16432743010434' }, //KTC Coal Mining & Energy
    { 'name': 'Perusahaan 2', 'lat': '-0.5596930181225697', 'long': '117.0123133483281' }, //Mine Office PT. ABPEnergy.
    { 'name': 'Perusahaan 3', 'lat': '-0.45807350571763233', 'long': '117.15444896922294' },//Batu bara coal
    { 'name': 'Perusahaan 4', 'lat': '-0.44215622038265573', 'long': '117.09120112247776' },//Trade Batu Bara
    { 'name': 'Perusahaan 5', 'lat': '-0.43884195946781196', 'long': '117.07793174067075' },//PT. Mitra Abadi Mahakam site BBE office
    { 'name': 'Perusahaan 6', 'lat': '-0.4271381957394824', 'long': '117.08013873899733' },//PT BBE (Bukit Baiduri Energi)
])




const titik_posisi = ref([-0.4325622038265573, 117.14120112247776])

onMounted(() => {

    // Inisialisasi peta
    const map = L.map('map').setView(titik_posisi.value, 13); // Koordinat awal [lat, lng] dan zoom level

    // Menambahkan layer peta dari OpenStreetMap
    const osm = L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    });
    // Menambahkan layer peta satelit dari Esri World Imagery
    const esri = L.tileLayer('https://server.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer/tile/{z}/{y}/{x}', {
        attribution: '&copy; <a href="https://www.esri.com/">Esri</a> contributors'
    });

    /*
        const sentinel = L.tileLayer('https://services.sentinel-hub.com/ogc/wms/'+id_sentinel.value+'?SERVICE=WMS&VERSION=1.3.0&REQUEST=GetMap&LAYERS=NDVI&FORMAT=image/png&TILED=true&WIDTH=256&HEIGHT=256&CRS=EPSG:4326&BBOX={bbox}&TIME=2021-06-01/2021-06-30', {
            attribution: '&copy; <a href="https://www.sentinel-hub.com/">Sentinel Hub</a>',
            minZoom: 12,
            maxZoom: 19
        }).addTo(map);
        */

    esri.addTo(map)
    // Menambahkan marker di peta
    //L.marker([-0.48898650986250075, 117.15436396864372]).addTo(map)
    //    .bindPopup('Perusahaan Tambang')
    //    .openPopup();

    // Kontrol layer untuk memilih peta
    const baseLayers = {
        "Open Street Map": osm,
        "Esri": esri,
        //"Sentinel" : sentinel
    };

    L.control.layers(baseLayers).addTo(map);


    // Define the radar dot's radius
    const radius = 50;

    // Function to create a moving dot (like radar points)
    function createRadarDot(angle) {


    }

    // Set an interval for creating radar dots
    let angle = 0;

    // Mengatur radar
    const radar = [
        L.circleMarker(titik_posisi.value, { radius: 20, color: 'red', fillOpacity: 0.1 }).addTo(map),
        L.circleMarker(titik_posisi.value, { radius: 40, color: 'red', fillOpacity: 0.1 }).addTo(map),
        L.circleMarker(titik_posisi.value, { radius: 60, color: 'red', fillOpacity: 0.1 }).addTo(map),
        L.circleMarker(titik_posisi.value, { radius: 80, color: 'red', fillOpacity: 0.1 }).addTo(map),
        L.circleMarker(titik_posisi.value, { radius: 100, color: 'red', fillOpacity: 0.1 }).addTo(map),
    ]

    const titik = L.marker(titik_posisi.value, { draggable: true })
    titik.addTo(map)
        .bindPopup('Lokasi Saat Ini')
        .openPopup();

    titik.addEventListener('drag', (e) => {
        var pos = titik.getLatLng();
        titik_posisi.value = [pos.lat, pos.lng]
        radar[0].setLatLng([pos.lat, pos.lng])
        radar[1].setLatLng([pos.lat, pos.lng])
        radar[2].setLatLng([pos.lat, pos.lng])
        radar[3].setLatLng([pos.lat, pos.lng])
        radar[4].setLatLng([pos.lat, pos.lng])
    })

    setInterval(() => {
        //console.log(angle)
        radar[0].removeFrom(map);
        radar[1].removeFrom(map);
        radar[2].removeFrom(map);
        radar[3].removeFrom(map);
        radar[4].removeFrom(map);
        radar[angle % 5].addTo(map);
        angle += 1;
    }, 300);

    titik_tambang.value.forEach(element => {

        L.marker([element.lat, element.long]).addTo(map).bindPopup(element.name).openPopup();
    });
});

watch(tahun_peta, (newValue, oldValue) => {
    //perubahan tahun peta
    loading.value = !loading.value
    setTimeout(() => {
        loading.value = !loading.value
    }, 2000);
});

</script>

<style scoped>
/* Menyesuaikan ukuran peta */
#map {
    height: 100%;
    width: 100%;
}

</style>
