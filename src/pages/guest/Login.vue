<template>
 <q-layout class="bg-blue-grey-8" view="lHh Lpr Lff">
  <q-page-container>
    <q-page padding class="row items-center justify-center">
       <div>
         <div>
          <q-card flat class="text-blue-grey-14">
            <div>
              <div>
                <div>
                </div>
              </div>
              <div class="col-md-6">
                   <q-card-section>
                    <q-img src="~assets/LOGO-UBL.png"></q-img>
                    <div>Untuk Mahasiswa Yang Belum Memiliki Akun Silahkan Registrasi</div>
                   </q-card-section>
                   <q-form
                    @submit="login"
                   >
                    <q-card-section>
                        <q-input v-model="username" label="Username"/>
                        <q-input type="password" v-model="password" label="Password"/>
                   </q-card-section>
                   <q-card-section>
                     <q-btn class="full-width" type="submit" unelevated color="secondary" label="Login"/>
                     <q-btn class="full-width q-mt-md" :to="{ name:'registerPage' }" flat unelevated color="Primary" label="Registrasi"/>
                    </q-card-section>
               </q-form>
             </div>
           </div>
         </q-card>
       </div>
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
      password: null
    }
  },
  methods: {
    login () {
      this.$axios.post('user/login', {
        username: this.username,
        password: this.password
      }).then(res => {
        if (res.data.sukses) {
          this.$q.localStorage.set('dataMahasiswa', res.data.data)
          if (res.data.data.level === 1) {
            this.$router.push({ name: 'dataMahasiswa' })
          } else {
            this.$router.push({ name: 'homeUser' })
          }
        } else {
          this.$showNotif(res.data.pesan, 'negative')
        }
      })
    }
  }
}
</script>
