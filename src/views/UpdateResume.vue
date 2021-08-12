<template>
  <div class="update">
    <form></form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      errors: [],
      currentEducationParams: {},
      currentExperienceParams: {},
      currentSkillParams: {},
      currentCapstoneParams: {},
    };
  },
  created: function () {},
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
  },
};
</script>
