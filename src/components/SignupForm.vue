<template>
  <form @submit.prevent="handleSubmit">
  
    <label>Email:</label>
    <input type="email" required v-model="email">
    
    <br>
    
    <label>Password:</label>
    <input type="password" required v-model="password">
    <div v-if="passwordError" class="error">{{  passwordError }}</div>

    <br>

    <label>Role:</label>
    <select v-model="role">
        <option value="developer">Web Developper</option>
        <option value="designer">Web Designer</option>
    </select>

    <br>

    <div class="terms"> 
        <input type="checkbox" required v-model="terms">
        <label>Accept terms and conditions</label>
    </div>

    <br>

    <div>
        <input type="checkbox" value="shaun" v-model="names">
        <label>Shaun</label>
    </div>
    <div>
        <input type="checkbox" value="yoshi" v-model="names">
        <label>Yoshi</label>
    </div>
    <div>
        <input type="checkbox" value="marion" v-model="names">
        <label>Mario</label>
    </div>

    <br>

    <div>
        <label>Skills:</label>
        <input type="text" v-model="tempSkill" @keyup="addSkill">
    </div>
    <div v-for="skill in skills" :key="skill" class="skill" @click="removeSkill(skill)">
        {{ skill }}
    </div>

    <br>

    <div class="submit">
        <button>Submit</button>
    </div>

  </form>

 

  <p>Email : {{ email }}</p>
  <p>Password : {{ password }}</p>
  <p>Role: {{ role }}</p>
  <p>Terms: {{ terms }}</p>
  <p>Names: {{ names }}</p>
  <p>Skills : {{ skills }}</p>

</template>

<script>
export default {
    data() {
        return {
            email: '',
            password: '',
            role: 'designer',
            terms: false,
            names: [],
            tempSkill: '',
            skills: [],
            passwordError: ''
        }
    },
    methods: {
        addSkill(e) {
            if (e.key === ',' && this.tempSkill) {
                this.tempSkill = this.tempSkill.replace(',', '')
                if (!this.skills.includes(this.tempSkill)) {
                    this.skills.push(this.tempSkill)
                }
                this.tempSkill = ''
            }
        },
        removeSkill(skill) {
            this.skills = this.skills.filter((s) => s !== skill)
        },
        handleSubmit() {
            this.passwordError = this.password.length > 5 ? 
             '' : 'Password must be at least 5 characters long !'

            if (!this.passwordError) {
                console.log("email: " + this.email);
                console.log("password: " + this.password);
                console.log("role: " + this.role);
                console.log("skills " + this.skills);
            }

        }
    }
}
</script>

<style>
  .skill {
    border: 1px solid black;
    background: white;
    border-radius: 10px;
    display: inline-block;
    padding: 5px;
    margin: 5px;
    cursor: pointer;
  }
  .error {
    color: red;
    font-weight: bolder;
  }
  button {
    padding: 10px 20px;
    margin: 20px;
    border: 0;
    background: #0b6dff;
    color: white;
    border-radius: 20px;
  }
</style>