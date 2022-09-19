<template>
  <form @submit.prevent="submitForm">
    <div class="form-control" :class="{invalid: userNameValidity === 'invalid'}">
      <label for="user-name">Your Name</label>
      <!-- "blur" is a built in event that gets called when the element is no longer in focus -->
      <input id="user-name" name="user-name" type="text" v-model.trim="userName" @blur="validateInput"/>
      <p :class="{invalid: userNameValidity === 'invalid'}" v-if="userNameValidity === 'invalid'">**Invalid name**</p>
    </div>
    <div class="form-control">
      <label for="age">Your Age (Years)</label>
      <input id="age" name="age" type="number" v-model="userAge" ref="ageInput" />
    </div>
    <div class="form-control">
      <label for="referrer">How did you hear about us?</label>
      <select id="referrer" name="referrer" v-model="referrer">
        <option value="no-selection">-- select one --</option>
        <option value="google">Google</option>
        <option value="wom">Word of mouth</option>
        <option value="newspaper">Newspaper</option>
      </select>
    </div>
    <!--Need a value="" attribute to distinguish elements, and also an array in data() so Vue can keep track of multiple elements in v-model that belong to the "select group".  -->
    <div class="form-control">
      <h2>What are you interested in?</h2>
      <div>
        <input id="interest-news" name="interest" type="checkbox" value="news" v-model="interest"/>
        <label for="interest-news">News</label>
      </div>
      <div>
        <input id="interest-tutorials" name="interest" type="checkbox" value="tutorials" v-model="interest"/>
        <label for="interest-tutorials">Tutorials</label>
      </div>
      <div>
        <input id="interest-nothing" name="interest" type="checkbox" value="nothing" v-model="interest"/>
        <label for="interest-nothing">Nothing</label>
      </div>
    </div>
    <div class="form-control">
      <h2>How do you learn?</h2>
      <div>
        <input id="how-video" name="how" type="radio" value="video" v-model="how"/>
        <label for="how-video">Video Courses</label>
      </div>
      <div>
        <input id="how-blogs" name="how" type="radio" value="blogs" v-model="how"/>
        <label for="how-blogs">Blogs</label>
      </div>
      <div>                                             <!-- :value="other" @input="()=>this.how = 'other'"-->
        <input id="how-other" name="how" type="radio" value="other" v-model="how"/>
        <label for="how-other">Other</label>
      </div>
    </div>
    <div class="form-control">
      <!-- custom v-model="rating" is the same as
           1) :modelValue="rating" which is saved to state below and brings the value into the markup, and
           2) @update:modelValue="$emitted_from_RatingControl_activate()_function" and sets the value when changed, -->
      <rating-control v-model="rating" ></rating-control>
    </div>
      <div class="form-control">
        <h2>Terms of Usage</h2>
        <input id="confirm-terms" name="confirm-terms" type="checkbox" value="news" v-model="confirm"/>
          <label for="confirm-terms">Agree to terms of use</label>
      </div>
    <div>
      <button>Save Data</button>
    </div>
  </form>
</template>
<script>
  import RatingControl from './RatingControl.vue';

export default {
  components: {
    RatingControl,
  },
  data(){
    return {
      userName: '',
      userAge: null,
      referrer: 'no-selection',
      interest: [],
      how: null,
      confirm: false,
      userNameValidity: 'pending',
      rating: '',
    }
  },
  methods:{
    submitForm(){
      console.log(this.userName, this.userAge, this.referrer, this.interest, this.how, this.confirm, this.rating);
      [ this.userName, this.userAge, this.referrer, this.interest, this.how, this.confirm, this.rating ] = 
      [   '',            null,       'no-selection',   [],           null,     false,       null      ];
    },
    validateInput(){
      this.userNameValidity = this.userName === '' ? 'invalid' : 'valid';
    }
},
}
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

/* highlights there was an error */
.form-control.invalid input{
  border-color: red;
}
.form-control.invalid label{
  color: red;
}

p.invalid{
  background: rgb(254, 178, 178);
  font-size: 0.5rem;
  margin-top:0.1rem;
  padding: 0.1rem 1rem;
  border-radius: 15px;
  display:inline;
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

button {
  font: inherit;
  border: 1px solid #0076bb;
  background-color: #0076bb;
  color: white;
  cursor: pointer;
  margin-top: 0.5rem;
  padding: 0.5rem 2rem;
  border-radius: 30px;
}

button:hover,
button:active {
  border-color: #002350;
  background-color: #002350;
}
</style>