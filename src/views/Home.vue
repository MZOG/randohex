<template>
  <div class="home">
    <div class="randomColor">
    </div>

    <div class="colorInfo">
      <p>Hex: <span class="colorHex"></span></p>
    </div>

    <div class="recentColors">

    </div>

    <foot></foot>
  </div>
</template>

<script>

import Foot from '../components/Footer.vue';

export default {
  name: 'home',
  components: {
    Foot
  },
  methods: {
    getRandomColor: function() {
      let letters = '0123456789ABCDEF';
      let color = '#';

      for (let i = 0; i < 6; i++) {
        color += letters[Math.floor(Math.random() * 16)];
      }

      // get randomColor div and change background
      let colorContainer = document.querySelector('.randomColor');
      colorContainer.style.backgroundColor = color;

      // get colorHex paragraph and write the hex code into page
      let colorHex = document.querySelector('.colorHex');
      colorHex.innerHTML = color;
      
      // save recent colors to localStorage
      let savedColors = localStorage.getItem('colors');
      savedColors = (savedColors) ? JSON.parse(savedColors): [];
      savedColors.push(color);
      localStorage.setItem('colors', JSON.stringify(savedColors));

      for (let i = 0; i < savedColors.length; i++) {
        let recentColor = document.createElement('div');
        recentColor.className = ('recentColor');
        recentColor.style = ('background-color:' + savedColors[i]); 

        // let recentColorText = document.createTextNode(savedColors[i]);
        let recentColorText = document.createElement('p');
        recentColorText.innerHTML = savedColors[i];
        recentColor.appendChild(recentColorText);
        

        document.querySelector('.recentColors').prepend(recentColor);
        // document.querySelector('.recentColor').appendChild(recentColorText);
      }

      return color;

    },
  },
  mounted: function() {
    this.getRandomColor();
  }
}
</script>
