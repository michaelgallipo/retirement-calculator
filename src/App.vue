<template>
	<div id="app">
		<header>
			<img
				class="headerImage"
				id="leftImage"
				alt="Hippo logo"
				src="./assets/images/hippo.jpg"
			/>
			<p class="title">Internet Hippo's Retirement Calculator</p>
			<img
				class="headerImage"
				id="rightImage"
				alt="Hippo logo"
				src="./assets/images/hippo.jpg"
			/>
		</header>
		<Calculator />
	</div>
</template>

<script>
import Calculator from "./components/Calculator.vue";

export default {
	name: "app",
	components: {
		Calculator,
	},
};
</script>

<style>
#app {
	font-family: "Avenir", Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}

.headerImage {
	width: 150px;
	height: 150px;
	position: absolute;
	padding: 20px;
}
#leftImage {
	top: 0px;
	left: 0px;
}
#rightImage {
	top: 0px;
	right: 0px;
}

.title {
	font-size: 46px;
	font-weight: bold;
	text-align: center;
	font-family: cursive;
}

@media screen and (max-width: 950px) {
	.headerImage {
		position: relative;
	}
	#rightImage {
		display: none;
	}
}
</style>
