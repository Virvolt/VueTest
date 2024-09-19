<template>
    <div class="flex flex-col items-center justify-center bg-slate-700 h-screen text-slate-100 gap-6">
      <h2 class="text-2xl font-semibold">Qui êtes vous ? </h2>
      <!-- Avatars button -->
      <div class=" space-x-6 font-semibold">
        <button class=" bg-slate-50 text-gray-700 p-4 rounded-xl hover:bg-pink-200 focus:bg-pink-300"
        @click="displayAvatarStory('katia')">
        
        Katia
          <img src="/katia.svg" alt="old Katia" width="50"/>
        </button>
        <button class=" bg-slate-50 text-gray-700 p-4 rounded-xl hover:bg-blue-200 focus:bg-blue-300"
            @click="displayAvatarStory('pascalou')" >
            Pascal
            <img src="/pascal.svg" alt="old Pascal" width="50"/>
        </button>
      </div>

    <!--Scénario Avatar katia -->
        <div v-if="toggleAvatarButton==='katia'" class="bg-slate-500 rounded m-10 p-5 flex flex-col">
          
          
          <div v-if="counter >= 1" class=" flex flex-col items-center pt-2">
            <h3 class="text-center text-xl font-semibold">Coucou {{ compliments.katia.fonction }}</h3>
            <p class="mt-2">Clic sur le bouton pour un sourire</p>
            
            <p class="p-4 font-bold"> {{complimentAleatoire.toUpperCase()}}</p>
            <button class="bg-lime-200 self-center px-4 py-2 rounded text-slate-800 font-semibold hover:bg-lime-300 active:bg-lime-400 mt-2"
            @click="afficherComplimentAleatoire">
            Il te reste encore : {{ counter }} {{ counter === 1 ? 'clic' : 'clics' }}</button>

          </div>
          <div v-else class="flex items-center gap-2">
              <h4>C'est terminé, sachez que je vous aimes fort!</h4>
              <img src="/kiss.svg" alt="Des Bisous" width="50">
          </div>
        </div>

        <!--Scénario Avatar Pascal -->
        <div v-if="toggleAvatarButton==='pascalou'" class="bg-slate-500 rounded m-10 p-5 flex flex-col">
          
          
          <div v-if="counter >= 1" class=" flex flex-col items-center pt-2">
            <h3 class="text-center text-xl font-semibold">Coucou {{ compliments.pascalou.fonction }}</h3>
            <p class="mt-2">Clic sur le bouton pour un sourire</p>
            
            <p class="p-4 font-bold"> {{complimentAleatoire.toUpperCase()}}</p>
            <button class="bg-amber-200 self-center px-4 py-2 rounded text-slate-800 font-semibold hover:bg-amber-300 active:bg-amber-400 mt-2"
            @click="afficherComplimentAleatoire">
            Il te reste encore : {{ counter }} {{ counter === 1 ? 'clic' : 'clics' }}</button>

          </div>
          <div v-else class="flex items-center gap-2">
              <h4>C'est terminé, sachez que je vous aimes fort!</h4>
              <img src="/love.svg" alt="Des Bisous" width="50">
          </div>
        </div>

      </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const compliments = {
  pascalou: {
    fonction: 'beau papa',
    compliment: [
      '« Dieu a dit : “Je partage en deux, les riches auront de la nourriture, les pauvres de l’appétit.” » – Coluche',
      '« La vie est une maladie sexuellement transmissible. » – Coluche',
      '« On peut rire de tout mais pas avec tout le monde. » – Pierre Desproges',
      '« La différence entre un homme et une pizza, c’est que la pizza peut être réchauffée. » – Pierre Desproges',
      '« Si vous avez une belle-mère, ne la laissez pas tomber dans la piscine ! » – Raymond Devos',
      '« Je ne suis pas raciste, je déteste tout le monde. » – Raymond Devos',
      '« Les bêtises, ça n’arrive pas qu’aux autres. » – Raymond Devos',
      '« Le rire est le propre de l’homme, mais on peut aussi en rire. » – Pierre Desproges',
      '« Les statistiques, c’est comme les mini-jupes. Ça donne des idées mais ça cache l’essentiel. » – Coluche',
      '« Quand on est vieux, on a encore des souvenirs, mais on ne peut plus les partager avec ceux qui n’étaient pas là. » – Pierre Desproges',
      '« La France est le pays des libertés. Les Français n’en profitent que pour critiquer les autres. » – Coluche',
      '« La meilleure manière de réaliser ses rêves, c’est de se réveiller. » – Pierre Desproges',
      '« L’honnêteté est une vertu qu’il est parfois difficile de pratiquer quand on a des dents en trop. » – Raymond Devos',
    ]
  },
  katia: {
    fonction: 'belle maman',
    compliment: [
      '« Je ne suis pas sûr que l’on doive toujours dire la vérité, mais j’ai l’impression que c’est souvent mieux que de mentir. » – Pierre Desproges',
      '« Les cons, ça ose tout. C’est même à ça qu’on les reconnaît. » – Michel Audiard',
      '« Quand on est né avec un défaut, il vaut mieux qu’on en ait plusieurs. » – Raymond Devos',
      '« L’avenir, c’est ce qui nous arrive quand on n’est pas prêt. » – Pierre Desproges',
      '« Il vaut mieux avoir un ami qui se moque de soi que d’être seul avec sa propre solitude. » – Coluche',
      '« On peut tout faire avec la tête, sauf la mettre dans le gaz. » – Raymond Devos',
      '« La chance, c’est ce qui vous arrive quand vous êtes préparé. » – Pierre Desproges',
      '« Les femmes, c’est comme les bateaux : plus elles sont grandes, plus elles sont chères. » – Coluche',
      '« On n’est jamais mieux servi que par soi-même, sauf quand on est complètement incompétent. » – Raymond Devos',
      '« La procrastination est la mère de tous les vices… mais je n’ai pas encore trouvé le temps de m’en occuper. » – Pierre Desproges',
      '« Je suis pour l’égalité des sexes, mais je suis contre l’égalité des salaires. » – Coluche',
      '« Le problème des gens qui parlent trop, c’est qu’ils ne laissent pas le temps aux autres de leur répondre. » – Raymond Devos',
    ]
  }
};

const counter = ref(4)
const toggleAvatarButton = ref('none')
const complimentAleatoire = ref('');
let complimentsRestants = ref([])


// Fonction pour afficher l'histoire de l'avatar sélectionné
const displayAvatarStory = (avatar) => {
  if (compliments[avatar]) {
    toggleAvatarButton.value = avatar;
    counter.value = 4; // Réinitialiser le compteur
    complimentAleatoire.value = ''; // Réinitialiser le message
    complimentsRestants.value = [...compliments[avatar].compliment]; // Réinitialiser la liste des compliments restants
  }
};

  
 const afficherComplimentAleatoire = () => {
  if (counter.value >= 1 && complimentsRestants.value.length > 0) { 
    counter.value--; // Décrémente le compteur
    
    // Générer un index aléatoire pour le compliment
    const indexAleatoire = Math.floor(Math.random() * complimentsRestants.value.length);
    complimentAleatoire.value = complimentsRestants.value[indexAleatoire];
    
    // Supprimer le compliment sélectionné de la liste des compliments restants
    complimentsRestants.value.splice(indexAleatoire, 1);
  }
};
    


</script>


