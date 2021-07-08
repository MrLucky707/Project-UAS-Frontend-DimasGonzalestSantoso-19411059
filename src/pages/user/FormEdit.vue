<template>
  <q-layout>
    <q-page-container>
        <q-page padding class="bg-blue-grey-5">
            <div class="row">
                <q-card class="fixed-center col-md-4 col-xs-12">
                    <q-card-section>
                        <div class="text-h6">
                            Silahkan Edit Data
                        </div>
                        <q-form
                            @submit="onSubmit"
                        >
                            <q-input
                                v-model="username"
                                label="Username"
                                :rules="[
                                val => val && val.length > 0 || 'Tolong Ketik Username'
                                ]"
                             />
                            <q-input
                                v-model="namaLengkap"
                                label="Nama Lengkap"
                                :rules="[
                                val => val && val.length > 0 || 'Tolong Ketik Nama Lengkap Anda'
                                ]"
                            />
                            <q-input
                                v-model="prodi"
                                label="Program Studi"
                                :rules="[
                                val => val && val.length > 0 || 'Tolong Ketik Program Studi Pilihan Anda'
                                ]"
                            />
                            <q-input
                                v-model="noTelp"
                                label="Nomor Telepon Aktif"
                                :rules="[
                                val => val && val.length > 0 || 'Tolong Masukan Nomor Telepon Anda'
                                ]"
                            />
                            <q-input
                                v-model="email"
                                label="Email"
                                :rules="[
                                val => val && val.length > 0 || 'Tolong Masukan Email Anda'
                                ]"
                            />
                            <q-input
                                v-model="password"
                                label="Password"
                                type="password"
                                :rules="[
                                val => val && val.length > 0 || 'Tolong Ketik Password Anda'
                                ]"
                            />
                            <div class="q-gutter-md">
                            <q-btn label="Submit" type="submit" color="secondary"/>
                            <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
                            </div>
                        </q-form>
                    </q-card-section>
                </q-card>
            </div>
        </q-page>
    </q-page-container>
  </q-layout>
</template>
<script>
export default {
  data () {
    return {
      username: null,
      namaLengkap: null,
      prodi: null,
      noTelp: null,
      email: null,
      password: null
    }
  },
  created () {
    this.getData()
  },
  methods: {
    getData () {
      this.$axios.get(`user/getbyid/${this.$route.params.id}`)
        .then(res => {
          if (res.data.sukses) {
            this.form = res.data.data
          } else {
            this.$router.push({ name: 'homeUser' })
          }
        })
    },
    onSubmit () {
      this.$axios.put(`user/edit/${this.$route.params.id}`, {
        username: this.username,
        namaLengkap: this.namaLengkap,
        prodi: this.prodi,
        noTelp: this.noTelp,
        email: this.email,
        password: this.password
      })
        .then(res => {
          if (res.data.sukses) {
            this.$showNotif(res.data.pesan, 'positive')
            this.$router.push({ name: 'homeUser' })
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
  background-color:rgb(208, 124, 108);
}
</style>
