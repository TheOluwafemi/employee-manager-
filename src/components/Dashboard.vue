<template>

	<div id="dashboard">

		<ul class="collection with-header">
			<li class="collection-header"><h4>Employees</h4>
			</li>
			<li v-for='employee in employees' v-bind:key='employees.id' class="collectio-item">
				{{employee.Name}}
			</li>
		</ul>

		<div class="fixed-action-btn">
			<router-link to="/new" class="btn-floating btn-large red">
				<i class="fa fa-plus"></i>
			</router-link> 
		</div>
	</div>

</template>

<script>
	import db from './firebaseInit'
	export default {
		name:'dashboard',
		data() {
			return {
				employees: []
			}
		},
		created () {
			db.collection('Employees').get().then
			(querySnapshot => {
				querySnapshot.forEach(doc => {
					console.log(doc.data());
					const data = {
						'id': doc.id,
						'employee_id': doc.data().employee_id,
						'name': doc.data().Name,
						'dept': doc.data().Dept,
						'position': doc.data().Position,
					}
					this.employees.push(data)
					
				})
			})
		}
	}

</script>
