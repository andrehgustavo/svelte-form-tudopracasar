<script>
	import { getEventsAction } from "./utils.js";
	import { current_component } from "svelte/internal";
	const events = getEventsAction(current_component);
    export let value;
	export let question;

</script>

	<input use:events {value} placeholder={question.auxLabel} type={question.type} id={question.id} name={question.id} required/>

