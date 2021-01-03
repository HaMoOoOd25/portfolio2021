<template>
  <div>
    <Nuxt />
  </div>
</template>

<style>
* {
  font-family: 'Roboto';
}

body {
  @apply bg-bgdark
}

/* width */
::-webkit-scrollbar {
  width: 2px;
}

/* Track */
::-webkit-scrollbar-track {
  background: transparent;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: #6C63FF;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: #6C63FF;
}
</style>
