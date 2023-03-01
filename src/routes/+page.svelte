<script>
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

<div class="main">

	<p>Since Midnight in the City of Brentwood, residents have used approximately <mark>{formatNum(Math.round(percent*bottles))} plastic water bottles</mark>.</p>
	<div class="statistics">
		<p><mark>{formatNum(12)}</mark> bottles/minute.</p>
		<p><mark>{formatNum(17280)}</mark> bottles/day.</p>
	</div>

	<!-- <h1>{Math.round(percent*bottles)} Bottles</h1>
	<p>Have been wasted in the past <mark>{today.getHours()}</mark> hours.</p> -->
</div>

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

	.main h1 {
		font-size: 100px;
		padding: 0;
		margin: 0;
	}
	.main p {
		font-size: 45px;
		padding: 0;
		margin: 0;
	}

	.statistics {
		margin-top: 45px;
	}

	@media (max-width: 768px) {

		.main h1 {
			font-size: 50px;
		}
		.main p {
			font-size: 20px;
		}

	}

</style>