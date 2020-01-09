<template>
  <div class="form">
    <h2>{{ msg }}</h2>
    <form action>
      <label for="name">your name</label>
      <input name="name" v-model="name" type="text" />
      <label for="vehicle">your vehicle</label>
      <input type="text" v-model="vehicle" name="vehicle" />
      <input type="submit" v-on:click="submit" />
    </form>
    <FormDisplay :submissions="submissions" />
  </div>
</template>

<script>
import FormDisplay from '../components/FormDisplay'
export default {
  name: 'Form',
  components: {
    FormDisplay,
  },
  props: {
    msg: { type: String, default: 'nah' },
  },
  data: () => ({
    name: '',
    vehicle: 'bicycle',
    submissions: [],
  }),
  methods: {
    submit() {
      event.preventDefault()
      this.submissions = [
        ...this.submissions,
        { name: this.name, vehicle: this.vehicle },
      ]
      this.name = ''
      this.vehicle = ''
    },
  },
}
</script>
