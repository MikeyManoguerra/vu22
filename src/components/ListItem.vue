<template>
  <div draggable="true" class="item-guy" v-bind:class="{ active: activeItem, selected: selected }">
    <p>{{ item.vehicle }}</p>
    <p>{{ item.name }}</p>
    <button v-on:click="deleteThis">delete</button>
    <button v-on:click="toggle">check</button>
  </div>
</template>

<script>
export default {
  name: 'ListItem',
  props: {
    item: {
      type: Object,
    },
  
    currentUserId: {
      type: Number,
    },
  },
  data() {
    return {
      selected: false,
    }
  },
  methods: {
    toggle() {
      this.selected = !this.selected
    },
    deleteThis() {
      const importantInfo = {
        randomNumber: Math.floor(Math.random() * 10),
        id: this.item.id,
      }
      return this.$emit('deleteMe', importantInfo)
    },
  },

  computed: {
    activeItem() {
      return this.$props.item.id === this.$props.currentUserId ? 'active' : ''
    },
    highlightedItem() {
      return this.selected ? 'selected' : ''
    },
  },
}
</script>

<style>
.active {
  border: 1px solid red;
}
.selected {
  background-color: lightblue;
}
.item-guy {
  margin: 10px auto;
  padding: 10px;
  width: 250px;
  height: 150px;
  list-style-type: none;
}
</style>