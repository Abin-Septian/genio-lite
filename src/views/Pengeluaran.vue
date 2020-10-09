<template>
    <div>
        <base-header type="gradient-success" class="pb-6 pb-8 pt-5">
            <h1 class="text-white">Pengeluaran</h1>
        </base-header>

        <div class="container-fluid mt--7">
            <div class="row">
                <div class="col">
                    <projects-table title="Daftar Pengeluaran" :dataPemasukan="data.pengeluaran" :organisasi="data.organisasi" :user="data.user" tipe="Customer"></projects-table>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
const axios = require('axios');
import ProjectsTable from './Tables/PengeluaranTable'

export default {
    components: {
      ProjectsTable
    },
    props:{
    },
    data () {
        return {
            data : null,
        }
    },
    created: function (){
        axios.get('https://localhost:8081/v1/pengeluaran?id_user=19', {
            headers : {
                'X-API-KEY' : 'eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhdXRoRGF0ZUNyZWF0ZWQiOiIxMS0wOS0yMDIwIDEwOjMyOjQyIiwiYXV0aFNlcnZpY2VLZXkiOiJjNDNlOWQ2Njk1ZWRmNjYwZmIyNTgzZmMzMDE4OTg1NyIsImF1dGhDbGllbnRBUElLZXkiOiJzNWltODkwNzE2OHQyMDVrOTFkMjMxcmEzOTZhZXN0MnR0ODRjcDAwc2VvIiwiYXV0aENsaWVudElQIjoiMTgyLjIuNzIuMjEiLCJhdXRoRXhwaXJlc0luIjoxNjAyMzg3MTYyLCJhdXRoVW5pcUtleSI6IjAuMTIwMTg5MDAgMTU5OTc5NTE2MiIsImF1dGhEQktleSI6InN5bmNvcmVpX2dlbmlvX2JpIiwiYXV0aE9yZ0tleSI6IiIsImF1dGhEZXB0S2V5IjoiIn0.-aFdNTrzDbPesDbJqf6b2thJ_QTv1N2w7CNgZKksrOM',
                'Content-Type' : 'application/json'
            }
        })
            .then(response => (this.data = response.data.responseData))
            .catch(err => {
                console.error(err);
            });
    },
}
</script>