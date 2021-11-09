<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="bg-teal-7">
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />
        <q-toolbar-title> CMUH AI CENTER </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>
    <q-drawer v-model="leftDrawerOpen" show-if-above bordered>
      <q-list>
        <q-item-label header> Essential Links </q-item-label>
        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>
    <!-- <q-page-container>
      <router-view />
    </q-page-container> -->
    <q-page-container>
      <div class="q-pa-md">
        <div class="q-gutter-y-md" style="width: 100%">
          <q-card>
            <q-tabs
              v-model="tab"
              dense
              class="text-grey"
              active-color="primary"
              indicator-color="primary"
              align="justify"
              narrow-indicator
            >
              <q-tab name="A1 A2 Montage" label="A1 A2 Montage" />
              <q-tab name="alarms" label="Double Banana" />
              <q-btn @click="toggle">點我</q-btn>
            </q-tabs>
            <q-separator />

            <q-tab-panels v-model="tab" animated keep-alive>
              <q-tab-pane name="A1 A2 Montage">
                <keep-alive >
                  <eeg></eeg>
                </keep-alive>
              </q-tab-pane>

              <q-tab-pane name="alarms">
                <keep-alive>
                  <div class="text-h6">Alarms</div>
                </keep-alive>
                Lorem ipsum dolor sit amet consectetur adipisicing elit.
              </q-tab-pane>
            </q-tab-panels>
          </q-card>
        </div>
      </div>
    </q-page-container>
  </q-layout>
</template>

<script lang="ts">
import EssentialLink from 'components/EssentialLink.vue';
import eeg from 'pages/eeg.vue';

const linksList = [
  {
    title: 'Docs',
    caption: 'quasar.dev',
    icon: 'school',
    link: 'https://quasar.dev',
  },
  {
    title: 'Github',
    caption: 'github.com/quasarframework',
    icon: 'code',
    link: 'https://github.com/quasarframework',
  },
  {
    title: 'Discord Chat Channel',
    caption: 'chat.quasar.dev',
    icon: 'chat',
    link: 'https://chat.quasar.dev',
  },
  {
    title: 'Forum',
    caption: 'forum.quasar.dev',
    icon: 'record_voice_over',
    link: 'https://forum.quasar.dev',
  },
  {
    title: 'Twitter',
    caption: '@quasarframework',
    icon: 'rss_feed',
    link: 'https://twitter.quasar.dev',
  },
  {
    title: 'Facebook',
    caption: '@QuasarFramework',
    icon: 'public',
    link: 'https://facebook.quasar.dev',
  },
  {
    title: 'Quasar Awesome',
    caption: 'Community Quasar projects',
    icon: 'favorite',
    link: 'https://awesome.quasar.dev',
  },
];

import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink,
    eeg,
  },

  setup() {
    const leftDrawerOpen = ref(false);
    let isShow = ref(true);
    function toggle() {
      isShow.value = !isShow.value;
    }

    return {
      tab: ref('A1 A2 Montage'),
      isShow,
      toggle,
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
});
</script>
