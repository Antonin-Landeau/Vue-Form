<template>
  <form @submit.prevent="handleSubmit">
    <h2>Register</h2>
    <font-awesome-icon icon="fa-solid fa-minus" />
    <div class="field">
      <label>Email</label><input v-model="email" type="text" />
    </div>
    <div class="field">
      <label>Password</label><input v-model="password" type="password" />
    </div>
    <div class="field">
      <label>Work</label>
      <select v-model="work">
        <option value="Web Developer">Web Developer</option>
        <option value="UI/UX designer">UI/UX Designer</option>
      </select>
    </div>
    <div class="skills-field field">
      <label>Skills <span class="consigne">(Barre espace pour ajouter)</span></label>
      <span
        ><input type="text" v-model="skillInput" @keyup.space="addSkill" /><i
          @click="addSkill"
          class="fa-solid fa-circle-plus"
        ></i
      ></span>
      <div class="skills">
        <div class="skill" v-for="skill in skills" :key="skill">
          <p>{{ skill }}</p>
          <i @click="removeSkill(skill)" class="fa-regular fa-circle-xmark"></i>
        </div>
      </div>
    </div>
    <div class="checkbox field">
      <input type="checkbox" v-model="therms" />
      <label>Accept <span>thermes</span> and <span>authorization</span>.</label>
    </div>
    <p class="error">{{ error }}</p>
    <button>Create Account</button>
  </form>
</template>

<script>
export default {
  name: "formCompponent",
  data() {
    return {
      email: "",
      password: "",
      work: "",
      therms: "",
      skillInput: "",
      skills: [],
      error: "",
    };
  },
  methods: {
    addSkill() {
      if (this.skillInput) {
        this.skills.push(this.skillInput);
      }
      this.skillInput = "";
    },
    removeSkill(skill) {
      console.log("remove skil", skill);
      this.skills = this.skills.filter((item) => {
        return item !== skill;
      });
    },
    handleSubmit() {
      if (this.therms) {
        this.error = "";
        console.log("email: ", this.email);
        console.log("password", this.password);
        console.log("job", this.work);
        console.table("skills",this.skills);
        
      } else {
        this.error = "Veuillez accepter les termes condition générals";
      }
    },
  },
};
</script>

<style scoped>
.consigne {
  text-transform: lowercase;
  color: #848484;
  font-weight: 400;
}
form {
  margin: 200px auto;
  background-color: #fcfcfc;
  width: 50%;
  padding: 40px;
  border-radius: 20px;
}
label {
  text-transform: uppercase;
  font-size: 12px;
  font-weight: 900;
  color: #bc6c25;
  letter-spacing: 1px;
}

.field {
  display: flex;
  flex-direction: column;
  margin: 20px auto;
}
input,
select {
  background: transparent;
  padding: 10px 3px 7px 3px;
  border: none;
  border-bottom: 1px solid #bababa;
  font-size: 18px;
  color: #848484;
}

input:focus,
select:focus {
  outline: none;
}

button {
  font-size: 18px;
  padding: 10px 20px;
  border: none;
  background: #bc6c25;
  color: white;
  border-radius: 5px;
  display: block;
  margin: 20px auto 0 auto;
}
button:hover {
  cursor: pointer;
}
h2 {
  font-size: 32px;
  text-align: center;
  color: #12130f;
}
.checkbox {
  flex-direction: row;
}
.checkbox label {
  color: #c6c6c6;
}
.checkbox input {
  margin-right: 10px;
  padding: 5px;
  width: 1.1rem;
}
.checkbox > label > span {
  color: #bc6c25;
}
.skills-field > span {
  position: relative;
}
.skills-field > span > input {
  width: 100%;
}
.fa-circle-plus {
  position: absolute;
  right: 3px;
  top: 50%;
  transform: translateY(-50%);
  color: #848484;
}
.fa-soli {
  color: #848484;
}

.fa-solid:hover,
.fa-regular:hover {
  cursor: pointer;
}

.skills,
.skill {
  display: flex;
  flex-direction: row;
}
.skills {
  padding: 0 0 5px 0;
  white-space: nowrap;
  overflow-y: hidden;
  margin: 7px 0 0 0;
}
.skill {
  background: #bc6c25;
  padding: 5px 10px;
  border-radius: 50px;
  align-items: center;
  margin: 0 5px 0 0;
}
.skill p {
  color: white;
  font-size: 14px;
}

.fa-circle-xmark {
  color: white;
  margin-left: 7px;
  font-size: 14px;
}
.error {
  color: #ff0000;
  font-size: 12px;
}
</style>
