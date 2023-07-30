<template>
  <div class="container">
    <div class="header">
    <div class="info">
      <Avatar :athlete-name="athlete.name" :image-url="athlete.profile_image" />
  
      <div class="infoRightSide">
        <div class="editableName">
          <h2 class="athleteName">{{athlete.name}}</h2>
          <button type="button" class="editButton">
            <img :src="editIcon" alt="Edit athlete name" @click="toggleModal(true)" />
          </button>
        </div>

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
    <div class="logoSection">
      <img :src="logoUrl" alt="Sports Recruits Insights logo" class="logo" />
      <h2 class="mainHeading">Academic Fit Report</h2>
    </div>
  </div>

    <div class="tableContainer">
      <ReportTable :report="athlete.report" :athlete-gpa="athlete.gpa" />
    </div>

    <ul class="footnotes">
      <li v-for="note in footnotes" :key="note" class="footnote">{{ note }}</li>
    </ul>

    <div v-if="isModalOpen" class="modal">
      <div class="modalDialog">
        <div class="modalHeading">Edit Name</div>
        <form @submit="handleClickSave" class="modalForm">
          <div class="formContent">
            <input type="text" v-model="editableName" />
          </div>
          <div class="formFooter">
            <button type="button" @click="toggleModal(false)" class="cancelButton">Cancel</button>
            <button type="submit" class="saveButton">Save</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import Avatar from './Avatar.vue';
import ReportTable from './ReportTable.vue';
import logoUrl from '../assets/SR_insights_logo.png';
import editIcon from '../assets/edit.svg';

export default {
  name: "AcademicFitReport",
  components: {
    Avatar,
    ReportTable
  },
  props: {
    athlete: {
      type: Object,
      required: true
    },
    updateName: {
      type: Function,
      required: true
    }
  },
  data: function () {
    return {
      editableName: '',
      editIcon,
      logoUrl,
      isModalOpen: false,
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
      ],
      footnotes: [
        '*Rankings for Division I schools based on NCAA data (www.ncaa.com) and rankings for Division II & III schools are based on data from Hero Sports (www.herosports.com/rankings)',
        '** GPA is based on SportsRecruits members who have shown interest in (favorited) the school and have provided their GPA on their profile',
        '***SAT and ACT scores based on national data provided by the National Center of Education Statistics- https://nces.ed.gov/ipeds/'
      ]
    }
  },

  created: function () {
    this.editableName = this.athlete.name
  },

  methods: {
      handleClickSave: function () {
        this.updateName(this.editableName)
        this.toggleModal(false);
      },
  
      toggleModal: function (visibility) {
        this.isModalOpen = visibility;
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
  display: flex;
  flex-direction: column;
  height: 100vh;
  padding: 1rem 1rem 2rem;
}

.editButton {
  border: none;
  background: none;
  cursor: pointer;
  height: 34px;
  width: 34px;
}

.editableName {
  align-items: center;
  display: flex;
}

.footnotes {
  padding-top: 1.5rem;
}

.footnote {
  font-size: 0.75rem;
}

.header {
  display: flex;
  flex-direction: column-reverse;
}

.info {
  display: flex;
  flex-direction: column;
}

.infoRightSide {
  padding-top: 2rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.logo {
  width: 220px;
}

.logoSection {
  padding-bottom: 2rem;
}

.mainHeading {
  font-size: 1.25rem;
}

.modalDialog {
  background-color: white;
  border-radius: 4px;
  box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
  display: flex;
  flex-direction: column;
  height: 200px;
  left: 50%;
  position: absolute;
  max-height: 100%;
  max-width: 100%;
  top: 50%;
  transform: translate(-50%, -50%);
  width: 300px;
  z-index: 4;
}

.modal::before {
  content: "";
  display: block;
  background: rgba(0, 0, 0, 0.6);
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 3;
}

.modalHeading {
  color: #00b4ff;
  font-size: 1rem;
  font-weight: bold;
  margin: 0;
  padding: 1rem 1rem 0;
}

.modalForm {
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}

.formContent {
  flex-grow: 1;
  padding: 1rem;
}

.formFooter {
  border-top: 1px solid #CCCCCC;
  display: flex;
  gap: 1rem;
  justify-content: flex-end;
  padding: 0.5rem 1rem;
}

.cancelButton {
  background: none;
  border: none;
  color: #00b4ff;
  cursor: pointer;
}

.cancelButton:hover {
  opacity: 0.9;
}

.saveButton {
  background-color: #00b4ff;
  border: none;
  border-radius: 4px;
  color: #FFFFFF;
  cursor: pointer;
  font-weight: bold;
  padding: 0.25rem 0.75rem;
}

.saveButton:hover {
  opacity: 0.9;
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
  flex-grow: 1;
  margin-top: 2rem;
  overflow: auto;
  width: 100%
}

@media screen and (min-width: 400px) {
  .info {
    flex-direction: row;
  }
  .infoRightSide {
    padding-left: 1rem;
    padding-top: 0;
  }
}

@media screen and (min-width: 768px) {
  .stats {
    display: flex;
    gap: 2rem;
  }
}

@media screen and (min-width: 820px) {
  .header {
    flex-direction: row;
    justify-content: space-between;
    align-items: flex-start;
  }

  .logoSection {
    text-align: right;
    padding-bottom: 0;
  }
}
</style>