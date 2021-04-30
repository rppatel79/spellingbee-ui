<script>
	import NavBar from "./NavBar.svelte"
	import Question from "./Question.svelte"

    const questionGeneratorUrl ="https://hsbva3hv4b.execute-api.us-west-2.amazonaws.com/default/questionGeneratorFunction"

    let loading=true;
    let questions= onLoad();

    async function onLoad() {
        try
        {
            console.log('onLoad');
            const questionGeneratorUrl ="https://pyr308hstc.execute-api.us-east-1.amazonaws.com/default/spellingtestQuestionGenerateFunction"
            // Call an authenication microservice to handle the authentication.
            const response = await fetch(questionGeneratorUrl,
                {
                    method: 'POST',
                }
            );
            let responseVal= await response;
            questions=  await responseVal.json();
            console.log(questions)
        }
        catch(err) {
            console.error(err);
        }
        finally{
            loading=false;
        }
    }

    function saveResults(data)
    {
        const url ="https://pjsn8b2l0f.execute-api.us-east-1.amazonaws.com/default/spellingtestSaveResults"

		// request options
		const options = {
			method: 'POST',
			body: JSON.stringify(data)
			/*,
			headers: {
				'content-type': 'application/json'
			}*/
		}

		// send post request
		fetch(url, options)
			.then(res => res.json())
			.then(res => console.log(res))
			.catch(err => console.error(err));

    }

	function submitTest()
	{
		var elements = document.getElementById("questionsForm").elements;

		let score =0

        var wordsArray =[]
        for (var i = 0, element; element = elements[i++];) {
			if (element.id != "buttonId")
			{
                var word ={}
                word['word']=element.id.toUpperCase()
                word['guess']=element.value.toUpperCase()

                if (element.id.toUpperCase() === element.value.toUpperCase() )
                {
                    score = score+1;
                    element.style = ""

                    word['correct']='true'
                }
                else
                {
                    element.style = "background-color:red"

                    word['correct']='false'
                }

                wordsArray[wordsArray.length]=word
		    }
		}

        let allWords ={"words" : wordsArray}
        console.log(allWords)
        saveResults(allWords)

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
	{#if loading }
		<p>Loading</p>
	{:else}
		<form id="questionsForm" method="POST">
			<table border="1">
				{#each questions as question, id}
					<Question word={question.word} week={question.week} id={id+1}/>
					<td colspan="2"><input type="text" autocomplete="off" colspan="2" id="{question.word}" value="" style=""/></td>
				{/each}
			</table>
			<input id="buttonId" type="button" value="I'm Done!" on:click="{submitTest}"/>

			<p id="score" value=""></p>
		</form>
	{/if}
</div>