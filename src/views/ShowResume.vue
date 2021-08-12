<template>
  <div class="resume-index">
    <!-- <p v-for="resume in resumes" :key="resume.id">{{ resumes }}</p> -->
  </div>
</template>
<script>
import axios from "axios";

export default {
  data: function () {
    return {
      // resumes: [],
      student: {},
      experience: {},
      skill: {},
      capstone: {},
    };
  },
  created: function () {
    this.showStudent();
    this.showExperience();
    this.showSkill();
    this.showCapstone();
  },
  methods: {
    // indexResume: function () {
    //   axios.get("/resume").then((response) => {
    //     this.resumes = response.data;
    //     console.log("All resumes", this.resumes);
    //   });
    // },
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
  },
};
</script>
