<template>
    <div class="modalDialog">
        <div class="modalHeading">Edit Name</div>
        <form @submit.prevent="onSubmit(editableName)" class="modalForm">
            <div class="formContent">
                <input type="text" v-model="editableName" />
            </div>
            <div class="formFooter">
                <button type="button" @click="close" class="cancelButton">Cancel</button>
                <button type="submit" class="saveButton">Save</button>
            </div>
        </form>
    </div>
</template>

<script>
export default {
    name: 'EditNameModal',
    props: {
        close: {
            type: Function,
            required: true
        },
        initialName: {
            type: String,
            required: true
        },
        onSubmit: {
            type: Function,
            required: true
        }
    },
    
    data: function () {
        return {
            editableName: ''
        }
    },

    created: function () {
        this.editableName = this.initialName;
    }
}
</script>

<style scoped>
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
</style>