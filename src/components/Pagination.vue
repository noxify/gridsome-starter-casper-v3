<template>
  <ul class="flex pl-0 list-none rounded my-2">

    <li class="w-10 relative block text-center py-2 leading-tight bg-white border border-gray-300 text-black ml-0 mr-1 rounded hover:bg-gray-300" v-if="!isFirstPage(currentPage, totalPages)">
      <g-link :to="previousPage(currentPage,totalPages)" class="page-link" tabindex="-1" >&laquo;</g-link>
    </li>

    <li 
    v-for="page in pages" :key="page.name"
    v-bind:class="[isCurrentPage(currentPage, page.name) ? 'border-l-2 border-l-black' : '']"
    class="w-10 relative block py-2 text-center leading-tight bg-white border border-gray-300 text-black rounded hover:bg-gray-300 ml-1 mr-1">
      <g-link
          :to="page.link"
          class="page-link"
          :aria-label="page.name"
          :aria-current="page.name"
        >{{page.name}}</g-link>
    </li>

    <li class="w-10 relative block py-2 text-center leading-tight bg-white border border-gray-300 text-black ml-1 rounded hover:bg-gray-300" v-if="!isLastPage(currentPage, totalPages)">
      <g-link :to="nextPage(currentPage,totalPages)" class="page-link" tabindex="-1" >&raquo;</g-link>
    </li>
  </ul>

</template>

<script>
export default {
  props: {
    baseUrl: String,
    currentPage: Number,
    totalPages: Number,
    maxVisibleButtons: {
      type: Number,
      required: false,
      default: 3
    }
  },
  methods: {
    isFirstPage(currentPage, totalPages) {
        return currentPage == 1;
    },
    isLastPage(currentPage, totalPages) {
        return currentPage == totalPages;
    },
    isCurrentPage(currentPage, pageElement) {
        return currentPage == pageElement;
    },
    nextPage(currentPage, totalPages) {
      return `${this.baseUrl}/${currentPage + 1}`;
    },
    previousPage(currentPage, totalPages) {
      return currentPage === 2
        ? `${this.baseUrl}/`
        : `${this.baseUrl}/${currentPage - 1}`;
    }
  },
  computed: {
    startPage() {
      if (this.currentPage === 1) {
        return 1;
      }
      if (this.currentPage === this.totalPages) {
        return this.currentPage - 1;
      }
      return this.currentPage - 1;
    },
    pages() {
      const range = [];
      for (
        let i = this.startPage;
        i <=
        Math.min(this.startPage + this.maxVisibleButtons - 1, this.totalPages);
        i += 1
      ) {
        range.push({
          name: i,
          isDisabled: i === this.currentPage,
          link: i === 1 ? `${this.baseUrl}/` : `${this.baseUrl}/${i}`
        });
      }
      return range;
    }
  }
};
</script>