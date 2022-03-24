<script>
	let months = ["Jan", "Feb", "Mar", "Apr", "Maj", "Jun", "Jul", "Aug", "Sep", "Okt", "Nov", "Dec"]
	let months_length = [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
	let weeks = ["M", "T", "O", "T", "F", "L", "S"]
	let lengths = {}

	init();
	
	function init() {
		for(var i = 0; i < months.length; i++) {
			lengths[months[i]] = []
			for(var j = 0; j < months_length[i]; j++) {
				lengths[months[i]].push(0);
			}
		}
	}

	function get_time(index) {
		var date = new Date();
		let time = new Date(date.getFullYear(), index, 1).getDay();
		let array = []
		for(var i = 0; i < time; i++) {
			array.push(i);
		}
		return array;
	}

	function get_day() {
		var date = new Date();
		// console.log(date.getDate());
		return date.getDate()
	}

	function get_month() {
		var date = new Date();
		// console.log(date.getDate());
		return date.getMonth()
	}

	function get_week_day() {
		var date = new Date();
		// console.log(date.getDate());
		return date.getDay()
	}

</script>

<main>
	2022
	<div class="months">
		{#each months as month, month_i}
			<div>
				{#if month_i == get_month()}
					<div>
						<div class="selected monthtag">
							{month}
						</div>
					</div>
				{:else}
					<div>
						{month}
					</div>
				{/if}
				<span class="days">
					{#each get_time(month_i) as i} 
						<div class="day">
							
						</div>
					{/each}
					{#each lengths[month] as day, i}
						{#if i == get_day() - 1 && month_i == get_month()}
							<div class="day selected">
								{i + 1}
							</div>
						{:else}
							<div class="day">
								{i + 1}
							</div>
						{/if}
					{/each}
				</span>
			</div>
		{/each}
	</div>
	<div class="weeks">
		{#each [0, 1, 2, 3, 4] as i} 
			{#each weeks as week, week_i}
				{#if week_i == get_week_day() && i == parseInt(get_day() / 5) - 1} 
					<div class="selected">
						{week}
					</div>
				{:else}
					<div>
						{week}
					</div>
				{/if}
			{/each}
		{/each}
		<div>
			M
		</div>
		<div>
			T
		</div>
	</div>
</main>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');
	main {
		font-family: 'Roboto', sans-serif;
		font-size: 30px;
		padding-left: 120px;
		padding-top: 40px;
	}

	.months {
		display: flex;
		flex-direction: column;
		gap: 30px;
		margin-top: 30px;
		font-weight: bold;
	}

	.weeks {
		position: absolute;
		display: flex;
		flex-direction: row;
		margin-left: 120px;
		gap: 40px;
		top: 48px;
		font-weight: bold;
	}

	.days {
		position: absolute;
		display: flex;
		flex-direction: row;
		left: 250px;
		flex-basis: 20px;
		gap: 24px;
		margin-top: -36px;
		font-weight: normal;
	}
	
	.day {
		width: 35px;
	}

	.selected {
		background-color: black;
		color: white;
	}

	.monthtag {
		width: max-content;
	}
</style>