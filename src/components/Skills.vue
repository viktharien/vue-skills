<template>
  <div class="skills">


    
    <div class="holder">
      <form @submit.prevent="addSkill">
        <input type="text" placeholder="Enter a skill you have.." v-model="skill" v-validate="'min:5'" name="skill"/>
        <transition name="alert-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
          <p class="alert" v-if="errors.has('skill')">{{ errors.first('skill') }}</p>
        </transition>
      </form>
      <ul>
        <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
          <li v-for="(data, index) in skills" :key='index'>
            {{ data.skill }}
            <i class="fa fa-minus-circle" v-on:click="remove(index)"></i>
            </li>
        </transition-group>
      </ul>

      <p>These are the skills that you possess.</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Skills',
  data() {
    return {
      skill: '',
      skills: [
        {"skill": "Vue.js"},
        {"skill": "Frontend Developer"},
      ],
    }
  },
  methods: {
    addSkill() {
      this.$validator.validateAll().then((result) => {
        if (result) {
          this.skills.push({skill: this.skill});
          this.skill = '';
        } else {
          console.log("Not valid");
        }
      });
      
    },
    remove(id) {
      this.skills.splice(id, 1);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  @import "https://cdn.jsdelivr.net/npm/animate.css@3.5.1";
  @import "https://use.fontawesome.com/releases/v5.0.13/css/all.css";
  

  ul {
    margin: 0;
    padding: 0;
    list-style-type: none;
  }
  
  ul li {
    padding: 20px;
    font-size: 1.3em;
    background-color: #E0EDF4;
    border-left: 5px solid #3EB3F6;
    margin-bottom: 2px;
    color: #3E5252;
  }

  p {
    text-align:center;
    padding: 30px 0;
    color: gray;
  }

  i {
    float: right;
    cursor: pointer;
  }

  .holder {
    background: #fff;
  }

  .container {
    box-shadow: 0px 0px 40px lightgray;
  }

  .alert {
    background-color: rgb(255, 255, 124);
    width:100%;
  }

  .alert-in-enter-active {
    animation: bounce-in .5s;
  }

  .alert-in-leave-active {
    animation: bounce-in .5s reverse;
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

  input {
    width: calc(100% - 40px);
    border: 0;
    padding: 20px;
    font-size: 1.3em;
    background: #323333;
    color: #687F7F;
  }
</style>
