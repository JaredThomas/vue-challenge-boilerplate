<template>
  <div class="container">
    <AcademicFitReport :athlete="athlete_info" :update-name="updateName" />
  </div>
</template>

<script>
import AcademicFitReport from "@/components/AcademicFitReport.vue";
import AthleteData from "@/assets/data.json";

export default {
  name: "app",
  components: {
    AcademicFitReport
  },
  data: function() {
    return {
      athlete_info: AthleteData.data[0]
    };
  },
  methods: {
    updateName: function (name) {
      this.athlete_info = {
        ...this.athlete_info,
        name
      }
    }
  }
};
</script>

<style>
body * {
  font-family: 'Roboto',Helvetica,Arial,sans-serif;
}
</style>
