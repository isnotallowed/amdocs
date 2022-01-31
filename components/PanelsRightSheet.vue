<template>
  <div class="right-sheet">
    <button class="right-sheet__cross" @click="$emit('closeRightSheet')">
      <CrossIcon />
    </button>
    <div class="right-sheet__wrapper">
      <span class="right-sheet__category">{{ category }}</span>
      <p class="right-sheet__title">Title: {{ title }}</p>
      <p class="right-sheet__intro">Intro: {{ intro }}</p>
      <ul class="right-sheet__details">
        <li
          v-for="(detail, index) in details"
          :key="index"
          class="right-sheet__detail"
        >
          {{ detail }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import CrossIcon from '~/components/icons/CrossIcon'
export default {
  name: 'PanelsRightSheet',
  components: { CrossIcon },
  props: {
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
.right-sheet {
  height: 100vh;
  position: fixed;
  top: 0;
  right: 0;
  background: #ffffff;
  box-shadow: -4px 0px 28px rgba(0, 0, 0, 0.1);
  &__wrapper {
    padding: 2rem;
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
  &__cross {
    position: absolute;
    top: 1rem;
    right: 1rem;
    background: none;
    border: none;
    color: black;
    cursor: pointer;
    transition: all 0.3s;
    &:hover {
      color: #3a7ee2;
    }
  }
}
@media (max-width: 768px) {
  .right-sheet {
    width: 100%;
  }
}
@media (min-width: 768px) {
  .right-sheet {
    width: 400px;
  }
}
</style>
