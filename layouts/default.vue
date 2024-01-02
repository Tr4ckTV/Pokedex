<template>
    <div id="pokedex">
      <div id="left">
        <div id="bg_curve1_left"></div>
        <div id="bg_curve2_left"></div>
        <div id="curve1_left">
          <NuxtLink to="/">
            <div id="buttonGlass">
              <div id="reflect"></div>
            </div>
          </NuxtLink>

        <div id="miniButtonGlass1"></div>
        <div id="miniButtonGlass2"></div>
        <div id="miniButtonGlass3"></div>
      </div>
    <div id="curve2_left">

    </div>
    </div>
  </div>

  <div class="slot-content">
    <slot />
  </div>
</template>

<style scoped>

@media all {

  div#pokedex
  {
    position: fixed;
    z-index: 0;
  }

  .slot-content
{
  z-index: 10;
  position: relative;
  transform: translateY(20%);
}

div#left
{
  float: left;
  position: relative;
  z-index: 0;
}

div#curve1_left
{
  width: 52.7vw;
  height: 85px;
  background-color: #8b0000;
  float: left;
  padding: 15px 0 0 15px;
  z-index: 0;

  position: absolute;
  top: 0;
  left: 0;

  box-shadow: -10px 9px #5e0000;
  -webkit-box-shadow: -10px 9px #5e0000;
  -moz-box-shadow: -10px 9px #5e0000;
  -o-box-shadow: -10px 9px #5e0000;

  border-bottom-right-radius: 85px 60px;
  -webkit-border-bottom-right-radius: 85px 60px;
  -moz-border-bottom-right-radius: 85px 60px;
  -o-border-bottom-right-radius: 85px 60px;

  border-top-left-radius: 30px;
  -webkit-border-top-left-radius: 30px;
  -moz-border-top-left-radius: 30px;
  -o-border-top-left-radius: 30px;
}


div#bg_curve1_left
{
  width: 100vw;
  height: 80px;
  background-color: #8b0000;
  z-index: 0;

  border-top-left-radius: 30px;
  -webkit-border-top-left-radius: 30px;
  -moz-border-top-left-radius: 30px;
  -o-border-top-left-radius: 30px;
}

div#curve2_left
{
  width: 50vw;
  height: 451px;
  background-color: #c00d0d;
  float: right;
  z-index: 0;

  position: absolute;
  bottom: 45.5vh;
  right: 0;

  border-top-left-radius:85px 60px;
  -webkit-border-top-left-radius: 85px 60px;
  -moz-border-top-left-radius: 85px 60px;
  -o-border-top-left-radius: 85px 60px;
}

div#bg_curve2_left
{
  width: 100vw;
  height: 90vh;
  background-color: #c00d0d;    
  z-index: 0;

  border-bottom-left-radius: 30px;
  -webkit-border-bottom-left-radius: 30px;
  -moz-border-bottom-left-radius: 30px;
  -o-border-bottom-left-radius: 30px;
}

div#buttonGlass
{
  width: 60px;
  height: 60px;
  margin-right: 15px;
  border: 5px solid #fff;
  float: left;
  z-index: 0;

  box-shadow: 0 0 10px #490000;
  -webkit-box-shadow: 0 0 10px #490000;
  -moz-box-shadow: 0 0 10px #490000;
  -o-box-shadow: 0 0 10px #490000;
  
  background: radial-gradient(#05fbfb, #29abe3);
  background: -webkit-radial-gradient(#05fbfb, #29abe3);
  background: -moz-radial-gradient(#05fbfb, #29abe3);
  background: -o-radial-gradient(#05fbfb, #29abe3);
  
  border-radius: 35px;
  -webkit-border-radius: 35px;
  -moz-border-radius: 35px;
     -o-border-radius: 35px;
}

div#reflect
{
  width: 30px;
  height: 18px;
  margin: 3px 0 0 15px;
  background: #fff;
  opacity: 0.6;
  z-index: 0;

  border-radius: 15px 9px;
  -webkit-border-radius: 15px 9px;
  -moz-border-radius: 15px 9px;
     -o-border-radius: 15px 9px;
          
}

div#miniButtonGlass1
{
  width: 20px;
  height: 20px;
  margin-right: 10px;
  float: left;
  z-index: 0;

  box-shadow: 0 0 10px #490000;
  -webkit-box-shadow: 0 0 10px #490000;
  -moz-box-shadow: 0 0 10px #490000;
  -o-box-shadow: 0 0 10px #490000;

  border-radius: 20px;
  -webkit-border-radius: 20px;
  -moz-border-radius: 20px;
  -o-border-radius: 20px;
  
  background: radial-gradient(#fb7b7b, #fb0505);
  background: -webkit-radial-gradient(#fb7b7b, #fb0505);
  background: -moz-radial-gradient(#fb7b7b, #fb0505);
  background: -o-radial-gradient(#fb7b7b, #fb0505);
}

div#miniButtonGlass2
{
  width: 20px;
  height: 20px;
  margin-right: 10px;
  float: left;
  z-index: 0;

  box-shadow: 0 0 10px #490000;
  -webkit-box-shadow: 0 0 10px #490000;
  -moz-box-shadow: 0 0 10px #490000;
  -o-box-shadow: 0 0 10px #490000;

  border-radius: 20px;
  -webkit-border-radius: 20px;
  -moz-border-radius: 20px;
  -o-border-radius: 20px;
  
  background: radial-gradient(#fbfb9b, #fbfb05);
  background: -webkit-radial-gradient(#fbfb9b, #fbfb05);
  background: -moz-radial-gradient(#fbfb9b, #fbfb05);
  background: -o-radial-gradient(#fbfb9b, #fbfb05);
}

div#miniButtonGlass3
{
  width: 20px;
  height: 20px;
  margin-right: 10px;
  float: left;
  z-index: 0;

  box-shadow: 0 0 10px #490000;
  -webkit-box-shadow: 0 0 10px #490000;
  -moz-box-shadow: 0 0 10px #490000;
  -o-box-shadow: 0 0 10px #490000;

  border-radius: 20px;
  -webkit-border-radius: 20px;
  -moz-border-radius: 20px;
  -o-border-radius: 20px;
  
  background: radial-gradient(#b0fb7b, #50fb05);
  background: -webkit-radial-gradient(#b0fb7b, #50fb05);
  background: -moz-radial-gradient(#b0fb7b, #50fb05);
  background: -o-radial-gradient(#b0fb7b, #50fb05);
}
}

</style>