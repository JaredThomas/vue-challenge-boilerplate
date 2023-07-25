<template>
    <tr :class="{highlightRow: isRowHighlighted}">
        <th class="schoolNameColumn">{{ record.school }}</th>
        <td :class="['athleticDivisionColumn', 'centeredColumnData']">{{ record.division }}</td>
        <td class="conferenceColumn">{{ record.conference }}</td>
        <td :class="['rankingColumn', 'centeredColumnData']">{{ record.ranking }}</td>
        <GpaCell :gpa="record.gpa.min" :athlete-gpa="athleteGpa" />
        <GpaCell :gpa="record.gpa['25%']" :athlete-gpa="athleteGpa" />
        <GpaCell :gpa="record.gpa['50%']" :athlete-gpa="athleteGpa" />
        <GpaCell :gpa="record.gpa['75%']" :athlete-gpa="athleteGpa" />
        <GpaCell :gpa="record.gpa.max" :athlete-gpa="athleteGpa" />
        <td :class="['testResultColumn', 'centeredColumnData']">{{ record.sat.reading.min !== 'N/A' && record.sat.reading.max !== 'N/A' ? `${record.sat.reading.min}-${record.sat.reading.max}` : 'Not Reported' }}</td>
        <td :class="['testResultColumn', 'centeredColumnData']">{{ record.sat.math.min !== 'N/A' && record.sat.math.max !== 'N/A'  ? `${record.sat.math.min}-${record.sat.math.max}` : 'Not Reported' }}</td>
        <td :class="['testResultColumn', 'centeredColumnData']">{{ record.act.min !== 'N/A' && record.act.max !== 'N/A' ? `${record.act.min}-${record.act.max}` : 'Not Reported' }}</td>
    </tr>
</template>

<script>
import GpaCell from './GpaCell.vue';

export default {
    name: 'ReportTableRow',
    components: {
        GpaCell
    },
    props: {
        athleteGpa: Number,
        isRowHighlighted: Boolean,
        record: Object
    }
}
</script>

<style scoped>
.highlightRow td,
.highlightRow th {
    background-color: #e8f0fe;
}

th {
  left: 0;
  position: sticky;
  top: 0;
  z-index: 2;
}

td,
th {
  background-color: #FFFFFF;
  color: #222222;
  font-size: 0.75rem;
  font-weight: 400;
  padding: 0.5rem 0.25rem;
  text-align: left;
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