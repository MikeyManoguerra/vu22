<template>
  <div>
    <p class="bolded" v-if="submissions.length">{{ submissionsDisplay[currentUser].name }}</p>
    <p class="bolded" v-if="submissions.length">{{ submissionsDisplay[currentUser].vehicle }}</p>
    <button v-on:click="click">click me</button>

    <div class="container">
      <ListItem
        v-for="(s, index) in submissionsDisplay"
        :currentUser="currentUser"
        :index="index"
        :item="s"
        v-bind:key="index"
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
      currentUser: 0,
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
      this.currentUser =
        this.currentUser >= this.submissionsDisplay.length - 1
          ? 0
          : this.currentUser + 1
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

.container{
  display: flex;
  flex-wrap: wrap;
}
</style>