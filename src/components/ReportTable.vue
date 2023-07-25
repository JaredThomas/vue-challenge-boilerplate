<template>
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
            <tr v-for="record in report" :key="record.school">
            <th class="schoolNameColumn">{{ record.school }}</th>
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
</template>

<script>
export default {
  name: "ReportTable",
  props: {
    report: {
      type: Object
    }
  }
};
</script>

<style scoped>
thead tr th,
thead tr td {
  background-color: #222222;
  color: #FFFFFF;
  font-size: 0.75rem;
  font-weight: bold;
  padding: 0.15rem 0;
  vertical-align: middle;
}

.tableHeaderSupplementalInfo {
  font-weight: 400;
  font-size: 0.65rem;
}

table {
  border-spacing: 0;
  width: 1400px;
  position: relative;
}

table thead {
  left: 0;
  position: sticky;
  top: 0;
  z-index: 3;
}

table tbody th:first-child,
table thead tr:first-child th:first-child {
  left: 0;
  position: sticky;
  top: 0;
  z-index: 2;
}

tbody td,
tbody th {
  background-color: #FFFFFF;
  color: #222222;
  font-size: 0.75rem;
  font-weight: 400;
  padding: 0.5rem 0.25rem;
  text-align: left;
}

tbody tr:nth-child(even) td,
tbody tr:nth-child(even) th {
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
</style>