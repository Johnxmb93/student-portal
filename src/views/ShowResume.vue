<template>
  <div class="resume-index">
    <h2>Student:</h2>
    <p>{{ student.first_name }} {{ student.last_name }}</p>

    <p>Skills:</p>
    <li v-for="skill in student.skills" :key="skill.id">{{ skill.name }}</li>

    <hr />
    <h3>Education:</h3>
    <div v-for="education in student.education" :key="education.id">
      <p>{{ education.university_name }}</p>
      <p>{{ education.details }}</p>
      <p>{{ education.start_date }} - {{ education.end_date }}</p>
    </div>

    <hr />
    <h3>Experience:</h3>
    <p>{{ experience.job_title }}</p>
    <p>{{ experience.company }}</p>
    <p>{{ experience.details }}</p>
    <p>{{ experience.start_date }} - {{ experience.end_date }}</p>
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
      axios.get("/students/" + this.$route.params.id).then((response) => {
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
