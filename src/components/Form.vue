<template>
  <div class="form">
    <h2>
      {{ msg }}
      <span>{{ randomNumber }}</span>
    </h2>
    <form action>
      <label for="name">your name</label>
      <input name="name" v-model="name" type="text" />
      <label for="vehicle">your vehicle</label>
      <input type="text" v-model="vehicle" name="vehicle" />
      <input type="submit" v-on:click="submit" />
    </form>
    <FormDisplay :submissions="submissions" @deleteMe="deleteMe" />
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
    randomNumber: 0,
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
    deleteMe(info) {
      this.randomNumber = info.randomNumber
      this.submissions = this.submissions.filter(
        (item, index) => index !== info.index
      )
    },
  },
}
</script>
