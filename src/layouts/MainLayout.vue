<template>
  <q-layout view="lHh Lpr lFf">
    <q-drawer
      v-model="leftDrawerOpen"
      elevated
      :width="280"
      :breakpoint="500"
      :content-class="$q.dark.isActive ? 'flex justify-between bg-primary' : 'flex justify-between'"
    >
      <q-list style="overflow-y: auto; -webkit-overflow-scrolling: touch;min-height: 100%" :class="$q.dark.isActive ? 'bg-dark' : 'bg-white'">
        <q-item-label
          header
          class="text-grey-8 q-pb-none"
          style="position: sticky; top: 0;z-index: 9;"
        >
          <div class="menu-img"></div>
          <div class="text-center text-bold text-secondary q-mt-md full-width text-h2">Wonder Rainbows</div>
        </q-item-label>
        <EssentialLink
          v-for="link in essentialLinks"
          :key="link.title"
          v-bind="link"
        />
        <!-- <q-item>
          <q-toggle
            :value="$q.dark.isActive"
            checked-icon="nights_stay"
            color="black"
            keep-color
            class="text-accent toggle-btn"
            unchecked-icon="wb_sunny"
            :label="$q.dark.isActive ? 'Dark Mode' : 'Light Mode'"
            @input="handlePallet()"
          />
        </q-item>
        <q-item>
          <q-btn
            outline
            class="full-width"
            :color="$q.dark.isActive ? 'white' : 'warning'"
            @click="$q.fullscreen.toggle()"
            :icon="$q.fullscreen.isActive ? 'fullscreen_exit' : 'fullscreen'"
            :label="$q.fullscreen.isActive ? 'Exit Fullscreen' : 'Go Fullscreen'"
          />
        </q-item> -->
      </q-list>
      <div class="full-width flex row justify-center position absolute-bottom" :class="$q.dark.isActive ? 'bg-dark' : 'bg-white'">
        <!-- DO NOT REMOVE THIS LINE -->
        <div style="border-top: 0.5px solid white" class="text-center text-h5 text-weight-thin">Made by - <a :class="$q.dark.isActive ? 'text-accent' : 'text-warning'" href="https://jonafrank13.github.io/">Jona Frank</a> - 2023</div>
        <!-- DO NOT REMOVE THIS LINE -->
      </div>
    </q-drawer>

    <q-page-container>
      <q-btn
        flat
        dense
        round
        icon="menu"
        color="secondary"
        aria-label="Menu"
        class="fixed-top-left animated infinite slow txt-shadow heartBeat"
        size="lg"
        style="z-index: 10;padding-left: inherit;"
        @click="handleMenuClick"
      />
      <transition
        name="transitions"
        enter-active-class="animated fadeInRight"
        leave-active-class="animated fadeOutLeft"
        mode="out-in"
      >
        <router-view />
      </transition>
    </q-page-container>
  </q-layout>
</template>

<script>
import EssentialLink from 'components/EssentialLink'

export default {
  name: 'MainLayout',
  data () {
    return {
      leftDrawerOpen: false,
      essentialLinks: [
        {
          title: 'Home',
          caption: 'Home Page',
          icon: 'home',
          link: '/'
        },
        {
          title: 'About',
          caption: 'Learn more about us',
          icon: 'mood',
          link: '/about'
        },
        {
          title: 'Gallery',
          caption: 'Checkout our work',
          icon: 'camera_enhance',
          link: '/gallery'
        },
        {
          title: 'Contact Details',
          caption: 'Our contact details',
          icon: 'contact_phone',
          link: '/contact'
        }
      ],
    }
  },
  components: {
    EssentialLink
  },
  methods: {
   handleMenuClick: function () {
      this.leftDrawerOpen = !this.leftDrawerOpen
    },
    handlePallet: function () {
      this.$q.dark.toggle()
      this.vibrate()
      localStorage.setItem('dark', this.$q.dark.isActive)
    },
  }
}
</script>
