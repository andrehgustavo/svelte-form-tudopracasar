<script>
import { onMount } from "svelte";
import { createEventDispatcher } from "svelte";
    export let questions;
    export let status;
    const dispatcher = createEventDispatcher();

    function change(){
        console.log('Status em Button: ' + status);
        dispatcher('changeStatus')
    }

    onMount(() =>{        
        const formElement = document.querySelector('#contact-form');
        formElement.addEventListener('submit', (event) =>{
            event.preventDefault();
            const data = new URLSearchParams(new FormData(formElement));
            fetch('https://getform.io/f/91cbf13b-dddc-457c-b7bb-5287303c1aab', {
                method: 'post',
                body: data
            });
            dispatcher('changeStatus');
        })
    });
    

</script>

<form id="contact-form" action="https://getform.io/f/91cbf13b-dddc-457c-b7bb-5287303c1aab" method="POST">
    <div class="off">
        <input type="text" name="name" value={questions[0].answer}>
        <input type="email" name="email" value={questions[1].answer}>
        <input type="text" name="phone" value={questions[2].answer}>
        <input type="text" name="wedding_date" value={questions[3].answer}>
        <input type="text" name="guests" value={questions[4].answer}>
        <input type="text" name="bugdet" value={questions[5].answer}>
        <input type="text" name="place" value={questions[6].answer}>
        <input type="text" name="banda_cerimonia" value={questions[7].fornecedores[0].answer} >
        <input type="text" name="bandas_festa" value={questions[7].fornecedores[1].answer}>
        <input type="text" name="bebidas" value={questions[7].fornecedores[2].answer}>
        <input type="text" name="bolo" value={questions[7].fornecedores[3].answer}>
        <input type="text" name="buffet" value={questions[7].fornecedores[4].answer}>
        <input type="text" name="cabine_entretenimento" value={questions[7].fornecedores[5].answer}>
        <input type="text" name="celebrante" value={questions[7].fornecedores[6].answer}>
        <input type="text" name="cerimonial" value={questions[7].fornecedores[7].answer}>
        <input type="text" name="convites" value={questions[7].fornecedores[8].answer}>
        <input type="text" name="decoracao" value={questions[7].fornecedores[9].answer}>
        <input type="text" name="doces" value={questions[7].fornecedores[10].answer}>
        <input type="text" name="filmagem" value={questions[7].fornecedores[11].answer}>
        <input type="text" name="fotografo" value={questions[7].fornecedores[12].answer}>
        <input type="text" name="gerador" value={questions[7].fornecedores[13].answer}>
        <input type="text" name="igreja" value={questions[7].fornecedores[14].answer}>
        <input type="text" name="iluminacao_som" value={questions[7].fornecedores[15].answer}>
        <input type="text" name="manobrista_seguraca" value={questions[7].fornecedores[16].answer}>
        <input type="text" name="recepcao_espaco" value={questions[7].fornecedores[17].answer}>
        <input type="text" name="salao_de_noiva" value={questions[7].fornecedores[18].answer}>
        <input type="text" name="vestido" value={questions[7].fornecedores[19].answer}>
    </div>
    <div class="center-div-row">
    {#if !status}
        <button type="submit" class="signup-button mt-4">
            Enviar
        </button>
    {/if}
    </div>   
  
  </form>
  <!-- <button type='button' class="signup-button mt-4" on:click={change} value={false}>Teste</button> -->
  {#if status}
        <br>  
        <div class="alert alert-success mt-3">Respostas enviadas com Sucesso!</div>
        <a class="signup-button mt-4" href="https://www.tudopracasar.com.br/">Voltar para o TudoPraCasar</a>
    {/if}