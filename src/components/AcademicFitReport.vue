<template>
  <div>
    <div class="info">
      <img :src="athlete.profile_image" :alt="`Profile picture of {{ athlete.name }}`" class="avatar" />
  
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
  </div>
</template>

<script>
export default {
  name: "AcademicFitReport",
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
.avatar {
  border-radius: 50%;
  height: 98px;
  width: 98px;
}

.athleteName {
  color: #00b4ff;
  font-size: 1rem;
  font-weight: bold;
  margin: 0;
}

.info {
  display: flex;
}

.infoRightSide {
  padding-left: 1rem;
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
  font-size: 0.75rem;
}

.statsList {
  list-style: none;
  padding-left: 0;
  margin: 0;
}

@media screen and (min-width: 768px) {
  .stats {
    display: flex;
    gap: 2rem;
  }
}
</style>