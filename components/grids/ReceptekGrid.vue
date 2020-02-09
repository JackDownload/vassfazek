<template>
  <resource-grid
    v-bind="$props"
    :resource="$cms.recept"
    :theme="$siteConfig.recepts.theme || $siteConfig.cards.theme || null"
  >
    <template v-slot:default="{ item }">
      <recept-card
        :title="item.title"
        :link="`/${item.slug}`"
        :image="item.featureImage"
        :author="item.author"
        :date="item.date"
      />
    </template>
  </resource-grid>
</template>

<script>
import ReceptCard from '~/components/cards/ReceptCard'
export default {
  name: 'ReceptekGrid',
  components: { ReceptCard },
  props: {
    perRow: { type: Number, default: 3 },
    number: { type: Number, default: 0 },
    order: { type: String, default: 'DESC' },
    category: {
      type: Array,
      default() {
        return []
      }
    },
    exclude: { type: String, default: '' }
  }
}
</script>
