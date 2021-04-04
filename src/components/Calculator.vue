<template>
	<div class="calculator">
		<h1>Please Enter Data to Calculate How Long Your Money Will Last</h1>
		<h2 id="finalMessage">{{ this.finalMessage }}</h2>
		<div class="row" id="display">
			<div id="dataEntry" class="col-sm-5">
				<div class="form-group row">
					<label class="col-sm-3 col-form-label">Current Age</label>
					<div class="col-sm-9">
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
					<label class="col-sm-3 col-form-label">Retirement Age</label>
					<div class="col-sm-9">
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
					<label class="col-sm-3 col-form-label">Assets</label>
					<div class="col-sm-9">
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
					<label class="col-sm-3 col-form-label">Savings</label>
					<div class="col-sm-9">
						<input
							type="number"
							class="form-control"
							v-model="addSavings"
							placeholder="Additional Annual Savings"
							maxlength="10"
						/>
					</div>
				</div>
				<div class="form-group row">
					<label class="col-sm-3 col-form-label">Spending</label>
					<div class="col-sm-9">
						<input
							type="number"
							class="form-control"
							v-model="spending"
							placeholder="Annual Spending at Retirement"
							maxlength="10"
						/>
					</div>
				</div>
				<button id="calculate" v-on:click="submit" class="btn btn-primary">
					Calculate
				</button>
				<button id="reset" v-on:click="reset" class="btn btn-warning">
					Reset
				</button>
			</div>
			<div class="col-sm-6 offset-sm-1" id="caveats">
				<h5>Assumptions and Caveats</h5>
				<ul id="caveatList">
					<li>
						Return based on constant annual returns. Less accurate than a full
						Monte Carlo simulation
					</li>
					<li>
						Annual savings added after return calculation for that given year
					</li>
					<li>
						Tax rate calculated at flat 20%. Your personal tax situation may be
						different
					</li>
					<li>Spending deducted at the start of a given year</li>
					<li>
						Stock/Bond allocation fixed at 50/50 mix for duration of
						calculation. Most likely you would want that allocation to change
						over time
					</li>
					<li>
						Equity return calculated at 9.5%/year (long term stock market
						average) and bond return calculated at 4%.
					</li>
				</ul>
			</div>
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
			bondPct: 0.5,
			equityPct: 0.5,
			finalMessage: "",
			moneyAge: 65,
			errors: [],
		};
	},
	methods: {
		submit: function() {
			this.calculateNestEgg();
			this.yearsOfMoney();
		},
		calculateNestEgg: function() {
			console.log(this.assets);
			let years = this.retirementAge - this.age;
			console.log(years, this.addSavings);
			let x;
			for (x = 0; x < years; x++) {
				let newTotal =
					this.assets * this.equityPct * (1 + this.equityReturn) +
					this.assets * this.bondPct * (1 + this.bondReturn) +
					parseInt(this.addSavings);
				console.log(newTotal);
				this.assets = newTotal;
			}
			return this.assets;
		},
		yearsOfMoney: function() {
			this.moneyAge = this.retirementAge;
			console.log(this.moneyAge);
			while (this.assets > 0) {
				this.assets = this.assets - this.spending / (1 - this.taxRate);
				// console.log(this.assets);
				let newTotal =
					this.assets * this.equityPct * (1 + this.equityReturn) +
					this.assets * this.bondPct * (1 + this.bondReturn);
				this.moneyAge++;
				this.assets = newTotal;
				console.log(this.assets, this.moneyAge);
				if (this.moneyAge > 99) {
					console.log("you have enough money", this.assets);
					this.finalMessage =
						"Congratulations! Your money should last until at least age 100";
					return this.finalMessage;
				}
			}
			console.log(this.moneyAge);
			this.finalMessage =
				"Based on the information given, you will run out of money at age " +
				this.moneyAge;
			return this.finalMessage;
		},
		reset: function() {
			this.assets = "";
			this.retirementAge = "";
			this.addSavings = "";
			this.spending = "";
			this.age = "";
			this.retirementAge = "";
			this.finalMessage = "";
		},
	},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculator {
	margin-top: 60px;
	padding-left: 30px;
}

label {
	text-align: left;
}

#dataEntry {
	padding-top: 20px;
}

#caveats {
	border: 3px;
	border-style: solid;
	padding-top: 20px;
}
#display {
	margin-top: 20px;
	margin-left: 10px;
	margin-right: 10px;
}
#caveatList {
	text-align: left;
	font-size: 18px;
}
#finalMessage {
	color: navy;
}
#reset {
	margin-left: 40px;
}

@media screen and (max-width: 950px) {
	h1 {
		font-size: 26px;
	}
}
</style>
