<template>
  <div class="container">
    <div class="info">
      <Avatar :athlete-name="athlete.name" :image-url="athlete.profile_image" />
  
      <div class="infoRightSide">
        <h2 class="athleteName">{{athlete.name}}</h2>

        <div class="stats">
          <ul class="statsList">
            <li v-for="stat in stats" :key="stat.label" class="stat">
              <label class="statLabel">{{ stat.label }}:</label>
              {{ stat.value }}
            </li>
          </ul>

          <ul class="statsList">
            <li v-for="stat in additionalStats" :key="stat.label" class="stat">
              <label class="statLabel">{{ stat.label }}:</label>
              {{ stat.value }}
            </li>
          </ul>
        </div>
      </div>
    </div>

    <div class="tableContainer">
      <ReportTable :report="athlete.report" :athlete-gpa="athlete.gpa" />
    </div>

  </div>
</template>

<script>
import Avatar from './Avatar.vue';
import ReportTable from './ReportTable.vue';

export default {
  name: "AcademicFitReport",
  components: {
    Avatar,
    ReportTable
  },
  props: {
    athlete: {
      type: Object,
      required: false
    }
  },
  data: function () {
    return {
      stats: [
        {
          label: 'Sport',
          value: this.athlete.sport
        },
        {
          label: 'Class',
          value: this.athlete.grad_year
        },
        {
          label: 'Club',
          value: this.athlete.club.name
        }
      ],
      additionalStats: [
        {
          label: 'High School',
          value: this.athlete.high_school.name
        },
        {
          label: 'GPA',
          value: this.athlete.gpa
        },
        {
          label: 'Desired Major',
          value: this.athlete.major
        }
      ]
    }
  }
}
</script>

<style scoped>

.athleteName {
  color: #00b4ff;
  font-size: 1.5rem;
  font-weight: bold;
  margin: 0;
}

.container {
  border-bottom: 8px solid #00b4ff;
  border-top: 8px solid #00b4ff;
  padding: 1rem 1rem 2rem;
}

.info {
  display: flex;
}

.infoRightSide {
  padding-left: 1rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.statLabel {
  font-weight: bold;
}

.stats {
  display: block;
}

.stat {
  padding-top: 0.5rem;
}

.stat, .statLabel {
  color: #222222;
  font-size: 1rem;
}

.statsList {
  list-style: none;
  padding-left: 0;
  margin: 0;
}

.tableContainer {
  margin-top: 2rem;
  max-height: 300px;
  overflow: auto;
  width: 100%
}

@media screen and (min-width: 768px) {
  .stats {
    display: flex;
    gap: 2rem;
  }
}
</style>