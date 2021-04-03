<script>
	export let word;
    export let week;
    export let id;
</script>

<tr>
    <td>{id}</td>
    <td>
        <audio controls><source src="audio/{week}}/{word}.mp3" type="audio/mpeg">Your browser does not support the audio element.</audio>
    </td>
 </tr>