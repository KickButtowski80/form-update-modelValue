<template>
  <ul>
    <li :class="{ active: choosenRating === 'Awful' }">
      <button v-on:click.prevent="chooseRating">Awful</button>
    </li>
    <li :class="{ active: choosenRating === 'Avarage' }">
      <button v-on:click.prevent="chooseRating">Avarage</button>
    </li>
    <li :class="{ active: choosenRating === 'Awesome' }">
      <button v-on:click.prevent="chooseRating">Awesome</button>
    </li>
  </ul>
</template>

<script>
export default {
  props: ['modelValue'],
  emits: ['update:modelValue'],
//   data() {
//     return {
//       choosenRating: this.modelValue,
//     };
//   },
  computed: {
      choosenRating() {
          return this.modelValue;
      }
  },
  methods: {
    chooseRating(event) {
      this.choosenRating = event.target.innerText;
      this.$emit('update:modelValue', event.target.innerText)
    },
  },
};
</script>

<style scoped>
.active {
  border-color: #a00078;
  background-color: #7d416e;
}

.active button {
  border-color: #a00078;
  color: white;
}

button {
  border: none;
  font: inherit;
  background-color: transparent;
  cursor: pointer;
}
ul {
  display: felx;
  margin: 0.5rem 0;
  padding: 0;
}
li {
  list-style: none;
  display: inline-flex;
  margin: 0 1rem;
  border: 1px solid #ccc;
  padding: 1rem;
  justify-content: center;
  align-items: center;
}
</style>