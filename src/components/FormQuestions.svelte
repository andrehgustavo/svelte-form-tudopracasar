<script>
    import Question from "./Question.svelte";
    let status=false;
    let alertMessage='';
    let questions = [
        {
            statement: "Qual o nome do casal?",
            id: "name",
            auxLabel: "João e Maria",
            type: "input",
            answer: "",
        },
        {
            statement: "E-mail para resposta:",
            id: "email",
            auxLabel: "email@gmail.com",
            type: "email",
            answer: "",
        },
        {
            statement: "Telefone para contato",
            id: "tel",
            auxLabel: "(XX) XXXXX-XXXX",
            type: "tel",
            answer: "",
        },
        {
            statement: "Qual a data do casamento?",
            id: "wedding_date",
            auxLabel: "11/10/2022",
            type: "date",
            answer: "",
        },
        {
            statement: "Quantos convidados?",
            id: "guests",
            auxLabel: "",
            type: "number",
            answer: "",
        },
        {
            statement: "Qual o valor disponível para o casamento?",
            id: "bugdet",
            auxLabel: "R$30.000,00",
            type: "number",
            answer: "",
        },
        {
            statement: "Nome da Cidade ou da Praia que querem casar?",
            id: "place",
            auxLabel: "",
            type: "input",
            answer: "",
        },
        {
            statement:
                "Marque as opções de fornecedores que desejam ter em sua festa! Nas opções marcadas, você pode adicionar alguma preferência.",
            auxLabel: "",
            type: "checkbox",
            fornecedores: [
                {
                    tipo: "banda_cerimonia",
                    name: "Banda Cerimônia",
                    check: false,
                    answer: "",
                    auxLabel: "Ex.: Voz feminina e piano; somente violino; etc",
                },
                {
                    tipo: "bandas_festa",
                    name: "Banda Festa",
                    check: false,
                    answer: "",
                    auxLabel: "Ex.: 01 de samba e 01 de sertanejo, etc",
                },
                {
                    tipo: "bebidas",
                    name: "Bebidas",
                    check: false,
                    answer: "",
                    auxLabel: "Ex.: Whisky 12 anos e chopp, etc",
                },
                {
                    tipo: "bolo",
                    name: "Bolo",
                    check: false,
                    answer: "",
                    auxLabel: "Ex.: De ameixa e com 2 andares, etc",
                },
                {
                    tipo: "buffet",
                    name: "Buffet",
                    check: false,
                    answer: "",
                    auxLabel: "Ex.: Buffet com camarão ou com filé e salmão, etc",
                },
                {
                    tipo: "cabine_entretenimento",
                    name: "Cabine Entretenimento",
                    check: false,
                    answer: "",
                    auxLabel:
                        "Ex.: Gravação de videos pelos convidados; impressão imediata de fotos, etc",
                },
                {
                    tipo: "celebrante",
                    name: "Celebrante",
                    check: false,
                    answer: "",
                    auxLabel: "Ex.: Juiz de Paz, Anglicano, evangélico, etc",
                },
                {
                    tipo: "cerimonial",
                    name: "Cerimonial",
                    check: false,
                    answer: "",
                    auxLabel: "",
                },
                {
                    tipo: "convites",
                    name: "Convites",
                    check: false,
                    answer: "",
                    auxLabel: "Ex.: Tradicional, rústico, etc",
                },
                {
                    tipo: "decoracao",
                    name: "Decoração",
                    check: false,
                    answer: "",
                    auxLabel:
                        "Ex.: Clássica, contemporânea, com as cores X e Y, etc",
                },
                {
                    tipo: "doces",
                    name: "Doces",
                    check: false,
                    answer: "",
                    auxLabel: "Ex.: Chocolate, bem-casado, trufas, etc",
                },
                {
                    tipo: "filmagem",
                    name: "Filmagem",
                    check: false,
                    answer: "",
                    auxLabel:
                        "Ex.: Somente a cerimônia; making of, cerimônia e festa; etc",
                },
                {
                    tipo: "fotografo",
                    name: "Fotógrafo",
                    check: false,
                    answer: "",
                    auxLabel:
                        "Ex.: Pacote cerimônia + festa; making of dos noivos, ensaio pré-casamento, etc",
                },
                {
                    tipo: "gerador",
                    name: "Gerador de Energia",
                    check: false,
                    answer: "",
                    auxLabel: "Ex.: Somente festa; cerimônia e festa",
                },
                {
                    tipo: "igreja",
                    name: "Igreja",
                    check: false,
                    answer: "",
                    auxLabel: "Ex.: Localidade X ou Y; arquitetura moderna, etc",
                },
                {
                    tipo: "iluminacao_som",
                    name: "Iluminação/Som",
                    check: false,
                    answer: "",
                    auxLabel:
                        "Ex.: Iluminação cerimônia e festa; paineis de LED no palco; dancing; 01 ou 02 palcos, etc",
                },
                {
                    tipo: "manobrista_seguraca",
                    name: "Manobrista/Seguraça",
                    check: false,
                    answer: "",
                    auxLabel:
                        "Ex.: Com traslado igreja-recepção; somente orientador de estacionamento, etc",
                },
                {
                    tipo: "recepcao_espaco",
                    name: "Recepção/Espaço",
                    check: false,
                    answer: "",
                    auxLabel: "Ex.: Ambiente fechado; espaço aberto; na praia; etc",
                },
                {
                    tipo: "salao_de_noiva",
                    name: "Salão de Noiva",
                    check: false,
                    answer: "",
                    auxLabel: "Ex.: Dia da noiva ou apenas maquiagem/penteado, etc",
                },
                {
                    tipo: "vestido",
                    name: "Vestido da Noiva",
                    check: false,
                    answer: "",
                    auxLabel: "Ex.: Aluguel ou compra.",
                },
            ],
        }
    ];
    let current = 0;
    let required = false;

    function next() {        
        if(questions[current].type == 'email'){
            validateEmail();
        }
        if(questions[current].answer != '' && current < questions.length - 1) {
            required=false;
            current++;
        }else{
            alertMessage='Campo obrigatório.'
            required=true;
        }        
    }

    function back() {
        required=false;
        if (current > 0) {
            current--;
        }
    }

    function onSelect(event) {
        questions[current].answer = event.detail;
    }
    function onSelectCheckbox(event) {
        questions[current].fornecedores[event.detail[1]].answer =
            event.detail[0];
    }

    function onStatusChange(event) {
        status=!status;
    }
    function validateEmail(){
        var mailformat = /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/;
        if(!questions[current].answer.match(mailformat)){
            alertMessage='Digite um email válido!'
            required=true;
            document.form1.text1.focus();
        }
    }
    
</script>

<div class="center-div-row">
    {#if current != 0}
        <i class="fas fa-angle-left prev" on:click={back} />
    {/if}
    <div class="center-div-column">
        <form >
            <Question
                {questions}
                {status}
                question={questions[current]}
                on:selected={onSelect}
                on:selectedCheckbox={onSelectCheckbox}
                on:changeStatus={onStatusChange} />
        </form>
        {#if required} 
            <div class="alert alert-danger mt-3">{alertMessage}</div>            
        {/if}
    </div>
    {#if current != questions.length-1}
        <i class="fas fa-angle-right next" on:click={next} />
    {/if}
    
</div>

<div class="center-div-row label-text pagination">{current + 1} de {questions.length}</div>
