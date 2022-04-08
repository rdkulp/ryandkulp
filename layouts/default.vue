<template>
  <div id="wrapper">
    <div class="half-content">
      <nuxt-link to="/"><div class="site-title">Ry Kulp</div></nuxt-link>
      <Nuxt />
    </div>
    <div class="menu-button" :class="{ open: is_open }">
      <button @click="toggleOpen"></button>
      <p role="heading" aria-level="1" class="extra-small">{{ pageName }}</p>
    </div>

    <div class="half-nav">
      <Nav
        @close="toggleOpen"
        :pages="[
          { 'name': 'ABOUT'},
          { 'name': 'PROJECTS'},
          { 'name': 'BLOG'}
        ]"
      />
      <Footer />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      is_open: false,
      page_name: null
    }
  },
  mounted() {
    this.is_open = false;
    console.log(this.$route);
  },
  computed: {
    pageName() {
      return this.$route.name.includes('-') ? '' : this.$route.name;
    }
  },
  methods: {
    toggleOpen () {
      this.is_open = !this.is_open;
    }
  }
};
</script>

<style lang="css">

.half-content {
  height: 100vh;
  width: 50%;
}

#wrapper {
	 position: relative;
	 overflow-x: hidden;
	 width: 100%;
	 height: auto;
	 padding: 2em;
}

#wrapper .half-content a {
  text-decoration: none;
  link-style: none;
}

#wrapper .half-content a .site-title {
  color: var(--primary-color);
  margin-bottom: 32px;
  font-size: clamp(2.25rem, calc(1.81rem + 2.20vw), 3.38rem);
}

#wrapper .menu-button {
  position: fixed;
  top: 2%;
  right: 2%;
  width: 40px;
  height: 40px;
  z-index: 10;
}

#wrapper .menu-button.open ~ .half-nav {
  opacity: 1;
  pointer-events: all;
}

#wrapper .menu-button.open button:before {
  transform: translateY(0) rotate(405deg);
}

#wrapper .menu-button.open button:after {
	transform: translateY(0) rotate(-45deg);
}

#wrapper .menu-button button {
  border: none;
  width: 100%;
  height: 100%;
  padding: 0;
  margin: 0;
  background-color: transparent;
	 cursor: pointer;
}
#wrapper .menu-button button:before {
  content: '';
  display: block;
  width: 40px;
  height: 5px;
  border-radius: 2.5px;
  background-color: #daa520;
  transform: translateY(-5px);
  transition: transform 333ms ease-in-out;
}

#wrapper .menu-button button:after {
  content: '';
  display: block;
  width: 40px;
  height: 5px;
  border-radius: 2.5px;
  background-color: #daa520;
  transform: translateY(5px);
  transition: transform 333ms ease-in-out;
}

#wrapper .menu-button p.extra-small {
  color: #daa520;
  position: absolute;
  right: 0;
  text-transform: uppercase;
}

#wrapper .half-nav {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 100%;
  height: 100%;
  background-color: #000;
  transition: opacity 333ms ease-in-out;
  opacity: 0;
  pointer-events: none;
}

@media all and (min-width: 768px) {
	#wrapper {
    display: flex;
	}

	#wrapper .half-content {
    width: 50%;
    height: 100%;
    padding: 3%;
	}

	#wrapper .half-content .site-title {
    margin-bottom: 64px;
	}

	#wrapper .menu-button {
    display: none;
	}
  
	#wrapper .half-nav {
    position: fixed;
    transform: none;
    top: unset;
    left: unset;
    right: 0;
    width: 50%;
    background-color: transparent;
    opacity: 1;
    pointer-events: all;
	}
}
</style>
