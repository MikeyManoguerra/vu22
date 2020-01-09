<template>
  <div>
    <p class="bolded" v-if="submissions.length">{{ submissionsDisplay[currentIndex].name }}</p>
    <p class="bolded" v-if="submissions.length">{{ submissionsDisplay[currentIndex].vehicle }}</p>
    <button v-on:click="click">click me</button>

    <div class="container">
      <ListItem
        v-for="(s) in submissionsDisplay"
        :currentUserId="submissionsDisplay[currentIndex].id"
        :item="s"
        v-bind:key="s.id"
        @deleteMe="deleteMe"
      />
    </div>
  </div>
</template>

<script>
import ListItem from './ListItem'
export default {
  name: 'FormDisplay',
  components: {
    ListItem,
  },
  props: {
    submissions: {
      type: Array,
    },
  },
  data() {
    return {
      submissionsDisplay: this.submissions,
      currentIndex: 0,
    }
  },

  watch: {
    submissions: {
      immediate: true,
      handler(submissions) {
        this.submissionsDisplay = submissions
      },
    },
  },
  methods: {
    click() {
      this.currentIndex =
        this.currentIndex >= this.submissionsDisplay.length - 1
          ? 0
          : this.currentIndex + 1
    },
    deleteMe(info) {
      return this.$emit('deleteMe', info)
    },
  },
}
</script>

<style >
.bolded {
  display: inline;
  padding: 10px;
  font-size: 40px;
  font-weight: bolder;
}
button {
  display: block;
  margin: 10px auto;
}

.container {
  display: flex;
  flex-wrap: wrap;
}
</style>