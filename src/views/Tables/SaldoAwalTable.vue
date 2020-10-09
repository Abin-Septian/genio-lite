<template>
  <div class="card shadow"
       :class="type === 'dark' ? 'bg-default': ''">
    <div class="card-header border-0"
         :class="type === 'dark' ? 'bg-transparent': ''">
      <div class="row align-items-center">
        <div class="col">
          <h3 class="mb-0" :class="type === 'dark' ? 'text-white': ''">
            {{title}}
          </h3>
        </div>
        <div class="col text-right">
          <button class="btn btn-primary btn-md " v-on:click="simpanData">Simpan Data</button>
        </div>
      </div>
    </div>

    <div class="table-responsive">
      <base-table class="table align-items-center table-flush"
                  :class="type === 'dark' ? 'table-dark': ''"
                  :thead-classes="type === 'dark' ? 'thead-dark': 'thead-light'"
                  tbody-classes="list"
                  :data="tableData">
        <template slot="columns">
          <th>Kode Akun</th>
          <th>Nama Akun</th>
          <th>Nominal</th>
        </template>

        <template slot-scope="{row}">
          <td class="budget">
            {{row.kode_akun}}
          </td>
          <td class="budget">
            {{row.nama_akun}}
          </td>
          <td class="budget">
            <input type="text" name="" id="" v-model="row.nominal" class="form-control text-right">
          </td>

        </template>

      </base-table>
    </div>

  </div>
</template>
<script>
const axios = require('axios');

export default {
  name: 'projects-table',
  props: {
    type: {
      type: String
    },
    title: String,
    data: Array,
    organisasi: Object,
    user: Object,
  },
  data() {
    return {
      tableData: this.data,
    }
  },
  methods:{
    simpanData: function() {
      const data =  {
            user : this.user,
            organisasi : this.organisasi,
            saldo_awal : this.tableData,
          }

      axios.post('https://localhost:8081/v1/saldo_awal', data, {
          headers : {
              'X-API-KEY' : 'eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhdXRoRGF0ZUNyZWF0ZWQiOiIxMS0wOS0yMDIwIDEwOjMyOjQyIiwiYXV0aFNlcnZpY2VLZXkiOiJjNDNlOWQ2Njk1ZWRmNjYwZmIyNTgzZmMzMDE4OTg1NyIsImF1dGhDbGllbnRBUElLZXkiOiJzNWltODkwNzE2OHQyMDVrOTFkMjMxcmEzOTZhZXN0MnR0ODRjcDAwc2VvIiwiYXV0aENsaWVudElQIjoiMTgyLjIuNzIuMjEiLCJhdXRoRXhwaXJlc0luIjoxNjAyMzg3MTYyLCJhdXRoVW5pcUtleSI6IjAuMTIwMTg5MDAgMTU5OTc5NTE2MiIsImF1dGhEQktleSI6InN5bmNvcmVpX2dlbmlvX2JpIiwiYXV0aE9yZ0tleSI6IiIsImF1dGhEZXB0S2V5IjoiIn0.-aFdNTrzDbPesDbJqf6b2thJ_QTv1N2w7CNgZKksrOM',
              'Content-Type' : 'application/json'
          },
          
      })
          .then(response => (this.data = response.data.responseData), alert('Data berhasil disimpan.'))
          .catch(err => {
              console.error(err);
          });
    }
  }
}
</script>
<style>
</style>
