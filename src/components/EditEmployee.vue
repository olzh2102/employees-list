<template>
  <div id="edit-employee">
    <h3>Edit Employee</h3>
    <div class="row">
      <form @submit.prevent="updateEmployee" class="col s12">
        <div class="row">
          <div class="field col s12">
            <label>Employee ID#</label>
            <input disabled type="text" v-model="employee_id" required>
          </div>
          <div class="field col s12">
            <label>Name</label>
            <input type="text" v-model="name" required>
          </div>
          <div class="field col s12">
            <label>Department</label>
            <input type="text" v-model="dept" required>
          </div>
          <div class="field col s12">
            <label>Position</label>
            <input type="text" v-model="position" required>
          </div>
          <div class="field col s12">
            <button type="submit" class="btn">Submit</button>
            <router-link to="/" class="btn red">Cancel</router-link>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import db from '@/components/firebaseInit'

export default {
  name: 'edit-employee',
  data() {
    return {
      employee_id: null,
      name: null,
      dept: null,
      position: null
    }
  },
  beforeRouteEnter(to, from, next) {
    db.collection('employees').where('employee_id', '==', to.params.employee_id).get().then((snapshot) => {
      snapshot.forEach((doc) => {
        next(vm => {
          vm.employee_id = doc.data().employee_id
          vm.name = doc.data().name
          vm.dept = doc.data().dept
          vm.position = doc.data().position
        })
      })
    })
  },
  watch: {
    '$route': 'fetchData'
  },
  methods: {
    fetchData() {
      db.collection('employees').where('employee_id', '==', this.$route.params.employee_id).get().then((snapshot) => {
        snapshot.forEach((doc) => {
          this.employee_id = doc.data().employee_id
          this.name = doc.data().name
          this.dept = doc.data().dept
          this.position = doc.data().position
        })
      })
    },
    updateEmployee() {
      db.collection('employees').where('employee_id', '==', this.$route.params.employee_id).get().then((snapshot) => {
        snapshot.forEach((doc) => {
          doc.ref.update({
            employee_id: this.employee_id,
            name: this.name,
            dept: this.dept,
            position: this.position
          }).then(() => {
            this.$router.push({ name: 'ViewEmployee', params: { employee_id: this.employee_id } })
          })
        })
      })
    }
  }
    
}
</script>

<style>

</style>