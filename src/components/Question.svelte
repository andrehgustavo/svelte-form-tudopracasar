<script>
    import { createEventDispatcher } from "svelte";
    import Button from "./Button.svelte";
    import Input from "./Input.svelte";
    import InputCheckbox from "./InputCheckbox.svelte";
    export let question;
    export let status;
    export let questions;
    let isFocused = false;
    const dispatcher = createEventDispatcher();
    let value = "";
    const onInput = (e) => (value = e.target.value);
    const onFocus = () => (isFocused = true);    




</script>

{#if typeof question.fornecedores != 'undefined'}
    <label class="label-text">{question.statement}</label>
    {#each question.fornecedores as fornecedor, index (fornecedor)}
        <div>
            <label class="label-check-box">
                <input
                    class="check-box"
                    type="checkbox"
                    id={fornecedor.tipo}
                    name={fornecedor.tipo}
                    bind:checked={fornecedor.checked}
                    value={fornecedor.name} />{fornecedor.name}
                {#if fornecedor.checked}
                    <InputCheckbox
                        {fornecedor}
                        on:input={onInput}
                        on:focus={onFocus}
                        on:blur={dispatcher('selectedCheckbox', [value, index])}
                        value={fornecedor.answer} />
                {/if}                
            </label>
        </div>
    {/each}
    <Button {questions} {status} on:changeStatus></Button>
{:else if question.type == 'end'}
    <Button {questions} {status} on:changeStatus></Button>
{:else}
    <label class="label-text">{question.statement}</label>
    <Input
        {question}
        on:input={onInput}
        on:focus={onFocus}
        on:blur={dispatcher('selected', value)}
        value={question.answer} />
        
{/if}
