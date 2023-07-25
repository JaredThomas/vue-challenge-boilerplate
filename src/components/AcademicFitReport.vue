<template>
  <div class="container">
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

    <table>
      <thead>
        <tr>
          <th scope="col">School Name</th>
          <th scope="col">Athletic Div</th>
          <th scope="col">Conference</th>
          <th scope="col">Ranking*</th>
          <th scope="colgroup" colspan="5">GPA**</th>
          <th scope="col">SAT Reading***</th>
          <th scope="col">SAT Math***</th>
          <th scope="col">ACT Composite***</th>
        </tr>
        <tr>
          <td colspan="3" />
          <th scope="col">(DI NCAA)<br />(DII & DIII Hero Sports)</th>
          <th scope="col">Min</th>
          <th scope="col">25%</th>
          <th scope="col">50%</th>
          <th scope="col">75%</th>
          <th scope="col">Max</th>
          <th scope="col">25%-75%</th>
          <th scope="col">25%-75%</th>
          <th scope="col">25%-75%</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="record in athlete.report" :key="record.school">
          <td>{{ record.school }}</td>
          <td>{{ record.division }}</td>
          <td>{{ record.conference }}</td>
          <td>{{ record.ranking }}</td>
          <td>{{ record.gpa.min.toFixed(2) }}</td>
          <td>{{ record.gpa['25%'].toFixed(2) }}</td>
          <td>{{ record.gpa['50%'].toFixed(2) }}</td>
          <td>{{ record.gpa['75%'].toFixed(2) }}</td>
          <td>{{ record.gpa.max.toFixed(2) }}</td>
          <td>{{ record.sat.reading.min !== 'N/A' && record.sat.reading.max !== 'N/A' ? `${record.sat.reading.min}-${record.sat.reading.max}` : 'Not Reported' }}</td>
          <td>{{ record.sat.math.min !== 'N/A' && record.sat.math.max !== 'N/A'  ? `${record.sat.math.min}-${record.sat.math.max}` : 'Not Reported' }}</td>
          <td>{{ record.act.min !== 'N/A' && record.act.max !== 'N/A' ? `${record.act.min}-${record.act.max}` : 'Not Reported' }}</td>
        </tr>
      </tbody>
    </table>
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
  padding-top: 0.25rem;
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

thead tr th,
thead tr td {
  background-color: #222222;
  color: #FFFFFF;
  font-size: 0.75rem;
}

table {
  border-spacing: 0;
  margin-top: 2rem;
}

tbody td {
  color: #222222;
  font-size: 0.75rem;
  font-weight: 400;
}

@media screen and (min-width: 768px) {
  .stats {
    display: flex;
    gap: 2rem;
  }
}
</style>