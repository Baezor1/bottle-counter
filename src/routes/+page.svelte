<script>
	import Fullscreen from "svelte-fullscreen";
	
	var today = new Date()
	var start = new Date(today.getFullYear(), today.getMonth(), today.getDate(), 0, 0, 0)
	var seconds = Math.round((today-start)/1000)
	var bottles = Math.floor(seconds/5)
	var percent = 0.1
	var milis = 10

	function updateTime() {
		today = new Date()
		seconds = Math.round((today-start)/1000)
		bottles = Math.round(seconds/5)
		setTimeout(updateTime, 1000)
	}

	function countUp() {
		percent = percent+0.03
		milis = milis+5
		if (percent < 1) {
			setTimeout(countUp, milis)
		} else {
			percent = 1
		}
	}

	function formatNum(x) {
		return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ",");
	}

	updateTime()
	countUp()

</script>

<Fullscreen let:onRequest let:onExit>
	<div class="main">

		<p>Since Midnight in the City of Brentwood, residents have used approximately <mark>{formatNum(Math.round(percent*bottles))} plastic water bottles</mark>.</p>
		<div class="statistics">
			<p><mark>{formatNum(12)}</mark> bottles/minute.</p>
			<p><mark>{formatNum(17280)}</mark> bottles/day.</p>
		</div>
	</div>
	<div class="fullscreen-button">
		<button on:click={() => onRequest()}>Enter Fullscreen</button>
	</div>
</Fullscreen>
<style>
	.main {
		width: 100vw;
		height: 100vh;
		background-color: cadetblue;
		display: flex;
		align-items: center;
		justify-content: center;
		text-align: center;
		flex-direction: column;
	}

	.main p {
		font-size: 45px;
		padding: 0;
		margin: 0;
	}

	.statistics {
		margin-top: 45px;
	}

	.fullscreen-button {
		position: fixed;
		bottom: 20px;
		right: 20px;
	}

	@media (max-width: 768px) {

		.main p {
			font-size: 30px;
		}

		.fullscreen-button {
			visibility: hidden;
		}

	}

</style>