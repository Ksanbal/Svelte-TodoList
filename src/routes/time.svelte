<script lang="ts">
	let now: Date;
	const month: string[] = [
		'January',
		'February',
		'March',
		'April',
		'May',
		'June',
		'July',
		'August',
		'September',
		'October',
		'November',
		'December'
	];
	const week: string[] = ['일', '월', '화', '수', '목', '금', '토'];

	function clock() {
		now = new Date();
	}
	clock();
	setInterval(clock, 1000);
</script>

<div class="top">
	<!-- 날짜 -->
	<span class="date">
		<span>{now.getDate()}</span>

		<small>
			{month[now.getMonth()]}<br />
			{now.getFullYear()}
		</small>
	</span>
	<!-- 시간 -->
	<span class="clock">
		{now.getHours()}:{now.getMinutes()}:{now.getSeconds()}
	</span>
</div>

<style>
	.top {
		border-radius: 1rem 1rem 0 0;
		padding: 5rem 2rem;
		background-color: #6393da;
		color: white;
		font-size: 2rem;
		text-align: center;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
	.date {
		font-size: 3rem;
	}
	.clock {
		opacity: 0.3;
	}
	.date > small {
		font-size: 1rem;
		display: inline-block;
	}
</style>
