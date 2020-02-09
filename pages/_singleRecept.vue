<template>
  <div id="recept-page" class="page-wrapper recept-page">
    <site-hero :title="title" :subtitle="subtitle" :image="featureImage">
      <span
        v-if="author && $siteConfig.receptek.displayAuthor"
        class="author-wrapper"
      >
        <strong>Author:</strong> {{ author }}
      </span>
      <span v-if="date" class="date-wrapper">
        <strong>Published on:</strong> {{ date }}
      </span>
    </site-hero>
    <main-section :one-column-constrained="true">
      <template v-slot:default>
        <div class="recept-wrapper">
          <markdown :markdown="$store.state.content" />
          <div class="other-receptek">
            <h6 class="subtitle is-size-4">
              Related Recepts
            </h6>
            <!-- Related Recepts -->
            <receptek-grid :number="3" :category="category" :exclude="slug" />
          </div>
          <disqus-comments :identifier="$route.params.singleRecept" />
        </div>
      </template>
      <template v-slot:sidebar>
        <recept-sidebar />
      </template>
    </main-section>
  </div>
</template>
<script>
import { mapState } from 'vuex'
import { setPageData, getFormattedDate } from '../helper'
// import 'highlight.js/styles/github.css'
import Markdown from '~/components/Markdown'
import ReceptSidebar from '~/components/ReceptSidebar'
export default {
  components: {
    Markdown,
    ReceptSidebar
  },
  computed: {
    ...mapState([
      'title',
      'subtitle',
      'featureImage',
      'underSubtitle',
      'author',
      'category',
      'slug'
    ]),
    date() {
      return getFormattedDate(this.$store.state.date)
    }
    url() {
      return `${process.env.URL}/${this.$route.fullPath}`
    }
  },
  fetch({ store, params }) {
    setPageData(store, { resource: 'recept', slug: params.singleRecept })
  }
}
</script>
<style scoped lang="scss">
.edit-recept {
  margin-bottom: 20px;
}
</style>
