<template>
  <div>
    <!-- Quote Header -->
    <div
      class="header flex flex-col md:flex-row justify-around items-center bg-bglight p-4 mb-4"
    >
      <div class="md:w-1/3 mb-3">
        <h1 class="text-white text-4xl">
          It’s the possibility of having a dream come true that makes life
          interesting
        </h1>
      </div>
      <img class="w-3/4 md:w-1/4" src="/assets/img/dream.svg" alt="dream">
    </div>

    <!-- Who am I + Discord -->
    <div class="w-11/12 mx-auto">
      <div class="flex flex-row justify-around items-center">
        <img class="w-1/4 hidden md:block" src="/assets/img/webdev.svg" alt="">
        <div class="flex flex-col">
          <h2 class="text-white text-center text-2xl">
            Hello! I am Mohammed Balfaqih, a full-stack web developer
          </h2>
          <div class="bg-main md:w-1/3 mx-auto p-1 text-white text-center mb-2">
            <i class="fab fa-discord fa-lg" />
            HaMoOoOd25#7712
          </div>
          <button
            class="bg-main md:w-1/3 mx-auto p-1 text-white text-center hover:bg-bglight duration-500"
            @click="contactModal"
          >
            <i class="fas fa-envelope fa-lg" />
            Contact Form
          </button>
        </div>
      </div>

      <!-- Projects -->
      <div class="mt-32" data-aos="fade-up" data-aos-duration="500">
        <h2 class="text-3xl text-main">
          Projects
        </h2>

        <!-- Category Selector -->
        <Selector :selected="selected" @select="select" />

        <!-- Cards -->
        <Projects :show="show" />

        <!-- Empty :/-->
        <transition name="empty">
          <div v-if="!show.length > 0" class="p-10">
            <img class="h-48 mx-auto" src="/assets/img/empty.svg" alt="">
            <h1 class="text-white text-2xl text-center">
              Dang, it's empty. Maybe I should work on more projects.
            </h1>
          </div>
        </transition>
      </div>
    </div>
  </div>
</template>

<script>
import Selector from '~/components/Selector.vue'
import Projects from '~/components/Projects.vue'
import contactModal from '~/components/Modals/Contact'

export default {
  components: { Selector, Projects },
  data () {
    return {
      selected: [],
      projects: [
        {
          id: 1,
          title: 'GameDev Qatar Website',
          description: 'Gamedev Qatar is a game development community based in Qatar.',
          thumbnail: '/assets/img/gdq_final.png',
          link: 'https://gamedevqatar.com',
          techs: ['MongoDb', 'NuxtJs', 'VueJs', 'NodeJs', 'ExpressJs']
        },
        {
          id: 2,
          title: 'GDQ dashboard',
          description: 'This dashboard is made for GDQ website. It is used to manage events, testimonials, and partners. The dashboard is also linked to google forms to accept or decline people who wants to become a member.',
          thumbnail: '/assets/img/gdq_final_white.png',
          link: 'https://dashboard.gamedevqatar.com',
          techs: ['MongoDb', 'VueJs', 'NuxtJs', 'ExpressJs', 'NodeJs']
        },
        {
          id: 3,
          title: 'Coremenus',
          description: 'Coremenus is an upcoming menu software for Qatar. It comes with 2 main websites, the menu website which is responsible for showing a restaraunts data. The dashboard is for restaraunts managers to manage their products. It has a branded barcode creator, analytics for each company, file manager for managing images, push notifications for customers, sales and discount manager.',
          thumbnail: '/assets/img/coremenus.png',
          link: 'https://coremenus.com',
          techs: ['MongoDb', 'VueJs', 'NuxtJs', 'ExpressJs', 'NodeJs', 'NGINX', 'Vuetify', 'TailwindCss']
        }
      ],
      show: []
    }
  },
  created () {
    this.show = this.projects
  },
  methods: {
    select () {
      this.show = []
      setTimeout(() => {
        if (this.selected.length === 0) {
          this.show = this.projects
        } else {
          const toShow = []

          for (const i in this.projects) {
            for (const j in this.projects[i].techs) {
              if (this.selected.includes(this.projects[i].techs[j])) {
                toShow.push(this.projects[i])
              }
            }
          }
          this.show = toShow
        }
      }, 500)
    },
    contactModal () {
      this.$modal.show(
        contactModal,
        {},
        {
          height: 'auto',
          adaptive: true,
          scrollable: true
        }
      )
    }
  }
}
</script>

<style>
.header h1 {
  overflow-wrap: break-word;
}

.empty-enter-active {
  transition: opacity .5s ease;
}

.empty-enter,
.empty-leave-to {
  opacity: 0;
}

.empty-enter-to,
.empty-leave {
  opacity: 1;
}
</style>
