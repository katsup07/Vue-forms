<template>
  <ul>
    <li>
      <button :class="{active: modelValue === 'poor'}" type="button" @click="activate('poor')">Poor</button></li>
    <li><button :class="{active: modelValue === 'average'}" type="button" @click="activate('average')">Average</button></li>
    <li><button :class="{active: modelValue === 'great'}" type="button" @click="activate('great')">Great</button></li>
  </ul>
</template>
<script>

export default{
  props: ['modelValue'], // bound to "rating" in TheForm
  emits: ['update:modelValue'],
 /*  data(){
    return{
      activeOption: this.modelValue, //! This only initializes and will not reflect changes later from modelValue when the form is submitted in TheForm, which leaves the button wrongly active. Other than that it works fine.
    };
  }, */
  methods: {
    activate(option){
      this.$emit('update:modelValue', option);
      setTimeout(() => console.log(this.modelValue), 100);
    },
  }
}
</script>

<style scoped>
ul{
  list-style: none;
  margin: 0.5rem 0;
  padding: 0;
  display: flex;
}

li{
  margin: 0 1rem;
  font-size: 0.8rem;
  transition: background 0.2s;
}


.active {
  background: rgb(255, 123, 117);
    color: black;
}

  button {
    font: inherit;
    border: none;
    border-radius: 2rem;
    background: rgb(148, 175, 211);
    cursor: pointer;
    padding: 0.2rem 0.5rem;
    color: white;
    transition: color 0.2s background 0.2s;
    overflow: hidden;
  }

.active button{
  background: rgb(255, 123, 117);
}
  button:hover{
    background: rgb(255, 123, 117);
    color: black;
  }

</style>