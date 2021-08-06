<template>
  <div>
    <ul class="pagination">
      <li class="pagination-item">
        <button 
          type="button" 
          @click="onClickPreviousPage"
          aria-label="Go to previous page"
          :disabled="isInFirstPage"
          class="previous"
        >
          Previous
        </button>
      </li>

      <li class="pagination-item">
        <p class="txt">Page {{currentPage}} of {{totalPages}}</p>
      </li>

      <li class="pagination-item">
        <button 
          type="button" 
          @click="onClickNextPage"
          aria-label="Go to next page"
          :disabled="isInLastPage"
          class="next"
        >
          Next
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'Pagination',
    props: ['currentPage', 'totalPages'],
    computed: {
      isInFirstPage() {
        return this.currentPage === 1;
      },
      isInLastPage() {
        return this.currentPage === this.totalPages;
      }
    },
    methods: {
      onClickPreviousPage() {
        if(this.currentPage !== 1) {
          this.$emit('pagechanged', this.currentPage - 1);
        }
      },
      onClickPage(page) {
        this.$emit('pagechanged', page);
      },
      onClickNextPage() {
        if(this.currentPage !== this.totalPages) {
            this.$emit('pagechanged', this.currentPage + 1);
        }
      },
      isPageActive(page) {
        return this.currentPage === page;
      },
    }
  }
  
</script>

<style scoped>
    .pagination {
      list-style-type: none;
      margin: 10px;
    }

    .pagination-item {
      display: inline-block;
    }

    button {
      text-decoration: none;
      padding: 5px 10px;
      margin: 3px;
      float: right;
    }

    button:hover {
      background-color: #ddd;
      color: black;
    }

    .txt {
      position: relative;
      bottom: 11px;
    }
</style>
