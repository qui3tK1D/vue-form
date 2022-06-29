<template>
  <form action="" @submit.prevent="handleSubmit">
    <label for="email">Email:</label>
    <input type="email" id="email" required v-model="email" />

    <label for="password">Password:</label>
    <input type="password" id="password" required v-model="password" />
    <div v-if="passwordError" class="error">{{ passwordError }}</div>

    <label for="role">Role:</label>
    <select id="role" v-model="role">
      <option value="developer">Web Developer</option>
      <option value="designer">Web Designer</option>
    </select>

    <label for="skills">Skills:</label>
    <input type="text" id="skills" v-model="tempSkill" @keyup="addSkills" />

    <div v-for="(skill, i) in skills" :key="i" class="pill">
      <span @click="deleteSkill(i)">{{ skill }}</span>
    </div>

    <div class="terms">
      <input type="checkbox" required id="terms" v-model="terms" />
      <label for="terms">Accept terms and conditions</label>
    </div>

    <div class="submit">
      <button>Create an Account</button>
    </div>

    <!-- <div>
      <input type="checkbox" id="name1" value="shaun" v-model="names" />
      <label for="name1">Shaun</label>
    </div>

    <div>
      <input type="checkbox" id="name2" value="steve" v-model="names" />
      <label for="name2">Steve</label>
    </div> -->
  </form>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "developer",
      tempSkill: "",
      skills: [],
      terms: false,
      passwordError: "",
      // names: [],
    };
  },
  methods: {
    addSkills(e) {
      if (e.key === "," && this.tempSkill) {
        // remove ','
        this.tempSkill = [...this.tempSkill].slice(0, -1).join("");

        // check if duplicate value and add
        if (!this.skills.includes(this.tempSkill)) {
          this.skills = [...this.skills, this.tempSkill];
        }

        this.tempSkill = "";
      }
    },

    deleteSkill(index) {
      this.skills = this.skills.filter((_, i) => i !== index);
    },

    handleSubmit() {
      //validate pw
      this.passwordError =
        this.password.length > 5
          ? ""
          : "Password must be at least 6 chars long.";
      if (!this.passwordError) {
        console.log("email: ", this.email);
        console.log("password: ", this.password);
        console.log("role: ", this.role);
        console.log("skills: ", this.skills);
        console.log("terms accepted: ", this.terms);
      }
    },
  },
};
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: #fff;
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

input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
  color: #555;
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
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  font-weight: bold;
  color: #777;
  cursor: pointer;
}

button {
  background: #0b6dff;
  border: 0;
  margin-top: 20px;
  padding: 10px 20px;
  color: #fff;
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
