<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import {onBeforeMount, onMounted } from 'vue'


window.onload = function(){
  let questions = `
  Un buen estilo de vida nos ayuda a mantenernos sanos personalmente, físicamente y mentalmente. ¿Cómo?
  Tener dos culturas y hablar dos idiomas tiene ventajas y desventajas. ¿Cuáles?
  Comer y compartir comida es una actividad social que tiene un impacto fuerte.
  Ser bilingüe es mejor que ser monolingüe. ¿Verdadero o falso?
  El móvil y los robots enriquecen nuestras vidas. ¿Verdadero o falso?
  Los bailes tradicionales nunca deberían cambiar. ¿Verdadero o falso?
  En tiempos malos como el covid-19, la gente recurre al arte para aguantar. ¿Por qué?
  ¿Qué significa la apropriación cultural?
  ¿Eres un viajero o un turista?
  ¿Cómo podemos viajar sin perjudicar al planeta o a la cultura de los sitios que visitamos?
  Todas las tradiciones son buenas. ¿Verdadero o falso?
  `.split('\n')
  


  const text = document.getElementById("textToConvert");
  const convertBtn = document.getElementById("convertBtn");

  convertBtn.addEventListener('click', function () {
    let voices = window.speechSynthesis.getVoices()


    for (let k = 0; k < 2000; k++) {
      if (voices[k].lang=="es") {
        console.log(k);
      }
    }

    let vo = 166;
    console.log(voices[vo])
    
    const speechSynth = window.speechSynthesis;
    const enteredText = text.value;
    const error = document.querySelector('.error-para');

    if (!speechSynth.speaking &&
        !enteredText.trim().length) {
        error.textContent = `Nothing to Convert! 
        Enter text in the text area.`
    }

    if (!speechSynth.speaking) {
        error.textContent = "bruh";
        const newUtter = new SpeechSynthesisUtterance(questions[Math.floor(Math.random()*questions.length)]);
        newUtter.voice = voices[vo];
        newUtter.lang = voices[vo].lang;
        console.log(voices)
        window.speechSynthesis.cancel();
        speechSynth.speak(newUtter);
        convertBtn.textContent = "Sound is Paying..."
    }
    
    setTimeout(() => {
        convertBtn.textContent = "Play Converted Sound"
    }, 5000);
});
}

</script>

<template>
  <header>

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>

    <div class="interaction-container">
                <textarea id="textToConvert" 
                    placeholder="Enter text to convert into speech..." 
                    cols="35" rows="10" 
                    class="text-control"></textarea>

                <p class="error-para"></p>

                <button class="btn" id="convertBtn">
                    Play Converted Sound
                </button>
            </div>
  </header>

</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
