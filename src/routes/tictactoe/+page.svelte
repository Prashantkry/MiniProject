<script>
	let buttons = new Array(9).fill(null);
	let result = null;
	let turn = 'X';
	const combinationWin = [
		[0, 1, 2],
		[3, 4, 5],
		[6, 7, 8],
		[0, 3, 6],
		[1, 4, 7],
		[2, 5, 8],
		[0, 4, 8],
		[2, 4, 6]
	];

	function setValue(i) {
		buttons[i] = turn;
		// buttons = [...buttons];
		turn = turn == 'X' ? 'O' : 'X';

		// check winner
		checkWinner();

		// check draw
		if (!result && buttons.every((button) => button !== null)) {
			result = 'Match Draw';
		}
	}

	function checkWinner() {
		for (let i = 0; i < combinationWin.length; i++) {
			if (buttons[combinationWin[i][0]] != null) {
				if (
					buttons[combinationWin[i][0]] == buttons[combinationWin[i][1]] &&
					buttons[combinationWin[i][1]] == buttons[combinationWin[i][2]]
				) {
					result = 'Winner: ' + buttons[combinationWin[i][0]];
					break;
				}
			}
		}
	}

	function restart() {
		buttons = new Array(9).fill(null);
		result = null;
		turn = 'X';
	}

	import { onMount } from 'svelte';
	onMount(() => {
		// alert("Let's start the game!")
	});

	function getButtonClass(button) {
		// Add logic to determine the background color based on the button value
		if (button === 'X') {
			return 'bg-blue-500'; // Change to your desired color for 'X'
		} else if (button === 'O') {
			return 'bg-red-500'; // Change to your desired color for 'O'
		} else {
			return 'bg-yellow-400'; // Default color for empty cells
		}
	}
</script>

<main>
	<h2 class=" text-center p-2 text-3xl font-bold shadow-lg">Tic Tac Toe</h2>
	<div class=" text-red-600 font-bold w-[30%]  p-2 m-4 text-center">
		{#if !result}
			<div class="mt-10 w-[300px] h-[300px] m-auto flex-wrap flex justify-center items-center">
				{#each buttons as button, i}
					<button
						on:click={() => {
							setValue(i);
						}}
						class="border-2 w-[100px] h-[100px] transition duration-300 ease-in-out {getButtonClass(
							button
						)}"
					>
						{button ? button : ''}
					</button>
				{/each}
			</div>
		{:else}
			<div>
				{result}
				<button class=" bg-green-700 p-2 rounded-md font-semibold cursor-pointer" on:click={restart}
					>Restart</button
				>
			</div>
		{/if}
	</div>
    <div class="">
        <div>
            <h2
                class="w-[35%]  text-center p-2 bg-pink-700 rounded-sm font-bold shadow-sm border-2 text-3xl mt-10 ml-3 mr-3"
            >
                Rules to Play Game
            </h2>
            <div class=" border-2 m-10 shadow-lg p-6 w-[31%] text-left font-bold ">
                <ol class="m-2">
                    <li class=" border-b-2 p-2 m-3">1. Click on any box randomly</li>
                    <li class=" border-b-2 p-2 m-3">2. Double click to change between X & O</li>
                    <li class=" border-b-2 p-2 m-3">3. Then play game till any one win</li>
                </ol>
            </div>
        </div>
        <!-- image -->
        <div>

        </div>
    </div>
</main>
