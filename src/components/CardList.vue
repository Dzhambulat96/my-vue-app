<script setup>
import { inject } from 'vue'
import Card from './Card.vue'
defineProps({
  items: Array,
})

const emit = defineEmits(['addToFavorite'])

const addToFavorite = inject('addToFavorite')
const onClickFavorite = () => {
  const obj = {
    ...props,
    parentId: props.id,
  }
  addToFavorite(obj)
}
</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
      v-for="item in items"
      :key="item.id"
      :id="item.id"
      :price="item.price"
      :title="item.title"
      :image-url="item.imageUrl"
      :onClickFavorite="() => emit('addToFavorite', item)"
      :onClickAdd="() => emit('addToCart', item)"
      :isFavorite="item.isFavorite"
      :isAdded="item.isAdded"
    />
  </div>
</template>
