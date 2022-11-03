<script>
	const dots = [0, 1, 2, 3, 4];
	const colors = ['red', 'yellow', 'blue', 'green'];
	const directions = ['up', 'down', 'right', 'left'];
	const rules = ['direction', 'dots', 'color'];

	let rule1;
	let rule2;
	let score = 0;
	const newTriangle = {};
	const previousTriangle = {};

	const ruleCreator = () => {
		// const rule = rules[Math.floor(Math.random() * rules.length)];
		rule1 = rules[Math.floor(Math.random() * rules.length)];
		rule2 = rules[Math.floor(Math.random() * rules.length)];
	};

	while (rule1 === rule2) {
		ruleCreator();
	}

	const triangleCreator = () => {
		newTriangle.dots = dots[Math.floor(Math.random() * dots.length)];
		newTriangle.color = colors[Math.floor(Math.random() * colors.length)];
		newTriangle.direction = directions[Math.floor(Math.random() * directions.length)];
		console.log(newTriangle);
	};

	triangleCreator();

	const setPreviousTriangle = () => {
		previousTriangle.dots = newTriangle.dots;
		previousTriangle.color = newTriangle.color;
		previousTriangle.direction = newTriangle.direction;
	};

	const ruleChecker = (rule) => {
		if (previousTriangle[rule] === newTriangle[rule]) {
			score = score + 1;
		} else {
			// score = score - 1;
		}
	};

	const checkRule1 = () => {
		ruleChecker(rule1);
		setPreviousTriangle();
		triangleCreator();
	};

	const checkRule2 = () => {
		ruleChecker(rule2);
		setPreviousTriangle();
		triangleCreator();
	};

	const checkNoMatch = () => {
		if (
			previousTriangle[rule1] !== newTriangle[rule1] &&
			previousTriangle[rule2] !== newTriangle[rule2]
		) {
			score = score + 1;
		}
		setPreviousTriangle();
		triangleCreator();
	};
</script>

<div class="flex flex-col gap-5 w-screen h-screen items-center justify-center">
	<div><span class="text-4xl">{score}</span></div>

	<div class="pb-10">
		<div>Rule 1: Same {rule1}</div>
		<div>Rule 2: Same {rule2}</div>
	</div>

	<button on:click={checkRule1} class="p-2">Rule 1</button>

	<div class="flex gap-5">
		<div
			class="w-0 h-0
      border-l-[50px] border-l-transparent
      border-t-[75px] border-t-{newTriangle.color}-500
      border-r-[50px] border-r-transparent
      {newTriangle.direction === 'down' && 'rotate-0'}
      {newTriangle.direction === 'left' && 'rotate-90'}
      {newTriangle.direction === 'up' && 'rotate-180'}
      {newTriangle.direction === 'right' && '-rotate-90'}"
		>
			{#if newTriangle.dots === 4}
				<div class="flex flex-col absolute bottom-7 -left-1 gap-1 rotate-90">
					<div class="w-3 h-3 rounded-full bg-white" />
					<div class="w-3 h-3 rounded-full bg-white" />
					<div class="w-3 h-3 rounded-full bg-white" />
					<div class="w-3 h-3 rounded-full bg-white" />
				</div>
			{/if}
			{#if newTriangle.dots === 3}
				<div class="flex flex-col absolute bottom-7 -left-1 gap-1 rotate-90">
					<div class="w-3 h-3 rounded-full bg-white" />
					<div class="w-3 h-3 rounded-full bg-white" />
					<div class="w-3 h-3 rounded-full bg-white" />
				</div>
			{/if}
			{#if newTriangle.dots === 2}
				<div class="flex flex-col absolute bottom-7 -left-1 gap-1 rotate-90">
					<div class="w-3 h-3 rounded-full bg-white" />
					<div class="w-3 h-3 rounded-full bg-white" />
				</div>
			{/if}
			{#if newTriangle.dots === 1}
				<div class="flex flex-col absolute bottom-7 -left-1 rotate-90">
					<div class="w-3 h-3 rounded-full bg-white" />
				</div>
			{/if}
		</div>

		<button on:click={checkNoMatch} class="p-2">No match</button>
	</div>

	<button on:click={checkRule2} class="p-2">Rule 2</button>
</div>
