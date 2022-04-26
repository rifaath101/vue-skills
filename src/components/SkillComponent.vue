<template>
  <div class="hello">
    <div class="holder">
      <ValidationObserver v-slot="{ handleSubmit }">
        <form @submit.prevent="handleSubmit(onSubmit)">
          <ValidationProvider
            name="skill"
            rules="required|min:8|max:13"
            v-slot="{ errors }"
          >
            <input
              type="text"
              placeholder="Enter a skill you have..."
              v-model="skill"
              v-validate="'min:5'"
              name="skill"
            />

            <p class="alert">
              {{ errors[0] }}
            </p>
          </ValidationProvider>
        </form>
      </ValidationObserver>

      <ul>
        <li v-for="(data, index) in skills" :key="index">
          {{ data.skill }}
        </li>
      </ul>

      <p>These are the skills that you possess</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "SkillComponent",
  data() {
    /* Properties - You can think of this as variables    */
    return {
      skill: "",
      /* v-model is a directive that takes a variable that stores the value of the input field. 
      It ignores the initial state and treats the current bound Js state as the source of truth.
       */
      skills: [{ skill: "Vue.js" }, { skill: "React.js" }],
      alertObject: {
        alert: true,
      },
    }
  },
  methods: {
    onSubmit() {
      /* This method will be called when the form is submitted  */
      this.skills.push({ skill: this.skill })
      this.skill = ""
      console.log(this.skills)
    },
  },
}
</script>

<style scoped>
/* Scoped means that the styles mentioned in this component will be applied to this component only */

@import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";
@import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css";
.holder {
  background: #fff;
}
ul {
  margin: 0;
  padding: 0;
  list-style-type: none;
}

ul li {
  padding: 20px;
  font-size: 1.3em;
  background-color: #e0edf4;
  border-left: 5px solid #3eb3f6;
  margin-bottom: 2px;
  color: #3e5252;
}
p {
  text-align: center;
  padding: 30px 0;
  color: gray;
}
.container {
  box-shadow: 0px 0px 40px lightgray;
}
input {
  width: calc(100% - 40px);
  border: 0;
  padding: 20px;
  font-size: 1.3em;
  background-color: #323333;
  color: #687f7f;
}
.alert {
  background: #fdf2ce;
  font-weight: bold;
  display: inline-block;
  padding: 5px;
  margin-top: -20px;
}
.alert-in-enter-active {
  animation: bounce-in 0.5s;
}
.alert-in-leave-active {
  animation: bounce-in 0.5s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.5);
  }
  100% {
    transform: scale(1);
  }
}
i {
  float: right;
  cursor: pointer;
}
</style>
