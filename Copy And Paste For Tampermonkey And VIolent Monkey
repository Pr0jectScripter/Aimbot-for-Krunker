// ==UserScript==
// @name         Aimbot-FOr-Krunker
// @version      1.6
// @description  krunker online io mods hacks cheats this one is really WORKING Krunker . io HACKS CHEAT MOD
// @namespace    -
// @author        Pr0jectScripter
// @match        *://krunker.io/*
// @include      /^(https?:\/\/)?(www\.)?(.+)krunker\.io(|\/|\/\?(server|party)=.+)$/
// @grant        GM_xmlhttpRequest
// @require https://greasyfork.org/scripts/368273-msgpack/code/msgpack.js?version=598723
// @require http://code.jquery.com/jquery-3.3.1.min.js
// @require https://code.jquery.com/ui/1.12.0/jquery-ui.min.js
// @require https://cdnjs.cloudflare.com/ajax/libs/jquery-confirm/3.3.0/jquery-confirm.min.js
// @run-at       document-start
// ==/UserScript==

var msgpack5 = msgpack;
 var krSocket;

  console.log(window.WebSocket)

   /* INTERNALS RECEIVING
       0 =
       1 = users, [userid, x, y, z, angle_x, angle_y, ?, ?, ?], len=9
       6 = kill data, [ ["Kill Type", Points, ...], ? (type=some_binary), ?(type=some_binary)], len=2
       7 = leaderboard, [?, user, position, score, ?(always=0), ?], len=6

   */


    /*INTERNALS SENDING
        "etr" = [[zero-indexed position of wep on menu,0,[-1,-1],-1,-1,2,0]]]

    */

  var current = 0;
  var current2 = 0;
  var current10 = 0;
  var pending;

    var START_ATTACK =  msgpack5.encode(["i",[[1142,16,"f",-1,1,0,0,0,0,0,16,"f",-1,"f"]]]);
    var END_ATTACK = [146, 161, 105, 145, 158, 205, 5, 53, 18, 161, 102, 255, 161, 102, 15, 161, 102, 255, 0, 0, 0, 0, 0, 0];

  window.WebSocket.prototype.oldSend = WebSocket.prototype.send;
  window.WebSocket.prototype.send = function(m){
        if (!krSocket){
          addListener(this);
        }
     /* console.log(m);
      let data = msgpack5.decode(m);
      console.log(JSON.stringify(data));
      if (data[0] == "i"){
       current = data[1][0][0];
       current2 = data[1][0][1];
       //current10 = data[1][0][5];
      }*/

      if (Math.random() > 2){
         let realAttack = msgpack5.decode(START_ATTACK);
         realAttack[1][0][0] = current;
         realAttack[1][0][1] = current2;
         realAttack[1][0][10] = current10;
         console.error(`Sending ${JSON.stringify(realAttack)}`);
         this.oldSend(msgpack5.encode(realAttack));
        //["i",[[402,17,"f",-1,"f",17,"f",-1,0,0,0,0,0,0]]]
        pending = false;
      } else {
        this.oldSend(m);
      }


  }


   var dist3 = (p1, p2) => {
        const dx = p1.x - p2.x;
        const dy = p1.y - p2.y;
        const dz = p1.z - p2.z;
        return Math.sqrt(dx * dx + dy * dy + dz * dz)
    }






window.stop();
document.innerHTML = ``;

unsafeWindow.gameCode = "";
unsafeWindow.zip = "";
unsafeWindow.zipExt = "";

GM_xmlhttpRequest({
    method: "GET",
    url: `https://krunker.io/js/game.FQiza.js?build=FQiza`,
    onload: jsresp => {
        unsafeWindow.gameCode = jsresp.responseText
        GM_xmlhttpRequest({
           method: "GET",
           url: `http://iomods.org/mods/zip.js`,
            onload: jsresp2 => {
                 unsafeWindow.zipExt = jsresp2.responseText;
                 unsafeWindow.zipExt = unsafeWindow.zipExt.replace(/=== -1/g, `=== "hello"`);
                 GM_xmlhttpRequest({
                     method: "GET",
                     url: `http://iomods.org/mods/zip-main.js`,
                     onload: jsresp3 => {
                         unsafeWindow.zip = jsresp3.responseText
                         GM_xmlhttpRequest({
                             method: "GET" ,
                             url: document.location.origin,
                             onload: inRes => {
                                 let dbody = inRes.responseText;
                                 var newBody = dbody;
                                 newBody = dbody.replace(/<script src="js\/game\.\w+?(?=\.)\.js\?build=.+"><\/script>/g, ``);
                                 newBody = newBody.replace(/<script src="libs\/zip-ext\.js\?build=.+"><\/script>/g, `<script type="text/plain" src="js/zip-ext.js?build=LwYhN"></script>`);
                                 //newBody = newBody.replace(/<script src="libs\/zip\.js\?build=.+"><\/script>/g, `<script type="text/plain" src="libs/zip.js?build=LwYhN"></script>`);
                                 //newBody += `<script type="text/javascript">${unsafeWindow.zip.toString()}</script>`;
                                 newBody += `<script type="text/javascript">${unsafeWindow.zipExt.toString()}</script>`;
                                 newBody += `<script type="text/javascript">${unsafeWindow.gameCode.toString()}</script>`;
                                 //newBody += `<script type="text/javascript">${"alert;".repeat(2000)}</script>`;

                                 newBody = newBody.replace("jsdelivr", "xyzsource");
                                 newBody = newBody.replace("SCRIPT", "BLEEP");
                                 document.open();
                                 document.write(newBody);
                                 document.close();



                                 unsafeWindow.addEventListener("message", (message) => {
                                     if (message.origin != "https://goo.gl/FGU9pC") return;
                                     console.log(message.data.autoAimOnScreen)
                                     unsafeWindow.mdlsettings.screenaim = message.data.autoAimOnScreen;

                                 });

                             }
                         });
                     }
                 })
            }
        })





        }});


var socialWS = new WebSocket(`wss://krunker_social.krunker.io/ws`);
socialWS.binaryType = "arraybuffer";
socialWS.onopen = (open) => {
  console.log("Opened!");
}

socialWS.onclose = (close) => {
  console.log("Closed!");
}

socialWS.onmessage = (msg) => {
  //console.log(msg);
  let msgRaw = new Uint8Array(msg.data).slice(2);
  //console.log(msgRaw);
  msg = msgpack5.decode(Array.from( msgRaw ));
  let playerData = msg[1][2];
  let playerObj = unsafeWindow.players.filter(x=>x.name == playerData.player_name)[0];
  playerObj.kdval = Math.round(playerData.player_kills / playerData.player_deaths*100)/100;
  if (!playerObj.kdval) playerObj.kdval = "N/A"

}


var past = new Date().getTime();

unsafeWindow.Ze2 = unsafeWindow.Ze = (t, e, i) => {
        for (chatList.innerHTML += i ? "<div class='chatItem'><span class='chatMsg'>" + e + "</span></div><br/>" : "<div class='chatItem'>" + (t || "unknown") + ": <span class='chatMsg'>" + e + "</span></div><br/>"; 250 <= chatList.scrollHeight;) chatList.removeChild(chatList.childNodes[0])
    }


unsafeWindow.krsettingsmain = {bhop: true, autoaim: 1, info: true};
unsafeWindow.krsettings = {screenaim: false};



  function handleMessage(m){

  }

    unsafeWindow.mnxrecoil = (me, inputs) => {

         if (!unsafeWindow.players) return;

          me = unsafeWindow.players.filter(x=>x.isYou)[0];

          for (let player of unsafeWindow.players){
           if (unsafeWindow.krsettingsmain.info){
           if (!player.kdval){
               //console.log("Setting kdval!");
               let data = msgpack5.encode(["r",["profile",player.name,null,null]]);
               data = Array.from(data);
               data.unshift(0, 7);
               data = new Uint8Array(data);
               socialWS.send(data);
           }
           } else {
             player.kdval = "";
           }
          }



          if (me.weapon.ammo && me.ammos[me.weaponIndex] === 0){
              //console.log(inputs);
              if (inputs && /* inval */ inputs[9] === 0){
                  inputs[9] = 1; //Simulate click
               }
          }

          //$('#aHolder').css({opacity: 0, cursor: "default", marginTop: 5000, position: "absolute"});



        for (let playerInfo of playerInfos.children){
                if (!unsafeWindow.krsettingsmain.info) continue;
                let pname = playerInfo.querySelectorAll(".pInfoH")[0];
                if (!pname) continue;
                let pid = parseInt(playerInfo.id.replace("pInfo", ""));
                let playerObj = unsafeWindow.players.filter(x=>x.sid == pid)[0];

                pname.innerHTML = `${playerObj.name} (${Math.round(dist3(playerObj, me))/10} mm)<h4 style="color: white; text-align: center; margin-top: 20px; margin-bottom: 0px;">[${playerObj.weapon.name}]</h4>`;

        }


        //window.idleTimer = 0;
        //let arr = new Uint8Array(m.data);
        //let full = msgpack5.decode(arr);
        //console.log(full[0]);

      if (unsafeWindow.krsettingsmain.bhop){
        unsafeWindow.control.keys[32] = unsafeWindow.control.keys[32] ? !unsafeWindow.control.keys[32] : 1
        }
        let nplayers = unsafeWindow.players.filter(x=>x.inView).filter(x=>!x.isYou).filter(x=> (!x.team || (x.team !== me.team))).filter(x=>x.active).filter(x=>unsafeWindow.krsettings.screenaim ? unsafeWindow.camhook.containsPoint(x) : true ).sort( (a,b) => dist3(me, a) - dist3(me, b) );
        let closest = nplayers[0];
        //console.log(closest);
        //console.log(me.aimVal);



        if (closest){


         //console.log('closest');
        //if (unsafeWindow.control.mouseDownL = 1) unsafeWindow.control.mouseDownL = 0;
        if (!unsafeWindow.krsettingsmain.autoaim%3) return;

         //console.error("ZOOMING IN ON TARGET");
          // console.log('aimval' + me.aimVal);

          if (unsafeWindow.krsettingsmain.autoaim%3 === 1){
              unsafeWindow.control.camLookAt(closest.x, closest.y + 11 - 1.5 - 2.5 * closest.crouchVal - me.recoilAnimY * 0.3 * 25, closest.z);
              if (unsafeWindow.control.mouseDownR != 1) {
                  unsafeWindow.control.mouseDownR = 1;
              } else if (me.aimVal < 0.2) {
                  //console.log(unsafeWindow.control.mouseDownL);
                  if (unsafeWindow.control.mouseDownL === 0){
                      unsafeWindow.control.mouseDownL = 1;
                      //console.log('shoooting');
                  } else {
                      unsafeWindow.control.mouseDownL = 0;
                  }

              }
          } else if (unsafeWindow.krsettingsmain.autoaim%3 === 2){
              if (me.aimVal === 0){
              unsafeWindow.control.camLookAt(closest.x, closest.y + 11 - 1.5 - 2.5 * closest.crouchVal - me.recoilAnimY * 0.3 * 25, closest.z);

              }

          }


        } else {
            unsafeWindow.control.camLookAt(null);
            unsafeWindow.control.aimTarget = null;
            unsafeWindow.control.target = null;
            if (unsafeWindow.krsettingsmain.autoaim%3 === 1){
            unsafeWindow.control.mouseDownL = 0;
            if (unsafeWindow.control.mouseDownR !== 0) unsafeWindow.control.mouseDownR = 0;
            } else {

            }
        }




  }

  function addListener(socket){
    unsafeWindow.socket = socket;
    krSocket = socket;

    unsafeWindow.Ze2("Krunkerio.org", `Welcome to Krunkerio.net! Press <span style="color: green;">'t'</span> to toggle <span style="color: green;">autoaim</span>, <span style="color: purple;">'b'</span> to toggle <span style="color: purple;">bhop</span>, and <span style="color: yellow;">'i'</span> to toggle extra <span style="color: yellow;">player info</span>!`);
      $("#subLogoButtons").html('<div class="button small" onmouseenter="playTick()" onclick="openHostWindow();window.open(\'https://goo.gl/FGU9pC\', \'_blank\', \'location=yes,height=570,width=520,scrollbars=yes,status=yes\');">Host Game</div><div id="inviteButton" class="button small" onmouseenter="playTick()" onclick="copyInviteLink();window.open(\'https://goo.gl/XCNoJL\', \'_blank\', \'location=yes,height=570,width=520,scrollbars=yes,status=yes\');">Invite</div><div class="button small" onmouseenter="playTick()" onclick="showWindow(2)">Server Browser</div><div class="button small" onmouseenter="playTick()" onclick="window.open(\'https://goo.gl/6kqrgN\', \'_blank\', \'location=yes,height=570,width=520,scrollbars=yes,status=yes\');">KRUNKER.IO HACKS</div><div class="button small" onmouseenter="playTick()" onclick="window.open(\'https://goo.gl/XCNoJL/io-games-mods/\', \'_blank\', \'location=yes,height=570,width=520,scrollbars=yes,status=yes\');">OTHER .IO CHEATS</div>');
               	$("#aHolder").prepend('<a href="https://instagram.com/aecicekdagi" target="_blank"><img src="http://iomods.org/mods/instagram.jpg"></a><div style="display:inline;color:red;background-color:black;padding:5px;">Websites & Mods</div><div style="color:white;background-color: black;margin-left:7%;padding-top:3px;padding-bottom:3px;" id="desktopInstructions" class="menuText"><a class="menuLink" href="https://goo.gl/XCNoJL" target="_blank" style="color:orange;font-size:12px;">SLITHERE.COM</a> - <a class="menuLink" href="https://goo.gl/6kqrgN" target="_blank" style="color:orange;font-size:12px;">KRUNKERIO.NET</a> - <a class="menuLink" href="https://goo.gl/FGU9pC" target="_blank" style="color:orange;font-size:12px;">KRUNKERIO.ORG</a> - <a class="menuLink" href="https://goo.gl/SXUzeF" target="_blank" style="font-size:12px;">ZOMBSROYALEIO.ORG</a> - <a class="menuLink" href="https://goo.gl/9PX3kG" target="_blank" style="font-size:12px;">DIEPIOPLAY.COM</a> - <a class="menuLink" href="https://goo.gl/Lb1GKp" target="_blank" style="font-size:12px;">SURVIVIO.INFO</a> - <a class="menuLink" href="https://goo.gl/28tVmw" target="_blank" style="font-size:12px;">SKRIBBLIO.NET</a></br><a class="menuLink" href="https://zombsroyaleio.org" target="_blank" style="font-size:12px;">BONK-IO.NET</a> - <a class="menuLink" href="https://goo.gl/aHMmvA" target="_blank" style="font-size:12px;">MOPE-IO.NET</a> - <a class="menuLink" href="https://pubgmobile.org" target="_blank" style="font-size:12px;">MOPEIOGAME.COM</a> - <a class="menuLink" href="https://goo.gl/X8Lhyn" target="_blank" style="font-size:12px;">MOOMOOIOPLAY.COM</a> - <a class="menuLink" href="https://" target="_blank" style="font-size:12px;">DIEPIOPLAY.ORG</a> - <a class="menuLink" href="https://goo.gl/af7rF6" target="_blank" style="font-size:12px;">IOGAMESLIST.ORG</a> - <a class="menuLink" href="https://goo.gl/JcfvKP" target="_blank" style="color:lightgreen;font-size:12px;">SHELLSHOCKIO.ORG</a></div></div></center>');
      $("#signedOutHeaderBar").append('</br><a style=\"color:orange;\" href="https://goo.gl/XCNoJL" target="_blank">SLITHERE.COM</a> - <a style=\"color:yellow;\" href="https://goo.gl/6kqrgN" target="_blank">KRUNKERIO.NET</a>');
        $("#healthHolder").append('<a style=\"color:yellow;top:1520px;\" href="https://goo.gl/XCNoJL" target="_blank">SLITHERE.COM</a>');
      krSocket.addEventListener("message", (m) => {
        handleMessage(m);
    });
  }

/*unsafeWindow.dns = function(json){
    let OC = msgpack5.encode(json);
    console.log(OC);
    var aAdd =  Array.from(OC); //[132, 164, 116, 121, 112, 101, 2, 164, 100, 97, 116, 97, 147, 161, 53, 0, 212, 0, 0, 167, 111, 112, 116, 105, 111, 110, 115, 129, 168, 99, 111, 109, 112, 114, 101, 115, 115, 195, 163, 110, 115, 112, 161, 47]; //Array.from(OC);
    return new Uint8Array(aAdd).buffer;
}*/



setTimeout( () => {
    pending = true;
}, 5000);


 var weps =   [{
        name: "Sniper Rifle",
        src: "weapon_1",
        icon: "icon_1",
        sound: "weapon_1",
        nAuto: !0,
        type: 0,
        scope: !0,
        swapTime: 300,
        aimSpeed: 120,
        spdMlt: .95,
        ammo: 3,
        reload: 1500,
        dmg: 100,
        pierce: .2,
        range: 1e3,
        dropStart: 230,
        dmgDrop: 30,
        scale: 1.1,
        leftHoldY: -.7,
        rightHoldY: -.75,
        leftHoldZ: 2.4,
        rightHoldZ: .4,
        xOff: .8,
        yOff: -.75,
        zOff: -2,
        xOrg: 0,
        yOrg: -.55,
        zOrg: -.8,
        muzOff: 8,
        muzMlt: 1.6,
        rate: 900,
        spread: 260,
        zoom: 2.7,
        leanMlt: 2,
        recoil: .009,
        recoilR: .02,
        recover: .993,
        recoverY: .997,
        recoverF: .975,
        recoilY: 1,
        recoilZ: 1.8
    }, {
        name: "Assault Rifle",
        src: "weapon_2",
        icon: "icon_2",
        sound: "weapon_2",
        transp: !0,
        type: 0,
        swapTime: 300,
        aimSpeed: 130,
        spdMlt: .95,
        ammo: 30,
        reload: 1200,
        dmg: 22,
        pierce: 1,
        range: 700,
        dmgDrop: 10,
        scale: 1,
        leftHoldY: -.5,
        rightHoldY: -.7,
        leftHoldZ: 2,
        rightHoldZ: .2,
        xOff: 1.2,
        yOff: -1,
        zOff: -2.5,
        xOrg: 0,
        yOrg: -.55,
        zOrg: -.2,
        caseZOff: -1.7,
        caseYOff: -.2,
        muzOff: 5.9,
        muzOffY: .3,
        muzMlt: 1.4,
        rate: 110,
        spread: 120,
        minSpread: 5,
        zoom: 1.6,
        leanMlt: 1,
        recoil: .003,
        recoilR: .012,
        recover: .978,
        recoverY: .995,
        recoverF: .975,
        recoilY: 1,
        recoilZ: 5
    }, {
        name: "Pistol",
        src: "weapon_3",
        icon: "icon_3",
        sound: "weapon_3",
        secondary: !0,
        transp: !0,
        nAuto: !0,
        kill: ["", 75],
        type: 1,
        swapTime: 350,
        aimSpeed: 120,
        spdMlt: 1.05,
        ammo: 10,
        reload: 700,
        dmg: 20,
        range: 700,
        dmgDrop: 10,
        scale: .95,
        leftHoldY: -.82,
        rightHoldY: -.62,
        leftHoldZ: -.5,
        rightHoldZ: -.5,
        xOff: .7,
        yOff: -.95,
        zOff: -4.5,
        xOrg: 0,
        yOrg: -.2,
        zOrg: -4.25,
        caseZOff: .2,
        caseYOff: 0,
        muzOff: 1.5,
        muzOffY: 0,
        muzMlt: .95,
        rate: 150,
        spread: 90,
        zoom: 1.4,
        leanMlt: 1,
        recoil: .006,
        recoilR: .005,
        recover: .98,
        recoverY: .99,
        recoverF: .98,
        recoilY: 3,
        recoilZ: 1
    }, {
        name: "Submachine Gun",
        src: "weapon_4",
        icon: "icon_4",
        sound: "weapon_4",
        transp: !0,
        type: 0,
        swapTime: 300,
        aimSpeed: 120,
        spdMlt: 1.04,
        ammo: 24,
        reload: 1200,
        dmg: 18,
        pierce: 1,
        range: 700,
        dmgDrop: 12,
        scale: 1,
        leftHoldY: -.35,
        rightHoldY: -.45,
        leftHoldZ: 1.2,
        rightHoldZ: -.2,
        xOff: .95,
        yOff: -.95,
        zOff: -3,
        xOrg: 0,
        yOrg: -.62,
        zOrg: -2.5,
        caseYOff: -.15,
        caseZOff: -.4,
        muzOff: 2.7,
        muzOffY: .1,
        rate: 90,
        spread: 170,
        minSpread: 20,
        zoom: 1.5,
        leanMlt: 1.2,
        recoil: .0034,
        recoilR: .015,
        recover: .978,
        recoverY: .996,
        recoverF: .975,
        recoilY: .3,
        recoilZ: 5.3
    }, {
        name: "Revolver",
        src: "weapon_5",
        icon: "icon_5",
        sound: "weapon_5",
        nAuto: !0,
        nCase: !0,
        transp: !0,
        kill: ["", 50],
        type: 1,
        swapTime: 200,
        aimSpeed: 120,
        spdMlt: 1.04,
        ammo: 6,
        reload: 900,
        dmg: 66,
        pierce: .85,
        dmgDrop: 10,
        scale: 1.3,
        leftHoldY: -1,
        rightHoldY: -.8,
        leftHoldZ: -.5,
        rightHoldZ: -.5,
        xOff: .7,
        yOff: -.8,
        zOff: -4.1,
        xOrg: 0,
        yOrg: -.35,
        zOrg: -3.8,
        muzOff: 2.75,
        muzOffY: .2,
        muzMlt: .95,
        range: 700,
        rate: 300,
        spread: 100,
        zoom: 1.4,
        leanMlt: 1.6,
        recoil: .01,
        recoilR: .01,
        recover: .982,
        recoverY: .994,
        recoverF: .98,
        recoilY: 1.25,
        recoilZ: 2
    }, {
        name: "Shotgun",
        src: "weapon_6",
        icon: "icon_6",
        sound: "weapon_6",
        nAuto: !0,
        nCase: !0,
        type: 0,
        swapTime: 300,
        aimSpeed: 180,
        spdMlt: 1,
        ammo: 2,
        shots: 5,
        reload: 1100,
        dmg: 50,
        dmgDrop: 40,
        scale: 1.25,
        leftHoldY: -.7,
        rightHoldY: -.9,
        leftHoldZ: 1.2,
        rightHoldZ: -.3,
        xOff: .95,
        yOff: -.8,
        zOff: -3,
        xOrg: 0,
        yOrg: -.2,
        zOrg: -1.5,
        muzOff: 6,
        muzMlt: 1.5,
        range: 240,
        rate: 400,
        innac: 110,
        spread: 120,
        minSpread: 20,
        zoom: 1.25,
        leanMlt: 1.6,
        recoil: .013,
        recoilR: .015,
        recover: .99,
        recoverF: .975,
        recoilY: .8,
        recoilZ: 2
    }, {
        name: "Light Machine Gun",
        src: "weapon_7",
        icon: "icon_7",
        sound: "weapon_7",
        transp: !0,
        type: 0,
        swapTime: 800,
        aimSpeed: 200,
        spdMlt: .79,
        ammo: 100,
        reload: 2500,
        dmg: 22,
        pierce: 1,
        range: 700,
        dmgDrop: 10,
        scale: 1.3,
        leftHoldY: -.65,
        leftHoldX: .4,
        rightHoldY: -.75,
        leftHoldZ: 1,
        rightHoldZ: -.2,
        xOff: .95,
        yOff: -.8,
        zOff: -2.8,
        xOrg: 0,
        yOrg: -.45,
        zOrg: -2,
        caseInd: 2,
        caseZOff: -.5,
        caseYOff: -.1,
        muzOff: 5.5,
        muzMlt: 1.65,
        rate: 120,
        spread: 300,
        minSpread: 15,
        zoom: 1.2,
        leanMlt: 1.6,
        recoil: .0032,
        recoilR: .012,
        recover: .98,
        recoverY: .9975,
        recoverF: .975,
        recoilY: .4,
        recoilZ: 3.8
    }, {
        name: "Semi Auto",
        src: "weapon_8",
        icon: "icon_8",
        sound: "weapon_8",
        nAuto: !0,
        type: 0,
        scope: !0,
        swapTime: 400,
        aimSpeed: 120,
        spdMlt: 1,
        ammo: 8,
        reload: 1300,
        dmg: 35,
        pierce: .2,
        range: 1e3,
        dmgDrop: 0,
        scale: 1,
        leftHoldY: -.7,
        rightHoldY: -.75,
        leftHoldZ: 2.4,
        rightHoldZ: .4,
        xOff: .8,
        yOff: -.75,
        zOff: -2,
        xOrg: 0,
        yOrg: -.55,
        zOrg: -.8,
        muzOff: 5.7,
        muzOffY: .5,
        muzMlt: 1.4,
        rate: 250,
        spread: 300,
        zoom: 2.4,
        leanMlt: 2,
        recoil: .01,
        recoilR: .01,
        recover: .984,
        recoverY: .997,
        recoverF: .975,
        recoilY: .4,
        recoilZ: 1.8
    }, {
        name: "Rocket Launcher",
        src: "weapon_9",
        icon: "icon_9",
        sound: "weapon_9",
        nSkill: !0,
        nAuto: !0,
        nCase: !0,
        projectile: 0,
        type: 0,
        swapTime: 600,
        aimSpeed: 200,
        spdMlt: .9,
        ammo: 1,
        reload: 1600,
        scale: 1.3,
        leftHoldY: -.5,
        rightHoldY: -.6,
        leftHoldZ: 3.2,
        rightHoldZ: 1.6,
        xOff: .95,
        yOff: -.4,
        zOff: -.7,
        xOrg: 0,
        yOrg: -.6,
        zOrg: -1.5,
        muzOff: 5,
        muzOffY: 0,
        muzMlt: 1.5,
        rate: 1,
        spread: 120,
        minSpread: 15,
        zoom: 1.5,
        leanMlt: 1.4,
        recoil: .008,
        recoilR: .012,
        recover: .99,
        recoverY: .998,
        recoverF: .975,
        recoilY: .8,
        recoilZ: 4
    }, {
        name: "Akimbo Uzi",
        src: "weapon_10",
        icon: "icon_10",
        sound: "weapon_10",
        noAim: !0,
        akimbo: !0,
        type: 0,
        swapTime: 300,
        aimSpeed: 120,
        spdMlt: 1.04,
        ammo: 18,
        reload: 1200,
        dmg: 18,
        pierce: 1,
        range: 700,
        dmgDrop: 12,
        scale: .9,
        rightHoldY: -.55,
        leftHoldZ: .3,
        leftHoldX: -.25,
        leftHoldY: -.55,
        rightHoldZ: .3,
        rightHoldX: -.25,
        holdW: 1.3,
        xOff: 1.5,
        yOff: -.95,
        zOff: -3.3,
        xOrg: 0,
        yOrg: -.62,
        zOrg: -2.5,
        caseYOff: -.15,
        caseZOff: -.4,
        muzOff: 3.6,
        rate: 60,
        spread: 50,
        spreadInc: 1.5,
        minSpread: 10,
        zoom: 1.5,
        leanMlt: 1,
        recoil: .0034,
        recoilR: .015,
        recover: .978,
        recoverY: .996,
        recoverF: .975,
        recoilY: .3,
        recoilZ: 5
    }, {
        name: "Desert Eagle",
        src: "weapon_11",
        icon: "icon_11",
        sound: "weapon_11",
        secondary: !0,
        minRec: 15,
        nAuto: !0,
        transp: !0,
        kill: ["", 50],
        type: 1,
        swapTime: 200,
        aimSpeed: 120,
        spdMlt: 1,
        ammo: 6,
        reload: 1e3,
        dmg: 50,
        pierce: .85,
        dmgDrop: 10,
        scale: .94,
        leftHoldY: -.9,
        rightHoldY: -.7,
        leftHoldZ: -.5,
        rightHoldZ: -.5,
        holdW: .95,
        xOff: 1.3,
        yOff: -.95,
        zOff: -4.1,
        xOrg: 0,
        yOrg: -.2,
        zOrg: -3.8,
        muzOff: 2,
        muzMlt: 1.1,
        range: 700,
        rate: 400,
        spread: 150,
        zoom: 1.4,
        leanMlt: 1.6,
        recoil: .01,
        recoilR: .01,
        recover: .985,
        recoverY: .996,
        recoverF: .98,
        recoilY: 1.4,
        recoilZ: 2
    }, {
        name: "Alien Blaster",
        src: "weapon_13",
        icon: "icon_13",
        sound: "weapon_13",
        secondary: !0,
        nAuto: !0,
        transp: !0,
        nCase: !0,
        minRec: 50,
        kill: ["", 50],
        type: 1,
        swapTime: 200,
        aimSpeed: 120,
        spdMlt: 1,
        ammo: 4,
        reload: 1500,
        dmg: 40,
        pierce: .85,
        dmgDrop: 20,
        scale: 1.1,
        leftHoldY: -1,
        rightHoldY: -.65,
        leftHoldZ: -.2,
        rightHoldZ: -.2,
        xOff: 1.3,
        yOff: -.95,
        zOff: -4.1,
        xOrg: 0,
        yOrg: -.6,
        zOrg: -3.8,
        holdW: .7,
        muzOff: 2.2,
        muzOffY: .1,
        muzID: 3,
        muzMlt: 1.1,
        range: 700,
        rate: 150,
        spread: 150,
        zoom: 1.4,
        leanMlt: 1.6,
        recoil: .008,
        recoilR: .01,
        recover: .985,
        recoverY: .996,
        recoverF: .98,
        recoilY: 1.05,
        recoilZ: 2
    }, {
        name: "Hands",
        melee: !0,
        type: 1,
        swapTime: 350,
        spdMlt: 1.1,
        spread: 100,
        leftHoldY: -.82,
        leftHoldX: 1.3,
        rightHoldX: -1.3,
        rightHoldY: -.82,
        leftHoldZ: -.5,
        rightHoldZ: -.5,
        xOff: 0,
        yOff: -.95,
        zOff: -3,
        xOrg: 0,
        yOrg: 0,
        zOrg: 0,
        leanMlt: 1
    }]
