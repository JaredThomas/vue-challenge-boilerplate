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
            <ReportTableRow v-for="(record, index) in report" :key="record.school" :record="record" :is-row-highlighted="(index + 1) % 2 === 0" :athlete-gpa="athleteGpa" />
        </tbody>
    </table>
</template>

<script>
import ReportTableRow from './ReportTableRow.vue';

export default {
  name: "ReportTable",
  components: {
    ReportTableRow
  },
  props: {
    athleteGpa: Number,
    report: {
      type: Array
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

table thead tr:first-child th:first-child {
  left: 0;
  position: sticky;
  top: 0;
  z-index: 2;
}
</style>