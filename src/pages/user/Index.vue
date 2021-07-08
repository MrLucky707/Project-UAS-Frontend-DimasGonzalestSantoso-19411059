<template>
  <q-page padding>
    <div class="row q-mb-md col-gutter-md">
      <div class="col-md-12 col-xs-12 col-lg-12">
        <div class="row">
          <div class="col-auto">
            <div class="left blue"></div>
          </div>
          <div class="col">
            <q-banner inline-actions class="text-blue-grey-14">
              <div class="text-h6">Data Diri Anda</div>
            </q-banner>
          </div>
        </div>
      </div>
    </div>
    <q-card flat>
      <q-table
        :rows="data"
        flat
        :columns="columns"
        row-key="name"
      >
        <template v-slot:body="props">
          <q-tr :props="props">
            <q-td key="username" :props="props">
              {{ props.row.username }}
            </q-td>
            <q-td key="namaLengkap" :props="props">
              {{ props.row.namaLengkap }}
            </q-td>
            <q-td key="prodi" :props="props">
              {{ props.row.prodi }}
            </q-td>
            <q-td key="noTelp" :props="props">
              {{ props.row.noTelp }}
            </q-td>
            <q-td key="email" :props="props">
              {{ props.row.email }}
            </q-td>
            <q-td key="aksi" :props="props">
              <div class="row q-gutter-md">
              <q-btn :to="{ name:'formEdit', params: { id: props.row._id }}" label="Edit" icon="edit" color="warning" unelevated/>
              </div>
            </q-td>
          </q-tr>
        </template>
      </q-table>
    </q-card>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      columns: [
        { name: 'username', align: 'left', label: 'Username', field: 'username', sortable: true },
        { name: 'namaLengkap', align: 'left', label: 'Nama Lengkap', field: 'namaLengkap', sortable: true },
        { name: 'prodi', align: 'left', label: 'Program Studi', field: 'prodi', sortable: true },
        { name: 'noTelp', align: 'left', label: 'Nomor Telepon', field: 'noTelp', sortable: true },
        { name: 'email', align: 'left', label: 'E-Mail', field: 'email', sortable: true },
        { name: 'aksi', align: 'left', label: 'Aksi', field: 'aksi' }
      ],
      data: []
    }
  },
  created () {
    this.getData()
  },
  methods: {
    getData () {
      this.$axios.get(`/user/getbyid/${this.$q.localStorage.getItem('dataMahasiswa')._id}`)
        .then(res => {
          if (res.data.sukses) {
            this.data = res.data.data
          } else {
            this.$showNotif(res.data.pesan, 'negative')
          }
        })
    }
  }
}
</script>
<style scoped>
.left{
  width: 5px;
  height: 100%;
  background-color:#f7a52c
}
</style>
