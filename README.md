<!DOCTYPE html>
<html>
<!--
Wall breaker game

made by Sriharsh 

coming soon: sounds ??.
-->
<head>
<meta name="description" content="canvas breakout">
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>Breakout edition</title>
  <style>
    #cv{border:1px solid}
    .btdi{width:60px;
        height:30px;
        font-size:20px;
    }
    
    
  </style>
  
</head>
<body>
  
  <canvas id=cv width=300 height=240></canvas><br>
  
    <input class=btdi type=button value="<--" onmousedown=irizQ() onmouseup=paR() style="margin-left:95px;margin-top:30px">
    <input class=btdi type=button value="-->" onmousedown=irdeR() onmouseup=paR() style="margin-left:15px"><br>
  <input id=bt type=button value="start" onclick=starT()>
  <input id=btAg type=button value="again" onclick=agaiN()>
  <input id=btPa type=button value="pause" onclick=pausE() style="margin-left:160px"><br>
  
  <fieldset style="width:280px">
    <legend>Controls:</legend>
    <input id=rdT type=radio name=ctrls><label for=rdT>Touch or Mouse</label><br>
    <input id=rdB type=radio  name=ctrls checked><label for=rdB>Buttons or Keyboard</label>
  </fieldset>
  

  
 <script>
   //w480 h320
   
  var pi=Math.PI;
   var co=cv.getContext("2d");
   
   var scorep=0;//score parcial
   var score=0;
   
   function dscorE(){
     co.font="16px consolas";
     co.fillStyle="grey";
     co.fillText("Score: "+score,8,20);
   }//dibujar puntaje
   
   
   var lvl=1;
   
   function dlvL(){
       co.font="16px consolas";
       co.fillStyle="dodgerblue";
       co.fillText("Level: "+lvl,125,20);
       co.fillStyle="grey";
       co.closePath();
   }//dibujar level
   
   
   var lives=3;
   
   function dliveS(){
     co.font="16px consolas";
     co.fillStyle="greydark";
     co.fillText("Lives: "+lives,cv.width-70,20);
   }//dibujar vidas
   
   
   
   
   
   
      
   //brick row columns width height padding offset top left
   var brrwc = 3;
var brclc = 3;
var brw = 75;
var brh = 20;
var brp = 10;
var brost = 30;
var brosl = 30; 
   
   
   var brs=[];
   
   mblQ(brclc,brrwc,lvl);
   
   /*
   for(c=0;c<brclc;c++){
   brs[c]=[];
   for(r=0;r<brrwc;r++){
   brs[c][r]={x:0,y:0,status:2};
   }
   }//for rows and cols
   */
   function mblQ(brclc,brrwc,nst){//n status or level
       for(c=0;c<brclc;c++){
   brs[c]=[];
   for(r=0;r<brrwc;r++){
   brs[c][r]={x:0,y:0,status:nst};
   }
   }//for rows and cols
   
   }//make bloques
   
   function dbrickS(){
     for(c=0; c<brclc; c++) {
        for(r=0; r<brrwc; r++) {
         if(brs[c][r].status==1){
          var brx=(c*(brw+brp))+brosl;
          var bry=(r*(brh+brp))+brost;
            brs[c][r].x = brx;
            brs[c][r].y = bry;
            co.beginPath();
            co.rect(brx, bry, brw, brh);
            co.fillStyle = "green";
            co.fill();
            co.closePath();
            //drawStar(brx+brw/2,bry+brh/2,5,8,8/2);
         }//if status 1 dibuja
         
         if(brs[c][r].status==2){
          var brx=(c*(brw+brp))+brosl;
          var bry=(r*(brh+brp))+brost;
            brs[c][r].x = brx;
            brs[c][r].y = bry;
            co.beginPath();
            co.rect(brx, bry, brw, brh);
            co.fillStyle = "rgb(175,140,109)";//bronze #a86
            co.fill();
            co.closePath();
            drawStar(brx+brw/2,bry+brh/2,5,8,8/2);
         }//if status 2 dibuja
         
         if(brs[c][r].status==3){
          var brx=(c*(brw+brp))+brosl;
          var bry=(r*(brh+brp))+brost;
            brs[c][r].x = brx;
            brs[c][r].y = bry;
            co.beginPath();
            co.rect(brx, bry, brw, brh);
            co.fillStyle = "rgb(141,166,175)";//silver #8aa
            co.fill();
            co.closePath();
            drawStar(brx+brw/2,bry+brh/2,5,8,8/2);
         }//if status 3 dibuja
         
         if(brs[c][r].status==4){
          var brx=(c*(brw+brp))+brosl;
          var bry=(r*(brh+brp))+brost;
            brs[c][r].x = brx;
            brs[c][r].y = bry;
            co.beginPath();
            co.rect(brx, bry, brw, brh);
            co.fillStyle = "rgb(248,182,76)";//gold#fb6
            co.fill();
            co.closePath();
            drawStar(brx+brw/2,bry+brh/2,5,8,8/2);
         }//if status 4 dibuja
         
         if(brs[c][r].status==5){
          var brx=(c*(brw+brp))+brosl;
          var bry=(r*(brh+brp))+brost;
            brs[c][r].x = brx;
            brs[c][r].y = bry;
            co.beginPath();
            co.rect(brx, bry, brw, brh);
            co.fillStyle = "rgb(74,112,149)";//platinum #479
            co.fill();
            co.closePath();
            drawStar(brx+brw/2,bry+brh/2,5,8,8/2);
         }//if status 1 dibuja
         
        }//for r
    }//for c
   }//dibujar bloques
   
  
   
   
   
   var izqpda = false;//izquierda pisada
   var derpda = false;
   
   document.addEventListener("keydown", keydwnH, false);
document.addEventListener("keyup", keyupH, false);
   
   function keydwnH(e) {
    if(e.keyCode == 39) {
        derpda = true;
    }
    else if(e.keyCode == 37) {
        izqpda = true;
    }
}//abajo handler key

function keyupH(e) {
    if(e.keyCode == 39) {
        derpda = false;
    }
    else if(e.keyCode == 37) {
        izqpda = false;
    }
}//arriba handler key

//con botones
   
   var dpad=26;
   
   function irizQ(){
     //izqpda=true;
     if(px>0){px-=dpad}
   }//ir a izquierda del paddle
   
   function irdeR(){
     //derpda=true;
     
     if(px<cv.width-pw){px+=dpad}
   }//ir a derecha

   function paR(){
     izqpda=false;
     derpda=false;
   }//soltada la pisada
   
   
   //window.addEventListener('touchmove',touchH);
   
   function touchH(e){
     var relx=e.touches[0].screenX-cv.offsetLeft;
     if(relx>0&&relx<cv.width){
       px=relx-pw/2;
     }//if dentro del canvas
   }//toque handler
   
   
   //document.addEventListener("mousemove", mouseMoveH,false);
   
   function mouseMoveH(e){
     var relx=e.clientX-cv.offsetLeft;
     if(relx>0&&relx<cv.width){
       px=relx-pw/2;
     }//if dentro del canvas
   }//mouse move handler
   
   
   var ph=10;//paleta alto
   var pw=75;
   var px=(cv.width-pw)/2;
    
   function dpaL(){
     co.beginPath();
    co.rect(px, cv.height-ph, pw,ph);
    co.fillStyle = "red";
    co.fill();
    co.closePath();
   }//dibujar paddle
   
   function dR(){
   return(Math.floor( (Math.random()*15)+1 ) )/100;//diferencial random
   }//diferencial random
   
   var x=cv.width/2;
   var y=cv.height-20;
   var dx=2+dR(),  dy=-2-dR();
   
   
   var rb=10;
   
   function dboL() {
     
    co.beginPath();
    co.arc(x, y, rb, 0, pi*2);
    co.fillStyle = "blue";
    co.fill();
    co.closePath();
}//dibuja bola

function haychoQ(){
     for(c=0;c<brclc;c++){
       for(r=0;r<brrwc;r++){
         //if(lvl===2){console.log(c,r)};
         if(c===3){break;};
         var b=brs[c][r];
      //calculos
   if(b.status>0){ 
            if(x>b.x&&x<b.x+brw&&y>b.y&&y<b.y+brh){//solo golpe de arriba y de abajo, falta de costado
              
              if(x-dx>b.x&&x-dx<b.x+brw){
              dy=-dy;
              }
              else{dx=-dx}
        
              b.status--;
              score++;
              scorep++;
         if(scorep==brrwc*brclc*lvl){//hacer score parcial
           //alert("You won, congrats!??");
           //alert("ready, for level"+(++lvl));
           lvl++;
           
           if(lvl<6){
            if(lvl<5){alert("You passed this level!??");}   
           var r=confirm("Ready?\n\npress Start! for level "+(lvl)+" "+tlvL(lvl));
           
           if(r==true){
              bi=0;
              //drW();
              scorep=0;
              dpad+=2;
              dx=dx+dR(), dy=dy-dR();
              reposyB();
              drW();
              bt.disabled=false;
             
           }//if ready
           else{
           bi=0;
           drW();
             agaiN();
           }//else not ready
           }//if lvl<6
           else{
               
               alert("Congratualtions, you finished the game!??????\n\n??")
               bi=0;
               lvl--;
               drW();
               btAg.disabled=false;
           }//else your finished
           //document.location.reload();
           //clearInterval(inter);
           //window.cancelAnimationFrame();
           
         } //if score igual a cant de bloques    
              
      }   //if choca
   }//if status 1
         
         
       }//for r
     }//for cols
       
 }//detecta si hay choque
   

   
   
function drW() {
    co.clearRect(0, 0, cv.width, cv.height);
    
    dbrickS();
    dboL();
    dpaL();
    
    dscorE();
    dlvL();
    dliveS();
    
    haychoQ();
  
  //rebota
  //centro saliendo?
  if(x + dx > cv.width-rb || x + dx < rb) {
        dx = -dx;
    }//invierte
    if( y + dy < rb) {//solo el techo
        dy = -dy;
    }//invierte altura
   else if(y + dy > cv.height-rb){
     
     if(x>px&&x<px+pw){dy=-dy}//pega del paddle
     else{
       
       lives--;
       if(!lives){
     btAg.disabled=false;
     alert("game over");
     score=0;
     lives=3;
     bi=0;
         drW();
     //console.log("juego terminado");
   //  document.location.reload();
     //clearInterval(inter);
      //   window.cancelAnimationFrame();
         
       }//if no vidas
       else{
        if(lives>1){
         alert(lives+" lives left");
         }//if mas de dos visas
        else{
           alert(lives+" live left"); 
        }//else 1 vida
         x=cv.width/2;
         y=cv.height-30;
         dx=2+dR();
         dy=-2-dR();
         px=(cv.width-pw)/2;
         
       }//else reposiciona y comienza nueva vida
     }
   }//se va al piso
  
  //movimiento de paddle
  if(derpda&&px<cv.width-pw){px+=7}
  else if(izqpda&&px>0){px-=7}
  
    x += dx;
    y += dy;
  
  if(bi===1){
        
    requestAnimationFrame(drW);
    
  }
  
}//dibuja
   var bi=0;
   drW();
   //var inter=setInterval(drW,10);
  function starT(){
   
bt.disabled=true;
   btAg.disabled=true;//false;
    if(rdT.checked==true){
      window.addEventListener('touchmove',touchH);
      document.addEventListener("mousemove", mouseMoveH,false);
    }//if agrega toque y mouse
    else{
      window.removeEventListener('touchmove',touchH);
      document.removeEventListener("mousemove", mouseMoveH,false);
    }//else quitar eventos
    
    
    bi=1;
    drW();
  }//comenzar
   
   function pausE(){
     
     bi=0;
     bt.disabled=false;
     //btAg.disabled=false;
     
   }//pausa
  
  function agaiN(){
      
      bt.disabled=false;
      btAg.disabled=true;
      
      dpad=26;
      lives=3;
      lvl=1;
      scorep=0;//score parcial
      score=0;
      
     reposyB();
      drW();
    
   }//again
   
   function reposyB(){
       x=cv.width/2;
      y=cv.height-20;
      dx=2+dR(), dy=-2-dR();
      px=(cv.width-pw)/2;
      
      brs=[];
     
      mblQ(brclc,brrwc,lvl);
      
      //drW();
       
   }//reposiciona y hace bloques
   
   
   function drawStar(cx, cy, spikes, outerRadius, innerRadius) {
    var rot = Math.PI / 2 * 3;
    var x = cx;
    var y = cy;
    var step = Math.PI / spikes;

    co.strokeSyle = "red";
    co.beginPath();
    co.moveTo(cx, cy - outerRadius)
    for (i = 0; i < spikes; i++) {
        x = cx + Math.cos(rot) * outerRadius;
        y = cy + Math.sin(rot) * outerRadius;
        co.lineTo(x, y)
        rot += step

        x = cx + Math.cos(rot) * innerRadius;
        y = cy + Math.sin(rot) * innerRadius;
        co.lineTo(x, y)
        rot += step
    }
    co.lineTo(cx, cy - outerRadius)
    co.closePath();
    co.lineWidth=2;
    co.strokeStyle='blue';
    co.stroke();
    co.fillStyle='white';
    co.fill();

}

function tlvL(lvl){
    
    switch(lvl){
        case 2:return "Bronze!";
        case 3:return "Silver!";
        case 4:return "Gold!";
        case 5:return "PLATINUM!"
    }//switch
    
}//nombre del level
   
  </script>
  
  <!-- nota: https://joshondesign.com/p/books/canvasdeepdive/chapter05.html  
  
  -->
</body>
</html>
