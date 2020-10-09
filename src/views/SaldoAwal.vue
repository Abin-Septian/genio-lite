<template>
    <div>
        <base-header type="gradient-success" class="pb-6 pb-8 pt-5">
            <div class="row">
                <div class="col-xl-4 col-lg-6">
                    <stats-card title="Jumlah Saldo Awal"
                                type="gradient-green"
                                sub-title="350,897"
                                icon="ni ni-money-coins"
                                class="mb-4 mb-xl-0">
                    </stats-card>
                </div>
                <div class="col-xl-4 col-lg-6">
                    <stats-card title="Ekuitas"
                                type="gradient-info"
                                sub-title="350,897"
                                icon="ni ni-chart-pie-35"
                                class="mb-4 mb-xl-0">
                    </stats-card>
                </div>
                <div class="col-xl-4 col-lg-6">
                    <stats-card title="Saldo Kas"
                                type="gradient-primary"
                                sub-title="350,897"
                                icon="ni ni-chart-bar-32"
                                class="mb-4 mb-xl-0">
                    </stats-card>
                </div>
            </div>
        </base-header>

        <div class="container-fluid mt--7">
            <div class="row">
                <div class="col">
                    <projects-table title="Saldo Awal" :data="data.saldo_awal" :organisasi="data.organisasi" :user="data.user"></projects-table>
                </div>
            </div>
        </div>

    </div>
</template>

<script>
const axios = require('axios');
import ProjectsTable from './Tables/SaldoAwalTable'

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
        axios.get('https://localhost:8081/v1/saldo_awal?id_user=19', {
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