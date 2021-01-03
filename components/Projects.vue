<template>
  <transition-group
    name="grid"
    class="flex flex-col md:grid grid-cols-3 gap-10 my-10 card-grid"
  >
    <div v-for="project in show" :key="project.id" class="card">
      <div class="card-content relative">
        <h1 class="text-xl">
          {{ project.title }}
        </h1>
        <p>{{ project.description }}</p>
        <hr>
        <div class="flex flex-row justify-between mt-3">
          <div class="flex flex-row justify-around text-sm opacity-75">
            {{ project.techs.join(', ') }}
          </div>
          <ul class="flex flex-row justify-around gap-3">
            <li v-if="project.github">
              <i class="fab fa-github fa-lg" />
            </li>
            <li v-if="project.link" class="hover:text-bglight duration-500">
              <a :href="project.link"><i class="fas fa-globe fa-lg" /></a>
            </li>
          </ul>
        </div>
      </div>
      <div class="card-image">
        <img :src="project.thumbnail" alt="">
      </div>
    </div>
  </transition-group>
</template>

<script>
export default {
  name: 'Projects',
  props: ['show']
}
</script>

<style scoped>
.card {
  @apply bg-bglight h-64 overflow-hidden relative;
  transition: translate .5s ease;
}

.card-content {
 @apply z-20 text-white bg-main absolute w-full bottom-0 px-3 py-1 h-8;
 transition: height 0.5s ease;
}

.card-content:hover {
  @apply overflow-auto;
  height: 100%;
}

.card-image {
  @apply absolute z-10;
}

.card-image img {
  @apply mx-auto w-full z-10;
}

.grid-enter-active,
.grid-leave-active {
  transition: opacity .5s ease;
}

.grid-enter,
.grid-leave-to {
  opacity: 0;
}

.grid-enter-to,
.grid-leave {
  opacity: 1;
}
</style>
