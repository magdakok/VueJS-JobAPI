<template>
  <div class="c-dashboard">
    <div class="c-dashboard__header"></div>
    <div class="c-dashboard__container">
      <transition name="fade" appear v-if="filters.length">
        <JobFilter
          :filters="filters"
          @clearFilters="clearFilters"
          @removeFilter="removeFilter"
        />
      </transition>
      <transition-group name="fade" tag="div" appear v-if="filters.length">
        <div v-for="job in filteredJobs" v-bind:key="job.id">
          <Job :job="job" @addFilter="addFilter" />
        </div>
      </transition-group>
      <transition-group name="fade" tag="div" appear v-else>
        <div v-for="job in jobs" v-bind:key="job.id">
          <Job :job="job" @addFilter="addFilter" />
        </div>
      </transition-group>
    </div>
  </div>
</template>

<script>
import { jobsdata } from "./../data";
import Job from "./Job";
import JobFilter from "./JobFilter";

export default {
  components: { Job, JobFilter },
  data() {
    return {
      jobs: jobsdata,
      filters: [],
    };
  },
  computed: {
    filteredJobs: function() {
      let newList = [];
      this.jobs.map((i) => {
        let technologies = [
          i.role,
          i.level,
          ...i.languages,
          ...i.tools,
        ].map((v) => v.toLowerCase());
        let filteredLowerCase = this.filters.map((v) => v.toLowerCase());
        if (filteredLowerCase.every((item) => technologies.includes(item))) {
          newList = [...newList, i];
        }
      });
      return newList;
    },
  },
  methods: {
    addFilter: function(newFilter) {
      if (
        !this.filters
          .map((v) => v.toLowerCase())
          .includes(newFilter.toLowerCase())
      ) {
        this.filters = [...this.filters, newFilter];
      }
    },
    clearFilters: function() {
      this.filters = [];
    },
    removeFilter: function(tag) {
      this.filters = this.filters.filter((f) => f !== tag);
    },
  },
};
</script>

<style lang="scss" scoped>
.c-dashboard {
  min-height: 100vh;
  background-color: #effafa;
}

.c-dashboard__header {
  height: 156px;
  background-color: hsl(180, 29%, 50%);
  /* background-image: url(${backgroundSvgDesktop}); */
  background-size: cover;
  @media only screen and (max-width: 850px) {
    /* background-image: url(${backgroundSvgMobile}); */
  }
}

.c-dashboard__container {
  padding: 52px 11%;
  position: relative;
  @media only screen and (max-width: 850px) {
    padding: 10px 6.5%;
  }
}
</style>
