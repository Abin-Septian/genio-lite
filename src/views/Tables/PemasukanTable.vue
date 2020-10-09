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
          <button class="btn btn-primary btn-md align-content-center"><i class="ni ni-fat-add"></i><span>Pemasukan</span></button>
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
          <th>Tanggal</th>
          <th>Nomor Bukti</th>
          <th>Pelanggan</th>
          <th>Nominal</th>
          <th>Uraian</th>
          <th></th>
        </template>

        <template slot-scope="{row}">
          <td class="budget">
            {{row.tanggal}}
          </td>
          <td class="budget">
            {{row.nomor}}
          </td>
          <td class="budget">
            {{row.nama_pelanggan}}
          </td>
          <td class="budget">
            {{row.nominal}}
          </td>
          <td class="budget">
            {{row.uraian}}
          </td>

          <td class="text-right">
            <base-dropdown class="dropdown"
                           position="right">
              <a slot="title" class="btn btn-sm btn-icon-only text-light" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                <i class="fas fa-ellipsis-v"></i>
              </a>

              <template>
                <a class="dropdown-item" href="#">Cetak</a>
                <a class="dropdown-item" href="#">Edit Data</a>
                <a class="dropdown-item" href="#">Hapus Data</a>
              </template>
            </base-dropdown>
          </td>

        </template>

      </base-table>
    </div>

  </div>
</template>
<script>
  export default {
    name: 'projects-table',
    props: {
      type: {
        type: String
      },
      title: String,
      dataPemasukan: Array,
      organisasi: Object,
      user: Object,
      tipe: String,
    },
    data() {
      return {
        tableData: this.dataPemasukan,
      }
    }
  }
</script>
<style>
</style>
