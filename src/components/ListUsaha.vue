<template>
    <v-container>
        <v-card>
            <v-card-title class="headline">Daftar Perusahaan</v-card-title>
            <v-card-subtitle>List Perusahaan Tambang</v-card-subtitle>
            <v-data-table :headers="headers" :items="perusahaan" density="compact" item-key="name">
                <template v-slot:item.location="{ item }">
                    <v-btn v-model="item.location" :ripple="false" icon="mdi mdi-map"></v-btn>
                </template>
            </v-data-table>
        </v-card>
    </v-container>
</template>

<script setup>
import { ref } from 'vue'

const headers = [
    { title: 'Perusahaan', align: 'start', sortable: false, key: 'nama' },
    { title: 'Alamat', align: 'start', key: 'alamat' },
    { title: 'Bidang Usaha', align: 'start', key: 'bidang' },
    { title: 'ESG', align: 'end', key: 'esg' },
    { title: 'Lokasi', align: 'start', key: 'location' },
]

const perusahaan = [
    {
        'nama': 'Perusahaan 1',
        'alamat': 'Jalan Usaha, RT 001/RW 001 Kutai',
        'bidang': 'Pertambangan Minyak Bumi',
        'esg': '40.3',

    },
    {
        'nama': 'Perusahaan 2',
        'alamat': 'Jalan Usaha, RT 010/RW 001 Kutai Kartanegara',
        'bidang': 'Pertambangan Batu Bara',
        'esg': '60.3',

    },
    {
        'nama': 'Perusahaan 3',
        'alamat': 'Jalan Ikan, RT 001/RW 001 Mahakam',
        'bidang': 'Pertambangan Emas',
        'esg': '40.3',

    },{
        'nama': 'Perusahaan 4',
        'alamat': 'Jalan Usaha, RT 001/RW 001 Kutai',
        'bidang': 'Pertambangan Nikel',
        'esg': '30.3',

    },
    {
        'nama': 'Perusahaan 5',
        'alamat': 'Jalan Usaha, RT 001/RW 001 Kutai',
        'bidang': 'Pertambangan Batu Bara',
        'esg': '20.3',
    },
    {
        'nama': 'Perusahaan 6',
        'alamat': 'Jalan Usaha, RT 001/RW 001 Kutai',
        'bidang': 'Pertambangan Tembaga',
        'esg': '60.3',

    },
    {
        'nama': 'Perusahaan 7',
        'alamat': 'Jalan Usaha, RT 001/RW 001 Kutai',
        'bidang': 'Pertambangan Pasir',
        'esg': '50.3',

    },{
        'nama': 'Perusahaan 8',
        'alamat': 'Jalan Usaha, RT 001/RW 001 Kutai',
        'bidang': 'Pertambangan Minyak Bumi',
        'esg': '20.3',

    },{
        'nama': 'Perusahaan 9',
        'alamat': 'Jalan Usaha, RT 001/RW 001 Kutai',
        'bidang': 'Pertambangan Emas',
        'esg': '10.3',

    },
    {
        'nama': 'Perusahaan 10',
        'alamat': 'Jalan Usaha, RT 001/RW 001 Kutai',
        'bidang': 'Pertambangan Intan',
        'esg': '30.3',

    },{
        'nama': 'Perusahaan 11',
        'alamat': 'Jalan Usaha, RT 001/RW 001 Kutai',
        'bidang': 'Pertambangan Batu Alam',
        'esg': '20.3',

    }


]
</script>