<script>
	import NavBar from "./NavBar.svelte"
	import Question from "./Question.svelte"

	let questions =
	[
		{
			word: "out",
			week: 5
		},
		{
			word: "now",
			week: 5
		},
		{
			word: "flower",
			week: 5
		},
		{
			word: "clown",
			week: 5
		},
		{
			word: "house",
			week: 5
		},
		{
			word: "sound",
			week: 5
		},
		{
			word: "crowd",
			week: 5
		},
		{
			word: "found",
			week: 5
		},
		{
			word: "ground",
			week: 5
		},
		{
			word: "buses",
			week: 4
		},
		{
			word: "watches",
			week: 4
		},
		{
			word: "numbers",
			week: 4
		},
		{
			word: "passes",
			week: 4
		},
		{
			word: "blocks",
			week: 4
		}
	]
	function submitTest()
	{
		var elements = document.getElementById("questionsForm").elements;

		let score =0
		
		for (var i = 0, element; element = elements[i++];) {
			if (element.id === element.value )
				score = score+1;
			else
                element.style = "background-color:red"
		}

		let numQuestion = elements.length -1
		if (score == numQuestion)
			// perfect score
			document.getElementById("score").style.color = "green";
		else
			// non-perfect score
			document.getElementById("score").style.color = "red";

        document.getElementById("score").innerHTML = score;
	}
</script>

<NavBar />
<div>
	{#if Question.length == 0}
		<p>No questions</p>
	{:else}
		<form id="questionsForm" method="POST">
			<table border="1">
				{#each questions as question, id}
					<Question word={question.word} week={question.week} id={id+1}/>
					<td colspan="2"><input type="text" autocomplete="off" colspan="2" id="{question.word}" value="" style=""/></td>
				{/each}
			</table>
			<input type="button" value="I'm Done!" on:click="{submitTest}"/>

			<p id="score" value=""></p>
		</form>
	{/if}
</div>