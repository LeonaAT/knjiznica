
<template>
  <q-layout view="lHh Lpr lFf">

    <q-header class="library-header">
      <q-toolbar class="q-px-lg">

        <q-btn
          flat
          round
          dense
          icon="menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />

        <q-toolbar-title class="text-weight-bold">
          <q-icon name="local_library" size="28px" class="q-mr-sm" />
          Gradska knjižnica
        </q-toolbar-title>

        <div class="text-subtitle2 gt-xs">
          Svijet znanja i mašte
        </div>

      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      :width="260"
      class="library-drawer"
    >
      <div class="drawer-heading q-pa-lg">
        <q-icon name="menu_book" size="55px" />
        <div class="text-h6 text-weight-bold q-mt-sm">
          Gradska knjižnica
        </div>
        <div class="text-caption">
          Vaše mjesto za nove priče
        </div>
      </div>

      <q-list padding>
        <q-item
          v-for="item in linkedList"
          :key="item.link"
          clickable
          v-ripple
          :to="item.link"
          exact
          active-class="active-link"
        >
          <q-item-section avatar>
            <q-icon :name="item.icon" />
          </q-item-section>

          <q-item-section>
            <q-item-label>{{ item.title }}</q-item-label>
            <q-item-label caption>
              {{ item.caption }}
            </q-item-label>
          </q-item-section>
        </q-item>
      </q-list>

      <div class="drawer-footer q-pa-md">
        <q-icon name="favorite" color="green-8" />
        <span class="q-ml-sm">Čitaj. Istražuj. Otkrij.</span>
      </div>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>

  </q-layout>
</template>

<script setup>
import { ref } from 'vue'

const leftDrawerOpen = ref(false)

const linkedList = [
  {
    title: 'Naslovnica',
    caption: 'Početna stranica',
    icon: 'home',
    link: '/'
  },
  {
    title: 'Popis knjiga',
    caption: 'Sve knjige',
    icon: 'menu_book',
    link: '/popis_knjiga'
  },
  {
    title: 'Pretraživanje',
    caption: 'Pronađi knjigu',
    icon: 'search',
    link: '/pretrazivanje'
  },
  {
    title: 'O nama',
    caption: 'Informacije o knjižnici',
    icon: 'info',
    link: '/o_nama'
  },
  {
    title: 'Lokacija',
    caption: 'Gdje se nalazimo',
    icon: 'location_on',
    link: '/lokacija'
  },
  {
    title: 'Login',
    caption: 'Prijava korisnika',
    icon: 'login',
    link: '/login'
  },
  {
    title: 'Registracija',
    caption: 'Novi korisnik',
    icon: 'person_add',
    link: '/registracija'
  }
]
</script>

<style scoped>
.library-header {
  background: #254b3b;
  color: white;
}

.library-drawer {
  background: #f7f5ef;
  color: #254b3b;
}

.drawer-heading {
  background: #e8eee8;
  color: #254b3b;
  text-align: center;
}

.active-link {
  background: #dce9df;
  color: #254b3b;
  font-weight: bold;
  border-radius: 10px;
  margin: 4px 8px;
}

.drawer-footer {
  color: #52685c;
  font-size: 13px;
  position: absolute;
  bottom: 0;
}
</style>
