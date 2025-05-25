<template>
  <main>
    <v-container>
      <h1>Transaksi Perusahaan 1</h1>
      <v-row ga="2">
        <v-col md="6" lg="6">
          <v-card>
            <v-card-title class="headline">Akun Transaksi Terbanyak</v-card-title>
            <v-card-subtitle>Akun No : 8724731955</v-card-subtitle>
            <div id="line"></div>
          </v-card>
        </v-col>
        <v-col md="6" lg="6">
          <v-card>
            <v-card-title class="headline">Jumlah Transaksi Terbesar</v-card-title>
            <v-card-subtitle>UK pounds 123.456.213</v-card-subtitle>
            <div id="line"></div>
          </v-card>
        </v-col>
        <v-col md="6" lg="6">
          <v-card>
            <v-card-title class="headline">Mata Uang Digunakan Terbanyak</v-card-title>
            <v-card-subtitle>UK pounds</v-card-subtitle>
            <div id="line"></div>
          </v-card>
        </v-col>
        <v-col md="6" lg="6">
          <v-card>
            <v-card-title class="headline">Tujuan Transaksi Terbanyak</v-card-title>
            <v-card-subtitle>UK (United Kingdom)</v-card-subtitle>
            <div id="line"></div>
          </v-card>
        </v-col>
      </v-row>
      <v-row>
        <v-col md="12" lg="12">
          <canvas id="myChart"></canvas>
        </v-col>
      </v-row>
    </v-container>
    
    <ListTransaksi />
  </main>
</template>

<script setup>
//
import Chart from 'chart.js/auto';
import { ref, onMounted } from 'vue'

onMounted(() => {
  const ctx = document.getElementById('myChart');
  
  new Chart(ctx, {
    type: 'bar',
    data: {
      labels: ['2025','2024','2023','2022','2021'],
      datasets: [{
        label: 'Jumlah Transaksi Per Tahun',
        data: [12, 19, 3, 5, 2, 3],
        borderWidth: 1
      }]
    },
    options: {
      scales: {
        y: {
          beginAtZero: true
        }
      }
    }
  });
})

</script>
