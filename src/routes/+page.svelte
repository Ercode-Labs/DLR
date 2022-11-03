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
		<div>Press top button if following triangle has the same {rule1}.</div>
		<div>Press bottom button if following triangle has the same {rule2}.</div>
		<div>If none of them is the same, press right.</div>
	</div>

	<button on:click={checkRule1} class="m-5 h-10 w-10 border rounded hover:bg-gray-500" />

	<div class="flex gap-5">
		<div
			class="w-0 h-0
      border-l-[50px] border-l-transparent border-t-[75px]
      {newTriangle.color === 'red' && 'border-t-red-500'}
      {newTriangle.color === 'yellow' && 'border-t-yellow-500'}
      {newTriangle.color === 'blue' && 'border-t-blue-500'}
      {newTriangle.color === 'green' && 'border-t-green-500'}
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

		<button on:click={checkNoMatch} class="m-5 h-10 w-10 border rounded hover:bg-gray-500" />
	</div>

	<button on:click={checkRule2} class="m-5 h-10 w-10 border rounded hover:bg-gray-500" />
</div>
