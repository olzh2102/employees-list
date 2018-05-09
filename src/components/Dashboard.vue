<template>
  <div id="dashboard">
    <ul class="collection with-header">
      <li class="collection-header"><h4>Employees</h4></li>
      <li v-for="employee in employees" :key="employee.id" class="collection-item">
        <span class="chip">{{ employee.dept }}</span>
        {{ employee.employee_id}}: {{ employee.name }}

        <router-link class="secondary-content" :to="{ name: 'ViewEmployee', params: { employee_id: employee.employee_id }}">
          <i class="material-icons">account_box</i>
        </router-link>
      </li>
    </ul>
  </div>
</template>

<script>
import db from '@/components/firebaseInit'

export default {
  name: 'Dashboard',
  data() {
    return {
      employees: []
    }
  },
  created() {
    db.collection('employees').orderBy('dept').get().then(snapshot => {
      snapshot.forEach(doc => {
        const data = {
          'id': doc.id,
          'employee_id': doc.data().employee_id,
          'name': doc.data().name,
          'dept': doc.data().dept,
          'position': doc.data().position
        }

        this.employees.push(data)
      })
    })
  }
}
</script>

<style>

</style>


