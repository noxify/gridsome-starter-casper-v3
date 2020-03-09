<template>
  <div class="fixed inset-0 h-16 bg-black">
    <nav 
    class="flex items-center justify-between flex-wrap container mx-auto px-4 sm:px-0 py-4 transition-all transition-500" 
    v-bind:class="{
      'opacity-100': !disableScroll && scrollPosition > headerHeight, 
      'opacity-0': !disableScroll && scrollPosition < headerHeight
    }">
      <div class="block flex-grow flex items-center w-auto">
        <div class="flex items-center flex-shrink-0 text-white mr-6">
          <font-awesome :icon="['fas', 'ghost']" class="mr-3"></font-awesome>
          <span class="font-semibold text-xl tracking-tight">{{ $static.metadata.siteName }}</span>
        </div>
        <div class="text-sm flex-grow uppercase">
          <ul 
          class="list-none flex justify-left text-gray-300 uppercase transition-all transition-500">
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
  </div>
</template>

<script>
/*
 * I'm a lazy guy, so i used this script
 * https://codepen.io/ninaregli/pen/OjeMLP
 * to calculate the current scroll position
 *
 * Will be used to add/remove the additional
 * css classes to show the sticky navbar
 */

import ThemeSwitcher from '~/components/ThemeSwitcher'

export default {
  components : {
    ThemeSwitcher
  },
  props: {
    disableScroll: {
      type: Boolean,
      default: false
    },
    theme: {
      type: String
    }
  },
  data: function() {
    return {
      scrollPosition: null,
      headerHeight: 0
    };
  },

  methods: {
    updateScroll() {
      this.scrollPosition = window.scrollY;
    },
    setHeaderHeight(height) {
      this.headerHeight = height;
    }
  },

  mounted() {
    if( !this.disableScroll ) {
      var height = document.getElementById("header").clientHeight;
      this.setHeaderHeight(height);
      window.addEventListener("scroll", this.updateScroll);
    }
  }
};
</script>

<static-query>
query {
  metadata {
    siteName
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
