<script setup lang="ts">
// import { ref } from 'vue'
import { useHead } from '@vueuse/head'

// import packageJson from '../../package.json'
import { useDarkmode } from '/@src/stores/darkmode'

// type TabId = 'elements' | 'components' | 'forms' | 'plugins'
// const activeTab = ref<TabId>('elements')
const darkmode = useDarkmode()

useHead({
  title: 'Charter Boats – chartering boats all over the world',
})
</script>

<template>
  <MinimalLayout theme="light">
    <div class="landing-page-wrapper">
      <!-- Hero and Navbar -->
      <div id="vuero-landing" class="hero is-fullheight rounded-hero is-active">
        <!-- Navbar partial -->
        <LandingNavigation />

        <div class="absolute-header">
          <div class="header-inner">
            <img
              class="cut-circle light-image-l"
              src="/@src/assets/shapes/cut-circle.svg"
              alt=""
            />
            <img
              class="cut-circle dark-image-l"
              src="/@src/assets/shapes/cut-circle-dark.svg"
              alt=""
            />
          </div>
        </div>

        <div class="hero-body has-text-centered">
          <div class="container">
            <div class="switch-wrapper">
              <div class="night-toggle night-toggle--daynight">
                <input
                  id="night-toggle--daynight"
                  type="checkbox"
                  class="night-toggle--checkbox"
                  :checked="!darkmode.isDark"
                  aria-label="Toggle dark mode"
                  @change="darkmode.onChange"
                />
                <label
                  class="night-toggle--btn"
                  for="night-toggle--daynight"
                  tabindex="0"
                  @keydown.space.prevent="(e) => (e.target as HTMLLabelElement).click()"
                >
                  <span class="night-toggle--feature"></span>
                </label>
              </div>
            </div>
            <h1 class="title is-1 is-bold is-light is-bold">
              Charter <span>Boats</span>
            </h1>
            <h3 class="subtitle is-4 is-light">
              chartering boats all over the world
              <span class="tag is-primary is-rounded">beta</span>
            </h3>
          </div>
        </div>

        <canvas id="demo-canvas"></canvas>
      </div>

      <div class="container">
        <ViewListV2 />
      </div>

      <!-- Footer -->
      <LandingFooter />

      <!-- Back To Top Button -->
      <div id="backtotop">
        <a href="#" aria-label="back to top">
          <i aria-hidden="true" class="fas fa-angle-up"></i>
        </a>
      </div>
    </div>
  </MinimalLayout>
</template>

<style lang="scss">
@import '../scss/abstracts/mixins';
@import '../scss/_demo/landing';
</style>
