<template>
  <li>
    <p>{{ item.vehicle }}</p>
    <p>{{ item.name }}</p>
  </li>
</template>

<script>
export default {
  name: 'ListItem',
  props: {
    item: {
      type: Object,
    },
  },
}
</script>
