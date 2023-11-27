<template>
  <q-layout view="hHh lpR fFf">

    <q-header elevated class="bg-cyan-8">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />

        <router-link style="text-decoration: none;color: white;" to="/">
          <q-toolbar-title class="text-weight-bold">
            Type Club
          </q-toolbar-title>
        </router-link>
      </q-toolbar>

    </q-header>

    <q-drawer class="bg-cyan-8 text-white" width="230" show-if-above v-model="leftDrawerOpen" side="left" bordered>

      <q-item to="/typetest" v-ripple clickable class="q-my-lg text-body1" :active="link === 'quiz'"
        @click="link = 'quiz'" active-class="my-menu-link">
        <q-item-section>
          Type test
        </q-item-section>
        <q-item-section>
          <q-icon name="quiz">
          </q-icon>
        </q-item-section>
      </q-item>

      <q-item v-ripple clickable class="q-my-lg text-body1">
        <q-item-section>
          Type course
        </q-item-section>
        <q-item-section>
          <q-icon name="class">
          </q-icon>
        </q-item-section>
      </q-item>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>

  </q-layout>
</template>

<script>
import { ref } from 'vue'

export default {
  setup() {
    const leftDrawerOpen = ref(false)

    return {
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value
      },
      link: ref('')
    }
  }
}
</script>
<style>
.my-menu-link {
  color: white;
  background: #5dec4aa2
}
</style>
