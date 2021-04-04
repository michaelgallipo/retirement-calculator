<template>
	<div class="calculator">
		<h1>Please Enter Data to Calculate How Long Your Money Will Last</h1>
		<div id="dataEntry">
			<div class="form-group row">
				<label class="col-sm-2 col-form-label">Current Age</label>
				<div class="col-sm-3">
					<input
						type="number"
						class="form-control"
						v-model="age"
						placeholder="Enter age"
						maxlength="2"
					/>
				</div>
			</div>
			<div class="form-group row">
				<label class="col-sm-2 col-form-label">Retirement Age</label>
				<div class="col-sm-3">
					<input
						type="number"
						class="form-control"
						v-model="retirementAge"
						placeholder="Desired Retirement Age"
						maxlength="2"
					/>
				</div>
			</div>
			<div class="form-group row">
				<label class="col-sm-2 col-form-label">Assets</label>
				<div class="col-sm-3">
					<input
						type="number"
						class="form-control"
						v-model="assets"
						placeholder="Starting Assets"
						maxlength="10"
					/>
				</div>
			</div>
			<div class="form-group row">
				<label class="col-sm-2 col-form-label">Savings</label>
				<div class="col-sm-3">
					<input
						type="number"
						class="form-control"
						v-model="assets"
						placeholder="Additional Annual Savings"
						maxlength="10"
					/>
				</div>
			</div>
			<div class="form-group row">
				<label class="col-sm-2 col-form-label">Spending</label>
				<div class="col-sm-3">
					<input
						type="number"
						class="form-control"
						v-model="assets"
						placeholder="Annual Spending at Retirement"
						maxlength="10"
					/>
				</div>
			</div>
			<button id="calculate" type="submit" class="btn btn-primary">
				Calculate
			</button>
		</div>
	</div>
</template>

<script>
export default {
	name: "Calculator",
	props: {},
	data: function() {
		return {
			age: "",
			retirementAge: "",
			assets: "",
			addSavings: "",
			spending: "",
			taxRate: 0.2,
			equityReturn: 0.095,
			bondReturn: 0.04,
			errors: [],
		};
	},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
	margin-top: 75px;
	padding-left: 30px;
}
h3 {
	margin: 40px 0 0;
}

label {
	text-align: left;
}

#dataEntry {
	padding-top: 20px;
}

#calculate {
	margin-top: 15px;
}
</style>
