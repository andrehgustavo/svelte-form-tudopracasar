<div class="container">
    <section id="logo">
        <div class="jumbotron text-center mt-3 col-md-12">
            <img {src}
                class="img-fluid mt-3"
                alt="Laços formando um coração"
                title="Logo TudoPraCasar" />
            <h4>Seu casamento em poucos cliques.</h4>
            <hr class="my-4" />
        </div>
    </section>
    <section id="form-section">
        {#if startForm}            
            <FormQuestions/> 
        {:else}
            <Welcome on:start={onStart}/>                   
        {/if}
    </section>
    <footer id="footer">
        <div class="wrap">
            <div class="social-links">
                <ul>
                    <li>
                        <a href="https://www.facebook.com/tudopracasar.com.br">
                            <i class="fab fa-facebook-f icon"></i> </a>
                    </li>
                    <li>
                        <a href="https://www.instagram.com/tudopracasar.com.br/"><i
                                class="fab fa-instagram icon"></i></a>
                    </li>
                    <li>
                        <a
                            href="https://api.whatsapp.com/send?phone=5584988189020&text=Gostaria%20de%20tirar%20uma%20d%C3%BAvida"><i
                                class="fab fa-whatsapp icon"></i></a></li>
                </ul>
            </div>
        </div>
    </footer>
</div>
<script>
    import FormQuestions from './FormQuestions.svelte';
    import Welcome from './Welcome.svelte';
    let src = "./images/logo_TudoPraCasar.png";
    let startForm = false;
    
    function onStart(event) {
		startForm = true;
	}

</script>
