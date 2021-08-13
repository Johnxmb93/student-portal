<template>
  <div class="update">
    <div>
      <form v-on:submit.prevent="updateEducation()">
        <ul>
          <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
        </ul>
        <h1>Education</h1>
        Start Date:
        <input type="text" v-model="currentEducationParams.start_date" />
        End Date:
        <input type="text" v-model="currentEducationParams.end_date" />
        Degree:
        <input type="text" v-model="currentEducationParams.degree" />
        University:
        <input type="text" v-model="currentEducationParams.university_name" />
        Details:
        <input type="text" v-model="currentEducationParams.details" />
        <input type="submit" value="submit" />
      </form>
    </div>
    <div>
      <form v-on:submit.prevent="updateExperience()">
        <ul>
          <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
        </ul>
        <h1>Experience</h1>
        Start Date:
        <input type="text" v-model="currentExperienceParams.start_date" />
        End Date:
        <input type="text" v-model="currentExperienceParams.end_date" />
        Job Title:
        <input type="text" v-model="currentExperienceParams.job_title" />
        Company:
        <input type="text" v-model="currentExperienceParams.company" />
        Details:
        <input type="text" v-model="currentExperienceParams.details" />
        <input type="submit" value="submit" />
      </form>
    </div>
    <div>
      <form v-on:submit.prevent="updateCapstone()">
        <ul>
          <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
        </ul>
        <h1>Capstone</h1>
        Name:
        <input type="text" v-model="currentCapstoneParams.name" />
        Description:
        <input type="text" v-model="currentCapstoneParams.description" />
        Url:
        <input type="text" v-model="currentCapstoneParams.url" />
        Picture:
        <input type="text" v-model="currentCapstoneParams.screenshot" />
        <input type="submit" value="submit" />
      </form>
    </div>
    <div>
      <form v-on:submit.prevent="updateSkill()">
        <ul>
          <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
        </ul>
        <h1>Skills</h1>
        Skill:
        <input type="text" v-model="currentSkillParams.skill_id" />
        <input type="submit" value="submit" />
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      currentEducationParams: {},
      currentExperienceParams: {},
      currentSkillParams: {},
      currentCapstoneParams: {},
      experience: [],
      education: [],
      skill: [],
      capstone: [],
      errors: [],
    };
  },
  created: function () {
    this.showExperience();
    this.showSkill();
    this.showCapstone();
    this.showEducation();
  },
  methods: {
    updateEducation: function () {
      axios.patch(`/education/${this.$route.params.id}`, this.currentEducationParams).then((response) => {
        console.log(response.data);
      });
    },
    updateExperience: function () {
      axios.patch(`/experiences/${this.$route.params.id}`, this.currentExperienceParams).then((response) => {
        console.log(response.data);
      });
    },
    updateSkill: function () {
      axios.patch(`/skills/${this.$route.params.id}`, this.currentSkillParams).then((response) => {
        console.log(response.data);
      });
    },
    updateCapstone: function () {
      axios.patch(`/capstones/${this.$route.params.id}`, this.currentCapstoneParams).then((response) => {
        console.log(response.data);
      });
    },
    // #ahagha
    addSkill: function () {
      axios.post("/skills" + this.currentSkillParams).then((response) => {
        console.log(response.data, this.currentSkillParams);
      });
    },
    showExperience: function () {
      axios.get("/experiences/" + this.$route.params.id).then((response) => {
        this.currentExperienceParams = response.data;
        console.log(this.currentExperienceParams);
      });
    },
    showSkill: function () {
      axios.get("/skills/" + this.$route.params.id).then((response) => {
        this.currentSkillParams = response.data;
        console.log(this.currentSkillParams);
      });
    },
    showCapstone: function () {
      axios.get("/capstones/" + this.$route.params.id).then((response) => {
        this.currentCapstoneParams = response.data;
        console.log(this.currentCapstoneParams);
      });
    },
    showEducation: function () {
      axios.get("/education/" + this.$route.params.id).then((response) => {
        this.currentEducationParams = response.data;
        console.log(this.currentEducationParams);
      });
    },
  },
};
</script>
