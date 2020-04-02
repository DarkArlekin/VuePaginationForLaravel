<template>
    <div id="app">
        <div v-if="showPagination" class="pagination">
            <nav aria-label="Page navigation">
                <ul class="pagination">
                    <li class="page-item">
                        <div class="page-link"
                             @click="changePage(1)">
                            В начало
                        </div>
                    </li>
                    <li class="page-item" v-for="(item, key) in pages">
                        <div class="page-link"
                             :class="{active: item === getCurrentPage}"
                             @click="changePage(item)">
                            {{ item }}
                        </div>
                    </li>
                    <li class="page-item">
                        <div class="page-link"
                             @click="changePage(getLastPage)">
                            В конец
                        </div>
                    </li>
                </ul>
            </nav>
        </div>
    </div>
</template>

<script>
  export default {
    name: 'vue-pagination',
    props: {
      links: Object,
      meta: Object,
      current_page: Number,
      last_page: Number,
      next_page_url: String,
      prev_page_url: String,
    },
    computed: {
      getNextPage() {
        if (this.next_page_url) return this.next_page_url;
        if (this.links && this.links.next) return this.links.next;

        return null;
      },
      getPrevPage() {
        if (this.prev_page_url) return this.prev_page_url;
        if (this.links && this.links.prev) return this.links.prev;

        return null;
      },
      getCurrentPage() {
        if (this.current_page) return this.current_page;
        if (this.meta && this.meta.current_page) return this.meta.current_page;

        return null;
      },
      getLastPage() {
        if (this.last_page) return this.last_page;
        if (this.meta && this.meta.last_page) return this.meta.last_page;

        return null;
      },
      showPagination() {
        return !!(this.getNextPage || this.getPrevPage);
      },
      pages() {
        let arrayPages = [];

        if (this.showPagination) {
          for (let i = 1; i <= this.getLastPage; i++) {
            arrayPages.push(i);
          }

          let startIndex = arrayPages.indexOf(this.getCurrentPage - 2);
          let endIndex = arrayPages.indexOf(this.getCurrentPage + 3);


          startIndex = (startIndex !== -1) ? startIndex : 0;
          endIndex = endIndex !== -1 ? endIndex : this.getLastPage;

          return arrayPages.slice(startIndex, endIndex);
        }

        return null;
      },
    },
    data() {
      return {
        pagination: null,
      }
    },
    methods: {
      changePage(page) {
        this.$emit('update', page);
      },
    },
  }
</script>

<style lang="scss">
    nav {
        display: block;

        .pagination {
            display: flex;
            padding-left: 0;
            list-style: none;
            border-radius: .25rem;

            .page-item {
                cursor: pointer;

                &:first-child {
                    .page-link {
                        margin-left: 0;
                        border-top-left-radius: .25rem;
                        border-bottom-left-radius: .25rem;
                    }
                }

                &:last-child {
                    .page-link {
                        border-top-right-radius: .25rem;
                        border-bottom-right-radius: .25rem;
                    }
                }

                .page-link {
                    &:hover {
                        z-index: 2;
                        color: #0056b3;
                        text-decoration: none;
                        background-color: #e9ecef;
                        border-color: #dee2e6;
                    }

                    position: relative;
                    display: block;
                    padding: .5rem .75rem;
                    margin-left: -1px;
                    line-height: 1.25;
                    color: #007bff;
                    background-color: #fff;
                    border: 1px solid #dee2e6;
                }
            }
        }
    }
</style>
