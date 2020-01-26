<template>
  <div class="clearfix" :class="{ linkable }" @click="onclick">
    <div class="image"><img :src="book.image"></div>
    <div class="details">
      <ul>
        <li v-if="index">{{ index }}</li>
        <li>{{book.title}} ({{ book.price}}円)</li>
        <li>{{book.author}} 著</li>
        <li>{{book.publisher}} /刊</li>
        <li>{{book.published}} /発売</li>
      </ul>
    </div>
  </div>
</template>

<script>
import { mapAciton } from 'vuex'
import { UPDATE_CURRENT } from '@/mutation-types'

export default {
  name: 'book-info',
  props: {
    index: { type: Number },
    linkable: { type: Boolean, default: false },
    book: { type: Object },
  },
  methods: {
    ...mapAciton([UPDATE_CURRENT]), // UPDATE_CURRENTを同名メソッドに紐付ける
    onclick() {
      if (this.linkable) {
        this[UPDATE_CURRENT](this.book)
        this.$router.push('/form')
      }
    }
  }
}
</script>

<style scoped>
.linkable:hover {
  cursor: pointer;
  background-color: #ff9;
}
</style>