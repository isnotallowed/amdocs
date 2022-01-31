<template>
  <div class="panel">
    <button
      class="panel__favorite"
      :class="{ 'panel__favorite-active': isFavorite }"
      @click.stop="$emit('toggleFavorite', { id: id, status: isFavorite })"
    >
      <StarIcon />
    </button>
    <span class="panel__category">{{ category }}</span>
    <p class="panel__title">{{ title }}</p>
    <p class="panel__intro">{{ intro }}</p>
    <ul class="panel__details">
      <li v-for="(detail, index) in details" :key="index" class="panel__detail">
        {{ detail }}
      </li>
    </ul>
  </div>
</template>

<script>
import StarIcon from '~/components/icons/StarIcon'
export default {
  name: 'PanelComponent',
  components: { StarIcon },
  props: {
    id: {
      type: Number,
      required: true,
    },
    title: {
      type: String,
      required: true,
    },
    intro: {
      type: String,
      required: true,
    },
    category: {
      type: String,
      required: true,
    },
    details: {
      type: Array,
      required: true,
    },
    isFavorite: {
      type: Boolean,
      default: false,
    },
  },
}
</script>

<style scoped lang="scss">
.panel {
  position: relative;
  padding: 1rem;
  border: 1px solid #eef2ff;
  border-radius: 1rem;
  cursor: pointer;
  transition: all 0.3s;
  &:hover {
    border-color: #3a7ee2;
  }
  &__title {
    margin-top: 1rem;
    font-style: normal;
    font-weight: bold;
    font-size: 1rem;
    line-height: 1.25rem;
    color: #3a7ee2;
  }
  &__category {
    margin-left: auto;
    background: #3a7ee2;
    color: white;
    font-size: 0.85rem;
    border-radius: 2rem;
    padding: 0.25rem 0.85rem;
  }
  &__intro {
    min-height: 2rem;
  }
  &__details {
    padding-left: 1rem;
  }
  &__detail {
    &::marker {
      color: #3a7ee2;
    }
    margin-bottom: 0.25rem;
    &:last-child {
      margin-bottom: 0;
    }
  }
  &__favorite {
    border: none;
    background: none;
    color: #3a7ee2;
    display: flex;
    align-items: center;
    justify-content: center;
    position: absolute;
    top: 0;
    right: 0;
    background: #eef2ff;
    border-radius: 100%;
    height: 1.5rem;
    width: 1.5rem;
    transform: translate(50%, -50%);
    cursor: pointer;
    &-active {
      color: #f2994a;
    }
  }
}
</style>
