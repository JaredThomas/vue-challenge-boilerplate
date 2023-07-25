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
          <th scope="col" rowspan="2">School Name</th>
          <th scope="col" rowspan="2">Athletic Div</th>
          <th scope="col" rowspan="2">Conference</th>
          <th scope="col" rowspan="2">Ranking*<div class="tableHeaderSupplementalInfo">(DI NCAA)<br />(DII & DIII Hero Sports)</div></th>
          <th scope="colgroup" colspan="5">GPA**</th>
          <th scope="col" rowspan="2">SAT Reading***<br />25%-75%</th>
          <th scope="col" rowspan="2">SAT Math***<br />25%-75%</th>
          <th scope="col" rowspan="2">ACT Composite***<br />25%-75%</th>
        </tr>
        <tr>
          <th scope="col">Min</th>
          <th scope="col">25%</th>
          <th scope="col">50%</th>
          <th scope="col">75%</th>
          <th scope="col">Max</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="record in athlete.report" :key="record.school">
          <td class="schoolNameColumn">{{ record.school }}</td>
          <td :class="['athleticDivisionColumn', 'centeredColumnData']">{{ record.division }}</td>
          <td class="conferenceColumn">{{ record.conference }}</td>
          <td :class="['rankingColumn', 'centeredColumnData']">{{ record.ranking }}</td>
          <td :class="['gpaColumn', 'centeredColumnData']">{{ record.gpa.min.toFixed(2) }}</td>
          <td :class="['gpaColumn', 'centeredColumnData']">{{ record.gpa['25%'].toFixed(2) }}</td>
          <td :class="['gpaColumn', 'centeredColumnData']">{{ record.gpa['50%'].toFixed(2) }}</td>
          <td :class="['gpaColumn', 'centeredColumnData']">{{ record.gpa['75%'].toFixed(2) }}</td>
          <td :class="['gpaColumn', 'centeredColumnData']">{{ record.gpa.max.toFixed(2) }}</td>
          <td :class="['testResultColumn', 'centeredColumnData']">{{ record.sat.reading.min !== 'N/A' && record.sat.reading.max !== 'N/A' ? `${record.sat.reading.min}-${record.sat.reading.max}` : 'Not Reported' }}</td>
          <td :class="['testResultColumn', 'centeredColumnData']">{{ record.sat.math.min !== 'N/A' && record.sat.math.max !== 'N/A'  ? `${record.sat.math.min}-${record.sat.math.max}` : 'Not Reported' }}</td>
          <td :class="['testResultColumn', 'centeredColumnData']">{{ record.act.min !== 'N/A' && record.act.max !== 'N/A' ? `${record.act.min}-${record.act.max}` : 'Not Reported' }}</td>
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

thead tr th,
thead tr td {
  background-color: #222222;
  color: #FFFFFF;
  font-size: 0.75rem;
  font-weight: bold;
  vertical-align: middle;
}

.tableHeaderSupplementalInfo {
  font-weight: 400;
  font-size: 0.65rem;
}

table {
  border-spacing: 0;
  margin-top: 2rem;
}

tbody td {
  color: #222222;
  font-size: 0.75rem;
  font-weight: 400;
  padding: 0.5rem 0.25rem;
}

tbody tr:nth-child(even) {
  background-color: #e8f0fe;
}

.athleticDivisionColumn {
  text-align: 90px;
}

.centeredColumnData {
  text-align: center;
}

.conferenceColumn {
  width: 300px;
}

.gpaColumn {
  width: 36px;
}

.testResultColumn {
  width: 120px;
}

.rankingColumn {
  width: 130px;
}

.schoolNameColumn {
  width: 250px;
}

@media screen and (min-width: 768px) {
  .stats {
    display: flex;
    gap: 2rem;
  }
}
</style>