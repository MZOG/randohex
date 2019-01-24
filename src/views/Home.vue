<template>
  <div class="home">
    <div class="randomColor"></div>

    <div class="colorInfo">
      <p>Color info:</p>
      <p>Hex: <span class="colorHex"></span></p>
      <p>RGB: <span class="colorRgb"></span></p>
    </div>
  </div>
</template>

<script>

export default {
  name: 'home',
  components: {
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

      return color;
    },

    convertHexToRGB: function(color) {
      
      let hex = color.replace('#','');
      let r = parseInt(hex.substring(0,2), 16);
      let g = parseInt(hex.substring(2,4), 16);
      let b = parseInt(hex.substring(4,6), 16);

      // get colorRgb paragraph and write the rgb code into page
      let colorRgb = document.querySelector('.colorRgb');
      colorRgb.innerHTML = '('+ r + ', ' + g + ', ' + b + ')';
      
    }
  },
  mounted: function() {
    this.convertHexToRGB(this.getRandomColor());
  }
}
</script>
