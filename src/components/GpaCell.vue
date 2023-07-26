<template>
    <td class="gpaColumn" :style="{backgroundColor: relativeGpaBackgroundColor}">{{ gpa.toFixed(2) }}</td>
</template>

<script>
export default {
    name: 'GpaCell',
    props: {
        athleteGpa: Number,
        gpa: Number
    },
    computed: {
        // returns a conditional cell background color based on the relative difference between the athlete's GPA and the school's GPA
        relativeGpaBackgroundColor: function () {
            const diff = this.gpa - this.athleteGpa;
            if (diff > 0.1) {
                return '#d7737d'
            }
            if (diff > 0 ) {
                return '#c194b5'
            }
            if (diff === 0) {
                return '#b4a7d6'
            }
            if (diff >= -0.1) {
                return '#a6a8da'
            }
            return '#75ace5';
        }
    }
}
</script>

<style scoped>
.gpaColumn {
  text-align: center;
  width: 36px;
}</style>