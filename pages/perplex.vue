<template>
    <div>
      <div ref="div1" class="div1">Div 1</div>
      <div ref="div2" class="div2">Div 2</div>
      <button @click="animate">Animer</button>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue'
  import { gsap } from 'gsap'
  
  const div1 = ref(null)
  const div2 = ref(null)
  
  const animate = () => {
    const tl = gsap.timeline()
  
    // Animation de div1
    tl.to(div1.value, {
      x: '100%', // Déplacement à droite
      duration: 1, // Durée de l'animation horizontale
      ease: 'power2.inOut'
    }).to(div1.value, {
      y: '100%', // Déplacement vers le bas
      duration: 1, // Durée de l'animation verticale
      ease: 'power2.inOut'
    }, '-=0.5') // Commence 0.5s avant la fin de l'animation précédente
  
    // Animation de div2
    tl.to(div2.value, {
      y: '-100%', // Déplacement du bas vers le haut
      scale: 1.5, // Augmentation de la taille
      duration: 1.5, // Durée totale de l'animation de div2
      ease: 'power2.inOut'
    }, '-=1') // Commence 1s avant la fin de l'animation de div1
  }
  
  onMounted(() => {
    // Initialisation si nécessaire
  })
  </script>
  
  <style scoped>
  .div1, .div2 {
    width: 100px;
    height: 100px;
    background-color: #3498db;
    margin: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    color: white;
  }
  
  .div2 {
    background-color: #e74c3c;
  }
  
  button {
    margin: 20px;
  }
  </style>