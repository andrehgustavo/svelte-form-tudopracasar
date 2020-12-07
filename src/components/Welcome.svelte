<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();

    function startForm() {
		dispatch('start');
	}

</script>

<div class="center-div-column">
    <h5 style="text-white">
        Olá, queridos noivos. Aqui vamos coletar algumas informações essenciais
        sobre como vocês imaginam sua festa, a fim de que possamos elaborar um
        orçamento com os serviços do jeitinho que vocês sonham.
    </h5>

    <button on:click={startForm} class="signup-button mt-4">
        Iniciar formulário
    </button>
</div>
