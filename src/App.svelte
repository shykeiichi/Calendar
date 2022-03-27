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
		time -= 1;
		if(time == -1) {
			time = 6;
		}

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

	function get_year() {
		var date = new Date();
		// console.log(date.getDate());
		return date.getFullYear()
	}

	function get_week_day() {
		var date = new Date();
		// console.log(date.getDate());
		return date.getDay()
	}

	function get_week_day_long(year, month, day) {
		var date = new Date(year, month, day);
		// console.log(date.getDate());
		return date.getDay()
	}

	function get_weekdays() {
		var list = []
		var day = 0;
		for(var i = 0; i < 37; i++) {
			day += 1;
			if(day == 8) {
				day = 1;
			}
			switch(day) {
				case 1: list.push("M"); break;
				case 2: list.push("T"); break;
				case 3: list.push("O"); break;
				case 4: list.push("T"); break;
				case 5: list.push("F"); break;
				case 6: list.push("L"); break;
				case 7: list.push("S"); break;
			}
		}
		return list
	}

	function get_hours() {
		let arr =[]
		for(var i = 0; i < 24; i++) {
			arr.push(i)
		}
		return arr;
	}

	function get_hour() {
		let date = new Date();
		return date.getHours()
	}

	function get_minutes() {
		let arr =[]
		for(var i = 0; i < 60; i++) {
			arr.push(i)
		}
		return arr;
	}

	function get_minute() {
		let date = new Date();
		return date.getMinutes()
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
						{#if get_week_day_long(get_year(), month_i, i) != 5 && get_week_day_long(get_year(), month_i, i) != 6}
							{#if i == get_day() - 1 && month_i == get_month()}
								<div class="day selected">
									{i + 1}
								</div>
							{:else}
								<div class="day">
									{i + 1}
								</div>
							{/if}
						{:else}
							{#if i == get_day() - 1 && month_i == get_month()}
								<div class="day selected weekend">
									{i + 1}
								</div>
							{:else}
								<div class="day weekend">
									{i + 1}
								</div>
							{/if}
						{/if}
					{/each}
				</span>
			</div>
		{/each}
	</div>
	<div class="weeks">
		<!-- {#each [1, 2, 3, 4, 5] as i} 
			{#each weeks as week, week_i}
				{console.log(week_i + (5 * (i - 1)))}
				{#if week_i + 1 == get_week_day()} 
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
		</div> -->
		{#each get_weekdays() as day, i}
			{#if i == get_day()}
				<div class="selected">
					{day}
				</div>
			{:else}
				<div>
					{day}
				</div>
			{/if}
		{/each}
	</div>
</main>

<time>
	<div class="time">
		<div>	
			Hrs
		</div>
		<div>
			Min
		</div>	
		<div class="hss">
			{#each get_hours() as hour} 
				{#if get_hour() != hour}
					<div class="hs">
						{hour}
					</div>
				{:else}
					<div class="hs selected">
						{hour}
					</div>
				{/if}
			{/each}
		</div>
		<div class="mss">
			{#each get_minutes() as hour} 
				{#if get_minute() != hour}
					<div class="hs">
						{hour}
					</div>
				{:else}
					<div class="hs selected">
						{hour}
					</div>
				{/if}
			{/each}
		</div>
	</div>
</time>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');
	main {
		font-family: 'Roboto', sans-serif;
		font-size: 30px;
		padding-left: 120px;
		padding-top: 40px;
		background-color: white;
	}
	
	time {
		position: absolute;
		font-family: 'Roboto', sans-serif;
		font-size: 30px;
		padding-left: 120px;
		top:1000px;
	}

	.hss {
		position: absolute;
		display: flex;
		flex-direction: row;
		left: 250px;
		flex-basis: 20px;
		gap: 24px;
		font-weight: normal;
	}

	.mss {
		position: absolute;
		display: flex;
		flex-direction: row;
		left: 250px;
		flex-basis: 20px;
		gap: 24px;
		font-weight: normal;
		top: 70px;
		width: 1800px;
		height: 100px;
		flex-wrap: wrap;
	}
	
	.hs {
		width: 35px;
		height: max-content;
	}

	.time {
		display: flex;
		flex-direction: column;
		gap: 30px;
		font-weight: bold;
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
		left: 245px;
		flex-basis: 20px;
		gap: 24px;
		margin-top: -36px;
		font-weight: normal;
	}
	
	.day {
		width: 35px;
		text-align: center;
	}

	.selected {
		background-color: black;
		color: white;
	}

	.monthtag {
		width: max-content;
	}

	.weekend {
		color: lightgray;
	}
</style>