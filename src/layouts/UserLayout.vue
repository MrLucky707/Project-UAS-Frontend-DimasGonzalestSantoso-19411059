<template>
  <q-layout view="lHh Lpr lFf">
    <q-header class="bg-white text-blue-grey-14">
      <q-toolbar>
        <q-btn dense flat round @click="leftDrawerOpen = !leftDrawerOpen" icon="menu"/>
        <q-space></q-space>
        <q-btn flat round>
          <q-avatar>
            <img src="~assets/student.jpg">
          </q-avatar>
          <q-menu>
          <q-list style="min-width: 100px">
            <q-separator />
            <q-separator />
            <q-item clickable v-close-popup @click="logout">
              <q-item-section>Logout</q-item-section>
            </q-item>
          </q-list>
        </q-menu>
          </q-btn>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      class="bg-primary text-accent"
    >
    <q-scroll-area class="fit">
          <q-list>
          <q-item class="justify-center text-center q-mb-md q-mt-md">
            <div class="text-h6">
              <q-avatar size="100px">
                <img src="~assets/student.jpg">
              </q-avatar>
              <div>Halaman Mahasiswa</div>
            </div>
          </q-item>

          <q-item clickable active-class="active" v-ripple exact :to=" { name: 'homeUser' } ">
            <q-item-section avatar>
              <q-icon name="account_circle"/>
            </q-item-section>
            <q-item-section>
              <q-item-label>Profile Mahasiswa</q-item-label>
            </q-item-section>
          </q-item>
          <q-item clickable active-class="active" v-ripple exact>
            <q-item-section avatar>
            <q-icon name="receipt"/>
            </q-item-section>
            <q-item-section>
              <q-item-label>Info Tagihan</q-item-label>
            </q-item-section>
          </q-item>
        </q-list>
    </q-scroll-area>
    </q-drawer>

    <q-page-container class="bg-grey-2">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>

export default {
  name: 'MainLayout',
  data () {
    return {
      leftDrawerOpen: false
    }
  },
  methods: {
    logout () {
      this.$q.localStorage.remove()
      this.$router.push({ name: 'loginPage' })
    }
  }
}
</script>
<style scoped>
.active {
  color: #000;
  background-color: #f7a52c;
  padding-right: 20px;
}
</style>
