<template>
  <div class="c-job-filter">
    <transition-group
      name="fade"
      tag="div"
      class="c-job-filter__container"
      appear
    >
      <div v-for="filter in filters" v-bind:key="filter">
        <RemoveableTag :text="filter" @removeFilter="removeFilter" />
      </div>
    </transition-group>
    <div class="c-job-filter__clear" @click="clearFilters">
      Clear
    </div>
  </div>
</template>

<script>
import RemoveableTag from "./RemoveableTag";
export default {
  components: { RemoveableTag },
  props: ["filters"],
  methods: {
    clearFilters() {
      this.$emit("clearFilters");
    },
    removeFilter(tag) {
      this.$emit("removeFilter", tag);
    },
  },
};
</script>

<style lang="scss" scoped>
.c-job-filter {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: white;
  padding: 13px 32px;
  border-radius: 7px;
  box-shadow: 5px 6px 25px -16px rgba(0, 0, 0, 0.3);
  position: absolute;
  width: 77%;
  top: 0;
  left: 50%;
  transform: translateX(-50%) translateY(-36px);
  @media only screen and (max-width: 850px) {
    padding: 13px 15px 13px 7px;
    position: relative;
    width: 100%;
    top: 0;
    left: 0;
    transform: translateX(0) translateY(-45px);
  }
}

.c-job-filter__container {
  display: flex;
  @media only screen and (max-width: 850px) {
    flex-wrap: wrap;
  }
}

.c-job-filter__clear {
  color: hsl(180, 29%, 50%);
  font-weight: bolder;
  cursor: pointer;
  &:hover {
    text-decoration: underline;
  }
  @media only screen and (max-width: 850px) {
    margin-left: 10px;
  }
}
</style>
