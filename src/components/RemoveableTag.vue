<template>
  <div class="c-btn">
    <div class="c-btn__text">{{ text }}</div>
    <div class="c-btn__delete" @click="removeFilter(text)">
      <img src="./../assets/icon-remove.svg" alt="" />
    </div>
  </div>
</template>

<script>
export default {
  props: ["text"],
  methods: {
    removeFilter(tag) {
      this.$emit("removeFilter", tag);
    },
  },
};
</script>

<style lang="scss" scoped>
.c-btn {
  background-color: hsl(180, 52%, 96%);
  color: hsl(180, 29%, 50%);
  font-weight: bolder;
  border-radius: 5px;
  margin: 8px;
  transition: all 0.2s;
  overflow: hidden;
  display: flex;
  @media only screen and (max-width: 850px) {
    font-size: 13px;
  }
}

.c-btn__text {
  padding: 7px;
}

.c-btn__delete {
  background-color: hsl(180, 29%, 50%);
  padding: 9px 9px 0 9px;
  cursor: pointer;
  &:hover {
    background-color: hsl(180, 14%, 20%);
  }
}
</style>
