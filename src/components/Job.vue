<template>
  <div class="c-job" :class="{ 'c-job--featured': featured }">
    <div class="c-job__logo">
      <img :src="logo" />
    </div>
    <div class="c-job__content">
      <div class="c-job__content-top">
        <div class="c-job__content-company">{{ job.company }}</div>
        <div class="c-job__label c-job__label--new" v-if="job.new">New!</div>
        <div class="c-job__label c-job__label--featured" v-if="job.featured">
          Featured
        </div>
      </div>
      <div class="c-job__content-position">{{ job.position }}</div>
      <div class="c-job__content-bottom">
        <span className="added">{{ job.postedAt }}</span>
        <span className="type">{{ job.contract }}</span>
        <span className="location">{{ job.location }}</span>
      </div>
    </div>
    <div class="c-job__technologies">
      <div v-for="technology in technologies" v-bind:key="job.id + technology">
        <TechnologyTag :text="technology" @addFilter="addFilter" />
      </div>
    </div>
  </div>
</template>

<script>
import TechnologyTag from "./TechnologyTag";

export default {
  props: ["job"],
  components: { TechnologyTag },
  computed: {
    technologies: function() {
      return [
        this.job.role,
        this.job.level,
        ...this.job.languages,
        ...this.job.tools,
      ];
    },
    logo: function() {
      return require(`./../assets/${this.job.logo}`);
    },
    featured: function() {
      return this.job.featured;
    },
  },
  methods: {
    addFilter(tag) {
      this.$emit("addFilter", tag);
    },
  },
};
</script>

<style lang="scss" scoped>
.c-job {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: white;
  margin: 22px 7px;
  padding: 31px 0;
  border-radius: 7px;
  box-shadow: 5px 6px 25px -16px rgba(0, 0, 0, 0.3);
  position: relative;
  @media only screen and (max-width: 850px) {
    flex-direction: column;
    margin: 4px 0 40px 0;
    padding: 34px 23px 21px 23px;
    align-items: flex-start;
  }

  &--featured {
    &::before {
      content: "";
      display: block;
      position: absolute;
      height: 100%;
      width: 5px;
      border-top-left-radius: 7px;
      border-bottom-left-radius: 7px;
      background-color: hsl(180, 29%, 50%);
      left: 0;
      top: 0;
    }
  }
}

.c-job__logo {
  margin: 0 24px 0 40px;
  @media only screen and (max-width: 850px) {
    margin: 0;
    position: absolute;
    top: -24px;
    left: 24px;
    width: 48px;
    height: 48px;
    img {
      width: 100%;
      height: 100%;
    }
  }
}

.c-job__content {
  display: flex;
  flex-direction: column;
  @media only screen and (max-width: 1320px) {
    margin-right: auto;
  }
  @media only screen and (max-width: 850px) {
    width: 100%;
    margin-right: 0;
    border-bottom: 1px solid rgba(123, 142, 142, 0.5);
    padding-bottom: 21px;
    margin-bottom: 9px;
  }
}

.c-job__content-top {
  display: flex;
  align-items: center;
  margin-bottom: 14px;
}

.c-job__content-company {
  font-weight: bolder;
  color: hsl(180, 29%, 50%);
  margin-right: 15px;
  @media only screen and (max-width: 850px) {
    margin-right: 11px;
  }
}

.c-job__label {
  display: inline-block;
  padding: 8px 10px 4px 10px;
  border-radius: 20px;
  margin: 0 3px;
  text-transform: uppercase;
  font-weight: bolder;
  line-height: 10px;
  font-size: 10px;
  color: white;
  &--new {
    background-color: hsl(180, 29%, 50%);
  }
  &--featured {
    background-color: hsl(180, 14%, 20%);
  }
}

.c-job__content-position {
  font-weight: bolder;
  font-size: 18px;
  cursor: pointer;
  &:hover {
    color: hsl(180, 29%, 50%);
  }
  @media only screen and (max-width: 850px) {
    font-size: 15px;
  }
}

.c-job__content-bottom {
  margin-top: 12px;
  display: flex;
  color: hsl(180, 8%, 52%);
  font-size: 15px;
  white-space: nowrap;
  & > *:not(:first-child)::before {
    content: "•";
    transform: scale(2);
    display: inline-block;
    margin: 0 15px;
    @media only screen and (max-width: 850px) {
      margin: 0 7px;
    }
  }
  @media only screen and (max-width: 850px) {
    font-size: 13px;
  }
}

.c-job__technologies {
  margin-left: auto;
  margin-right: 30px;
  display: flex;
  @media only screen and (max-width: 1320px) {
    flex-wrap: wrap;
    margin-left: 50px;
  }
  @media only screen and (max-width: 850px) {
    margin: 0;
  }
}
</style>
