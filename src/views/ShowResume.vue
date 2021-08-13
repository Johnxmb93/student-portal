<template>
  <div class="resume-index">
    <h2>Student:</h2>

    <div v-if="$parent.getUserId() == student.id">
      <p>Name: {{ student.first_name }} {{ student.last_name }}</p>

      <p>Skills:</p>
      <li v-for="skill in student.skills" :key="skill.id">{{ skill.name }}</li>

      <router-link v-bind:to="`/resume/${student.id}/edit`">add</router-link>

      <hr />
      <h3>Education:</h3>
      <div v-for="education in student.education" :key="education.id">
        <p>University: {{ education.university_name }}</p>
        <p>Details: {{ education.details }}</p>
        <p>Through: {{ education.start_date }} - {{ education.end_date }}</p>
      </div>
      <router-link v-bind:to="`/resume/${student.id}/edit`">edit</router-link>
      <hr />
      <h3>Experience:</h3>
      <p>Job Title: {{ experience.job_title }}</p>
      <p>Company: {{ experience.company }}</p>
      <p>Details: {{ experience.details }}</p>
      <p>Through: {{ experience.start_date }} - {{ experience.end_date }}</p>
      <router-link v-bind:to="`/resume/${student.id}/edit`">edit</router-link>
      <hr />
      <h3>Capstones:</h3>
      <div v-for="capstones in student.capstones" :key="capstones.id">
        <p>Name: {{ capstones.name }}</p>
        <p>Description: {{ capstones.description }}</p>
        <p>Url: {{ capstones.url }}</p>
        Photo:
        <p><img v-bind:src="capstones.screenshot" /></p>
        <p>
          <router-link v-bind:to="`/resume/${student.id}/edit`">edit</router-link>
        </p>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";

export default {
  data: function () {
    return {
      student: [],
      experience: [],
      skill: [],
      capstone: [],
      education: [],
    };
  },
  created: function () {
    this.showStudent();
    this.showExperience();
    this.showSkill();
    this.showCapstone();
    this.showEducation();
  },
  methods: {
    showStudent: function () {
      axios.get("/resumes/" + this.$route.params.id).then((response) => {
        this.student = response.data;
        console.log(this.student);
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
        this.education = response.data;
        console.log(this.education);
      });
    },
  },
};
</script>
