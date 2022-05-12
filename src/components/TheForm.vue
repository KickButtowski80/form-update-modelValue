<template>
  <form v-on:submit.prevent="submitForm">
    <div
      class="form-control"
      :class="{ invalid: userNameValidity === 'invalid' }"
    >
      <label for="user-name">Your Name</label>
      <input
        id="user-name"
        name="user-name"
        type="text"
        :value="userName"
        v-on:change="getUserName"
        v-on:blur="vaildateInput"
      />
    </div>
    <p v-if="userNameValidity === 'invalid'">the field is invalid</p>
    <div class="form-control">
      <label for="age">Your Age (Years)</label>
      <input
        id="age"
        name="age"
        type="text"
        ref="ageInput"
        v-model.number="userAge"
      />
    </div>
    <div class="form-control">
      <label for="referrer">How did you hear about us?</label>
      <select
        id="referrer"
        name="referrer"
        @change="referrer = $event.target.value"
      >
        <option value="google">Google</option>
        <option value="wom">Word of mouth</option>
        <option value="newspaper">Newspaper</option>
      </select>
    </div>
    <div class="form-control">
      <h2>What are you interested in?</h2>
      <div>
        <input
          id="interest-news"
          name="interest1"
          type="checkbox"
          value="News"
          :checked="checked"
          v-on:change="grabCheckValues"
        />
        <label for="interest-news">News</label>
      </div>
      <div>
        <input
          id="interest-tutorials"
          name="interest2"
          type="checkbox"
          :checked="checked"
          value="Tutorials"
          v-on:change="grabCheckValues"
        />
        <label for="interest-tutorials">Tutorials</label>
      </div>
      <div>
        <input
          id="interest-nothing"
          name="interest3"
          type="checkbox"
          :checked="checked"
          value="Nothing"
          v-on:change="grabCheckValues"
        />
        <label for="interest-nothing">Nothing</label>
      </div>
    </div>
    <div class="form-control">
      <h2>How do you learn?</h2>
      <div>
        <input
          id="how-video"
          name="how"
          value="video"
          type="radio"
          v-on:input="how = $event.target.value"
        />
        <label for="how-video">Video Courses</label>
      </div>
      <div>
        <input
          id="how-blogs"
          name="how"
          value="blog"
          type="radio"
          v-on:input="how = $event.target.value"
        />
        <label for="how-blogs">Blogs</label>
      </div>
      <div>
        <input
          id="how-other"
          name="how"
          value="other"
          type="radio"
          v-on:input="how = $event.target.value"
        />
        <label for="how-other">Other</label>
      </div>
    </div>
    <div class="form-control">
      <!-- <rating-control v-model="rating"> </rating-control> -->
      <rating-control 
      v-bind:model-value='rating'
      v-on:update:modelValue='gotRating'></rating-control>
    </div>
    <div class="form-control">
      <input
        type="checkbox"
        name="confirm-terms"
        id="confirm-terms"
        v-model="confirm"
      />
      <label for="confirm-term"> Agree to terms of use? </label>
    </div>
    <div>
      <button>Save Data</button>
    </div>
  </form>
</template>

<script>
import RatingControl from './RatingControl.vue';

export default {
  components: { RatingControl },
  data() {
    return {
      userName: '',
      userAge: null,
      referrer: 'wom',
      checked: false,
      interests: new Set(),
      how: null,
      confirm: false,
      rating: null,
      userNameValidity: 'pending',
    };
  },
  computed: {
    interestsActivties() {
      return this.interests;
    },
  },
  methods: {

    gotRating(event) {
      // debugger;
        this.rating = event
    },
    vaildateInput() {
      if (this.userName.trim() === '') {
        this.userNameValidity = 'invalid';
        return;
      }
      this.userNameValidity = 'valid';
    },
    grabCheckValues(event) {
      this.interestsActivties.add(event.target.value);
    },
    getUserName(event) {
      this.userName = event.target.value;
    },
    getUserAge(event) {
      this.userAge = event.target.value;
    },
    submitForm() {
      console.log(this.userName);
      console.log(31 + 5);
      console.log(this.userAge + 5);
      console.log(this.$refs.ageInput.value + 5);
      console.log('referrer', this.referrer);
      this.referrer = 'wom';
      console.log('check box ', this.interestsActivties);
      console.log('options', this.how);
      console.log('agree', this.confirm);
      console.log('rating', this.rating)
      this.rating = null;
    },
  },
};
</script>

<style scoped>
form {
  margin: 2rem auto;
  max-width: 40rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 2rem;
  background-color: #ffffff;
}

.form-control {
  margin: 0.5rem 0;
}

label {
  font-weight: bold;
}

h2 {
  font-size: 1rem;
  margin: 0.5rem 0;
}

input,
select {
  display: block;
  width: 100%;
  font: inherit;
  margin-top: 0.5rem;
}

select {
  width: auto;
}

input[type='checkbox'],
input[type='radio'] {
  display: inline-block;
  width: auto;
  margin-right: 1rem;
}

input[type='checkbox'] + label,
input[type='radio'] + label {
  font-weight: normal;
}

.invalid input[type='text'] {
  border-color: red;
}
.form-control.invalid label {
  color: red;
}
button {
  font: inherit;
  border: 1px solid #0076bb;
  background-color: #0076bb;
  color: white;
  cursor: pointer;
  padding: 0.75rem 2rem;
  border-radius: 30px;
}

button:hover,
button:active {
  border-color: #002350;
  background-color: #002350;
}
</style>