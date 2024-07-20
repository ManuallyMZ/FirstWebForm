<template>
  <form @submit.prevent="handleSubmit">

    <label>Email:</label>
    <input type="email" required v-model="email">

    <label>Password:</label>
    <input type="password" required v-model="password">
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label>Role:</label>
    <select v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <label>Skills:</label>
    <input  type="text" v-model="tempSkill" @keyup.space="addSkill">
    <div v-for="skill in skills" :key="skill" class="pill" @mouseover="skill.isHover = true" @mouseleave="skill.isHover = false"  @click="deleteSkill(skill)">

      <span>{{ skill.name }}</span>
      <div class="deleteBox" v-show="skill.isHover">X</div>
    </div>

    <div class="terms">
      <input type="checkbox" required v-model="terms">
      <label>Accept terms and conditions</label>
    </div>

    <div class="submit">
      <button>Create an Account</button>
    </div>

  </form>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: '',
      role: '',
      terms: false,
      tempSkill: '',
      skills: [],
      passwordError: ''
    }
  },
  methods: {
    addSkill(e){
      if(this.tempSkill){
        if(!this.skills.some(skill => skill.name === this.tempSkill)){
          this.skills.push({name: this.tempSkill, isHover: false})
        }
        this.tempSkill = ''
      }
    },
    deleteSkill(skill) {
      const index = this.skills.indexOf(skill);
      if (index !== -1) {
        this.skills.splice(index, 1);
      }
    },
    handleSubmit(){
      this.passwordError = this.password.length > 5 ? '' : 'Password must be at least 6 chars long';
      
      if (!this.passwordError) {
        console.log(
          'email: ', this.email, 
          'password: ', this.password, 
          'role: ', this.role, 
          'skills: ', this.skills, 
          'terms accepted: ', this.terms
        );
      }
    }
  }
}
</script>

<style>
form {
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}
label {
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input, select {
    background: #e0e0e0;
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #555;
    color: #555;
    border-radius: 15px;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 20px 6px 12px;
  background: #bbbbbb;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #555;
  cursor: pointer;
}
.deleteBox {
  display: inline;
  margin: -20px 0 0 5px;
  padding: -4px 1px;
  border-radius: 80%;
  border: 1px solid black;
  background: #bbbbbb83;
  color: black;
  font-weight: bold;
  font-size: 12px;
}
button {
  background: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 20px;
  color: white;
  border-radius: 20px;
}
.submit {
  text-align: center;
}
.error {
  color: #ff0062;
  margin-top: 10px;
  font-size: 0.8em;
  font-weight: bold;
}
</style>