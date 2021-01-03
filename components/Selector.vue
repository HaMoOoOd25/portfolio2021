<template>
  <ul class="grid grid-cols-4 md:grid-cols-8 lg:grid-cols-12 gap-3">
    <li v-for="option in options" :key="option" :class="{ 'selected': selected.includes(option) }" class="bg-white text-main px-2 py-1 font-bold text-sm rounded-xl text-center hover:bg-main hover:text-white duration-500" @click="Select(option)">
      {{ option }}
    </li>
  </ul>
</template>

<script>
export default {
  props: ['selected'],
  data () {
    return {
      options: [
        'VueJs',
        'NuxtJs',
        'DiscordJs',
        'NodeJs',
        'MongoDb'
      ]
    }
  },
  methods: {
    Select (option) {
      if (!this.selected.includes(option)) {
        this.selected.push(option)
        return this.$emit('select')
      }

      let i = 0
      this.selected.forEach((s) => {
        if (s === option) {
          this.selected.splice(i, 1)
        }
        i++
      })
      this.$emit('select')
    }
  }
}
</script>

<style scoped>
.selected {
    @apply bg-main text-white;
}

li {
    cursor: pointer;
}
</style>
