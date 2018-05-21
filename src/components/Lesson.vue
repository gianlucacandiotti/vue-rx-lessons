<template>
  <div class="lesson">
    <h2 class="title">
      {{title}}
    </h2>

    <div>
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    title: String,
  },
};
</script>

<style lang="scss" scoped>
.lesson {
  align-items: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 100%;
  padding: 20px 0;

  &:not(:last-child) {
    border-bottom: 1px solid;
  }
}

.title {
  font-size: 18px;
}
</style>
