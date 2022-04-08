<template>
  <nav>
    <ul class="nav-links">
      <li @click="$emit('close')" v-for="page in pages">
        <nuxt-link class="nuxt-link-active" :to="`/${page.name}`">{{ page.name }}</nuxt-link>
      </li>
    </ul>
  </nav>
</template>

<script>
  export default {
    props: {
      is_open: {
        type: Boolean,
        default: false,
      },
      pages: {
        type: Array,
        required: true
      }
    }
  }
</script>

<style lang="css">

nav {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-content: center;
  justify-content: center;
}

nav .nav-links {
  position: relative;
  z-index: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
}

nav .nav-links li {
  position: relative;
  margin-bottom: 24px;
}

nav .nav-links li a {
  color: var(--primary-color);
  width: 100%;
  text-align: center;
  height: auto;
  margin-bottom: 5px;
  line-height: 1.5;
  font-size: 36px;
  display: block;
  text-transform: uppercase;
  text-decoration: none;
  transition: color 333ms ease-in-out;
}

nav .nav-links li a:before {
  content: "";
  display: block;
  height: 100%;
  width: 100%;
  position: absolute;
  transform-origin: right;
  transform: scaleX(0);
  background-color: var(--primary-color);
  /* padding: 20px; */
  transition: transform 333ms ease-in-out;
  z-index: -1;
}

nav .nav-links li a.nuxt-link-exact-active {
  color: #daa520;
}

nav .nav-links li a.nuxt-link-exact-active:before {
  transform: translate(0%, -50%);
}

@media all and (min-width: 1280px) {
  nav .nav-links li a:before {
    width: 120%;
    margin-left: -10%;
    align-content: center;
  }
}

nav .nav-links li a:hover::before {
  transform-origin: left;
  transform: scaleX(1);
}

nav .nav-links li a:hover {
  color: #ffffff;
}

</style>
