<script>
	import { getEventsAction } from "./utils.js";
	import { current_component } from "svelte/internal";
	const events = getEventsAction(current_component);
    export let value;
    export let fornecedor;
</script>
<textarea class="input-checkbox" use:events {value} placeholder={fornecedor.auxLabel} id={fornecedor.tipo} name={fornecedor.tipo} rows="4"/>
