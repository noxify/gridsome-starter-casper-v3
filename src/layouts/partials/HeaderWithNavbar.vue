<template>
  <header class="bg-black relative z-1000 bg-radial-t-gray-to-black" id="header">
    <nav class="flex items-center justify-between flex-wrap container mx-auto px-4 sm:px-0 py-4">
      <div class="block flex-grow flex items-center w-auto height-30px">
        <div class="text-sm flex-grow uppercase">
          <ul class="list-none flex justify-left text-gray-300 uppercase">
            <li
              :key="element.name"
              v-for="(element,index) in $static.metadata.navigation"
              class="hover:text-white"
              v-bind:class="{'mr-4' : index != Object.keys($static.metadata.navigation).length - 1}"
            >
              <a
                :href="element.link"
                v-if="element.external"
                target="_blank"
                rel="noopener noreferrer"
                class="animated-link"
              >{{ element.name }}</a>
              <g-link v-else :to="element.link" class="animated-link">{{element.name}}</g-link>
            </li>
          </ul>
        </div>
        
        <div class="inline-block text-gray-400">
          <ul class="list-none flex justify-center md:justify-end">
            <li class="mr-0 sm:mr-6">
              <theme-switcher v-on="$listeners" :theme="theme"/>
            </li>
            <li
              :key="element.name"
              v-for="(element,index) in $static.metadata.social"
              class="hover:text-white hidden sm:block"
              v-bind:class="{'mr-6' : index != Object.keys($static.metadata.social).length - 1}"
            >
              <span class="text-sm">
                <a :href="element.link" target="_blank" rel="noopener noreferrer">
                  <font-awesome :icon="['fab', element.icon]" />
                </a>
              </span>
            </li>
          </ul>
        </div>

      </div>
    </nav>

    <div class="logo pt-0 pb-16 md:pb-32 md:pt-16 container mx-auto text-center text-white">
      <h2 class="m-0">
        <span class="text-4xl">
          <font-awesome :icon="['fas', 'ghost']" class="mb-1 mr-3"></font-awesome>
        </span>
        <span class="text-5xl text-white">{{ $static.metadata.siteName }}</span>
      </h2>
      <div class="text-gray-400 font-thin text-xl">{{ $static.metadata.siteDescription }}</div>
    </div>
  </header>
</template>

<script>

import ThemeSwitcher from '~/components/ThemeSwitcher'

export default {
  props: {
    theme: {
      type: String,
    },
  },
  components : {
    ThemeSwitcher
  }
};
</script>

<static-query>
query {
  metadata {
    siteName
    siteDescription
    navigation : headerNavigation {
      name
      link
      external
    }
    social {
      icon
      link
    }
  }
}
</static-query>