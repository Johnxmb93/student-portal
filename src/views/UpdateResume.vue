<template>
  <div class="update">
    <div>
      <form v-on:submit.prevent="updateEducation()">
        <ul>
          <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
        </ul>
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
      </form>
    </div>
    <div>
      <form v-on:submit.prevent="updateCapstone()">
        <ul>
          <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
        </ul>
        Name:
        <input type="text" v-model="currentCapstoneParams.name" />
        Description:
        <input type="text" v-model="currentCapstoneParams.description" />
        Url:
        <input type="text" v-model="currentCapstoneParams.url" />
        Picture:
        <input type="text" v-model="currentCapstoneParams.screenshot" />
      </form>
    </div>
    <div>
      <form v-on:submit.prevent="updateSkills()">
        <ul>
          <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
        </ul>
        Skill:
        <input type="text" v-model="currentSkillParams.skill_id" />
        Description:
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
      skills: [],
      capstones: [],
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
    updateSkills: function () {
      axios.patch(`/skills/${this.$route.params.id}`, this.currentSkillParams).then((response) => {
        console.log(response.data);
      });
    },
    updateCapstone: function () {
      axios.patch(`/capstones/${this.$route.params.id}`, this.currentCapstoneParams).then((response) => {
        console.log(response.data);
      });
    },
    showExperience: function () {
      axios.get("/experiences/" + this.$route.params.id).then((response) => {
        this.experience = response.data;
        console.log(this.experience);
      });
    },
    showSkill: function () {
      axios.get("/skills/" + this.$route.params.id).then((response) => {
        this.skill = response.data;
        console.log(this.skill);
      });
    },
    showCapstone: function () {
      axios.get("/capstones/" + this.$route.params.id).then((response) => {
        this.capstone = response.data;
        console.log(this.capstone);
      });
    },
    showEducation: function () {
      axios.get("/education/" + this.$route.params.id).then((response) => {
        this.capstone = response.data;
        console.log(this.capstone);
      });
    },
  },
};
</script>
