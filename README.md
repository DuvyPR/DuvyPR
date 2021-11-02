
/*
* Made by: UndercoverGoose
* Version: 1.9
*/
(function(){
  console.debug("%cRunning Gimkit Hack V1.9", "color:#FF5555;font-size:20px;");
  
  // Function/Variables to simplify the creation, appending, and getting of objects/elements
  let cN = "hckcntnt";
  let d = "div";
  let a3 = "#33aa33";
  let a33 = "#aa3333";
  let balanceChanges = [];
  let balanceTimes = [];
  function gcn(x,y){return document.getElementsByClassName(x)[y]}
  function cre(t,c,s,i){let x=document.createElement(t);x.className=c,x.style=s,x.innerHTML=i;return x;}
  function app(v){document.body.appendChild(v)}
  function appd(v){document.getElementsByClassName(cN)[1].appendChild(v)}
  function apps(v){document.getElementsByClassName(cN)[7].appendChild(v)}
  function appup(v){document.getElementsByClassName('sc-dUjcNx cMoWkD')[0].appendChild(v)}

  // Applies default button color and look without having to purchase an upgrade to update the style
  let newstyle = document.createElement('style');
  newstyle.textContent='.fkLxCm {box-sizing: border-box;font-size: 17px;color: white;font-weight: bold;text-align: center;display: inline-block;user-select: none;cursor: pointer;padding: 12px 16px;background: rgb(0, 85, 255);transition: background 0.2s ease 0s;border-radius: 4px;font-family: "Product Sans", sans-serif;}';
  app(newstyle);
  
  let qs = [],
      as = [];
  let list = [];
  for(let x=0;x<JSON[Object.keys(JSON)[0]].length;x++) {
    list.push(parseInt(JSON[Object.keys(JSON)[0]][x]["_id"].slice(19,99),16))
  }
  list.sort()
  let gameID = (JSON[Object.keys(JSON)[0]][0]["_id"].slice(0, 19) + (list[0] - 1).toString(16));
  let r = new XMLHttpRequest();
  r.open('GET', `https://www.gimkit.com/api/games/fetch/${gameID}`);
  r.onreadystatechange = function() { 
    if (r.readyState == 4 && r.status == 200) {
      let json = JSON.parse(r.responseText);
      for(let x=0;x<(json.kit.questions).length;x++) {
        qs.push(json.kit.questions[x].text);
        as.push(json.kit.questions[x].answers[0].text);
      }
    }
  }
  r.send();
  
  
  // Cheat toggles and "Menu" button creation
  let f = [0, 0, 0, 0, 0, 0];
  let hconfig = {
    keybinds:{
      hidemenu: 67, // c:67
      highlight: 72, // h:72
      biganswer: 66, // b:66
      inputanswer: 73, // i:73
      hiddenanswer: 79 // o:79
    },
    theme:{
      active:"default",
      default:[[48,63,159],[119,19,34],[168,92,21],[13,107,51],[7,98,150]],
      night:[[0,10,18],[38,50,56],[55,71,79],[69,90,100],[84,110,122]],
      thanos:[[13,0,25],[34,0,68],[51,0,102],[62,0,124],[79,23,135]],
      ocean:[[0,0,99],[40,53,147],[7,98,150],[2,119,189],[21,101,192]],
      forest:[[76,61,51],[56,86,69],[66,92,73],[65,86,65],[76,99,73]],
      sunset:[[127,116,150],[224,111,90],[237,113,45],[122,89,106],[232,171,60]],
      retro:[[156,0,34],[0,29,59],[255,174,82],[254,89,99],[167,28,148]],
      gold:[[0,0,0],[255,205,43],[255,199,33],[255,209,71],[255,205,56]]
    },
    upgrades:{
      money:[0,10,100,1e3,1e4,75e3,3e5,1e6,1e7,1e8],
      streak:[0,15,150,1500,15e3,115e3,45e4,15e5,15e6,2e8],
      multi:[0,50,300,2e3,12e3,85e3,7e5,65e5,65e6,1e9],
      protec:[0,10,250,1e3,25e3,1e5,1e6,5e6,25e6,5e8]
    }
  }
  let btnattr={
    style:"width:200px;height:40px;margin-top:3px;background:#aa3333",
    class:"sc-bdVaJa fkLxCm hckcntnt"
  }

  let b = cre(d,btnattr.class,"position: fixed; z-index: 1000000; left: 5px; bottom: 5px; width: 100px; height: 40px;","Menu");
  b.onclick=function(){if(f[0]===0){gcn(cN,1).style.display="block",f[0]=1,gcn(cN,0).innerHTML="X",gcn(cN,0).style.background="#ff0000";}else{gcn(cN,1).style.display="none",f[0]=0,gcn(cN,0).innerHTML="Menu",gcn(cN,0).style.background="";}};
  app(b);

  // Area for cheat buttons
  app(cre(d,btnattr.class,"position:fixed;z-index:10000;left:5px;bottom:5px;width:300px;height:600px;display:none",""));

  // Toggles/creates highlight answers cheat
  let h = cre(d,btnattr.class,btnattr.style,"Highlight Answers");
  h.onclick=function(){if(f[1]===0){gcn(cN,2).style.background=a3;f[1]=1;hlinterval=setInterval(highlight,0);}else{gcn(cN,2).style.background=a33;f[1]=0;clearInterval(hlinterval);}}
  appd(h);

  // Toggles/creates big answer cheat
  let ab = cre(d,btnattr.class,btnattr.style,"Big Answer Box");
  ab.onclick=function(){if(f[2]===0){gcn(cN,3).style.background=a3;f[2]=1;bainterval=setInterval(biganswer,0);}else{gcn(cN,3).style.background=a33;f[2]=0;clearInterval(bainterval);}}
  appd(ab);

  // Toggles/creates input answer cheat
  let ia = cre(d,btnattr.class,btnattr.style,"Input Answer");
  ia.onclick=function(){if(f[3]===0){gcn(cN,4).style.background=a3;f[3]=1;iainterval=setInterval(inputanswer,0);}else{gcn(cN,4).style.background=a33;f[3]=0;clearInterval(iainterval);}}
  appd(ia);

  // Toggles/creates hidden answer cheat
  let ha = cre(d,btnattr.class,btnattr.style,"Hidden Answer");
  ha.onclick=function(){if(f[5]===0){gcn(cN,5).style.background=a3;f[5]=1;hainterval=setInterval(hiddenanswer,0);}else{gcn(cN,5).style.background=a33;f[5]=0;clearInterval(hainterval);document.title="Play Gimkit! - Enter game code here";}}
  appd(ha);

  // Creates settings button
  let se = cre(d,btnattr.class,"width:170px;height:40px;margin-top:3px;background:#333333;position:absolute;bottom:0px;right:0px","Settings");
  se.onclick=function(){if(f[6]===0){gcn(cN,7).style.display="block";f[6]=1;}else{f[6]=0;gcn(cN,7).style.display="none";}}
  appd(se);

  // Creates Session Stealer Button
  let ssb = cre(d,"sc-bdVaJa fkLxCm",btnattr.style,"Session Stealer");
  ssb.onclick=function(){stealSession()};
  appd(ssb);

  // Creates Upgradeable Upgrade Display
  let autoclass = "sc-bdVaJa fkLxCm autoUp";

  let automoney = cre(d,autoclass,btnattr.style+";position:absolute;margin-left: 100px;font-size:12px","Money: Level ? for $?");
  appup(automoney);

  let autostreak = cre(d,autoclass,btnattr.style+";position:absolute;margin-left:300px;font-size:12px","Streak: Level ? for $?");
  appup(autostreak);

  let automulti = cre(d,autoclass,btnattr.style+";position:absolute;margin-left:500px;font-size:12px","Multi: Level ? for $?");
  appup(automulti);

  let autoprotec = cre(d,autoclass,btnattr.style+";position:absolute;margin-left:700px;font-size:12px","Protec: Level ? for $?");
  appup(autoprotec);
  
  let lvl = {
      money: 0,
      streak: 0,
      multi: 0,
      protec: 0
    }
  function autowhatever(){
    let bal = document.getElementsByTagName(d)[9].innerHTML.split(",").join("").split("$").join("");
    let shrink = document.getElementsByClassName('autoUp');
    let hc = hconfig.upgrades;

    if(typeof document.getElementsByClassName('sc-bdVaJa Harxh')[0] !== "undefined"){
      if(document.getElementsByClassName('sc-bdVaJa Harxh')[0].childNodes[0].childNodes[0].innerHTML === "Money Per Question"){
        for(let x=0;x<10;x++) {
          if(document.getElementsByClassName('sc-eXEjpC joQyGL')[x].innerHTML.lastIndexOf('gray') > -1 && x + 1 > lvl.money) {
            lvl.money = x + 1;
          }
        }
      }else if(document.getElementsByClassName('sc-bdVaJa Harxh')[0].childNodes[0].childNodes[0].innerHTML === "Streak Bonus") {
        for(let x=0;x<10;x++) {
          if(document.getElementsByClassName('sc-eXEjpC joQyGL')[x].innerHTML.lastIndexOf('gray') > -1 && x + 1 > lvl.streak) {
            lvl.streak = x + 1;
          }
        }
      }else if(document.getElementsByClassName('sc-bdVaJa Harxh')[0].childNodes[0].childNodes[0].innerHTML === "Multiplier") {
        for(let x=0;x<10;x++) {
          if(document.getElementsByClassName('sc-eXEjpC joQyGL')[x].innerHTML.lastIndexOf('gray') > -1 && x + 1 > lvl.multi) {
            lvl.multi = x + 1;
          }
        }
      }else if(document.getElementsByClassName('sc-bdVaJa Harxh')[0].childNodes[0].childNodes[0].innerHTML === "Amount Covered") {
        for(let x=0;x<10;x++) {
          if(document.getElementsByClassName('sc-eXEjpC joQyGL')[x].innerHTML.lastIndexOf('gray') > -1 && x + 1 > lvl.protec) {
            lvl.protec = x + 1;
          }
        }
      }
    }
    try{
      if(lvl.money < 10) {
        shrink[0].innerHTML = "Money: Level " + (lvl.money + 1) + " for $" + hc.money[lvl.money];
        if(bal >= hc.money[lvl.money]) {
          shrink[0].style.background = a3;
        }else {
          shrink[0].style.background = a33;
        }
      }else {
        shrink[0].innerHTML = "MAX";
      }
      if(lvl.streak < 10) {
        shrink[1].innerHTML = "Streak: Level " + (lvl.streak + 1) + " for $" + hc.streak[lvl.streak];
        if(bal >= hc.streak[lvl.streak]) {
          shrink[1].style.background = a3;
        }else {
          shrink[1].style.background = a33;
        }
      }else {
        shrink[1].innerHTML = "MAX";
      }
      if(lvl.multi < 10) {
