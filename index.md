## Track Your Initiative Below 
> Input character name and initiative.

<body>
<style>
custom-field input {
  border: 2px solid darkgrey;
  -webkit-appearance: none;
  -ms-appearance: none;
  -moz-appearance: none;
  appearance: none;
  background: #f2f2f2;
  padding: 12px;
  border-radius: 10px;
  width: 250px;
  font-size: 14px;
}
</style>
<style>
.center {
  margin: auto;
  width: 60%;
  border: 3px solid  #FFD133;
  padding: 10px;
}
.sortTitle {
  margin: auto;
  border: 3px solid  gray;
  padding: 12px;
  margin-bottom: 15px;
  margin-top: 15px;
  font-family: "Papyrus";
  font-size: 24px;
  text-align: center;
}
.playerBody {
  margin: auto;
  background-color: black;
  border: 3px solid  #FFC133;
  padding: 12px;
  width: 1000px;
  background: #f2f2f2;
}
.position1 {
  position: absolute;
  top: 765;
  background-color: black;
  border: 0px solid  gray;
  padding: 12px;
  width: 550px;
  background: #242423;
}
.position2 {
  position: absolute;
  top: 785;
  left: 0;
  right: 0;
  margin: 0 auto;
  color: white;
  border: 0px solid  gray;
  padding: 12px;
  width: 550px;
  background: #242423;
}
.position3 {
  position: absolute;
  top: 765;
  right: 0;
  color: white;
  border: 0px solid  gray;
  padding: 12px;
  width: 550px;
  background: #242423;
}
.sortText {
  font-family: "Papyrus";
  font-size: 24px;
  border: 3px solid  #FFD133;
}
.shifted {
  margin: auto;
  border: 3px solid  #FFD133;
  padding: 10px;
}
</style>
    <form>
        <custom-field class="formBox">
            <label for="name">Name</label>
            <input type="text" id="name" placeholder="Name"/>
        </custom-field>
        <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</p>
        <custom-field class="formBox">
            <label for="initiative">Initiative Roll</label>
            <input type="number" id="initiative" min="-40" max="40" step="1" placeholder="Initiative Roll"/>
        </custom-field>
        <p>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</p>
        <custom-field class="formBox">
            <button id="btn">Click to Add</button>
        </custom-field>
        <button onclick="logSort()">Display Initiative</button>
        <button onclick="clearInitiative()">Clear</button>
        <button onclick="removeInitiative()">Remove From Initiative</button>
    </form>
    <script>
        let players = [];
        // example {id:1592304983049, title: 'Avengers: Endgame', initiative: 'good action scenes.'}
        const addPlayer = (ev)=>{
            ev.preventDefault();  //stops the form submitting automatically
            let player = {
                id: Date.now(),
                name: document.getElementById('name').value,
                initiative: document.getElementById('initiative').value
            }
           players.push(player);
            document.forms[0].reset(); // to clear the form for the next entries
            console.warn('added' , {players} ); // displays array in the console
            //saving to localStorage
            localStorage.setItem('MyPlayerList', JSON.stringify(players) );
            //Addplayer()
        };
        document.addEventListener('DOMContentLoaded', ()=>{
            document.getElementById('btn').addEventListener('click', addPlayer);
        });
        function Addplayer() {
            var playerindex = players.length - 1;
            console.log(players[playerindex].name);
            const newDiv = document.createElement("div");
            newDiv.innerText = "Player: " + players[playerindex].name + "\nComments: " + players[playerindex].initiative
        }
        const titleDiv = document.createElement("div");
                    titleDiv.classList.add('sortTitle'); 
                    titleDiv.innerText = "Initiative Order Displayed Below:"
                    document.body.appendChild(titleDiv);
                const initDiv1 = document.createElement("div");
                    initDiv1.classList.add('position1'); 
                    document.body.appendChild(initDiv1);
                const initDiv2 = document.createElement("div");
                    initDiv2.classList.add('position2'); 
                    document.body.appendChild(initDiv2);
                const initDiv3 = document.createElement("div");
                    initDiv3.classList.add('position3'); 
                    document.body.appendChild(initDiv3);
        // Creating Body
        function increaseFontSize() {
        document.getElementById('a').style.fontSize = "50px";
        }
        function sortPlayers(array, valueKey) {
                event.preventDefault();
                array.sort((a, b) => b[valueKey] - a[valueKey]);
              }      
              function logSort() {
                event.preventDefault();
                sortPlayers(players, 'initiative');
                console.log(players);
                // Sort the array of dictionaries by the 'name' 
                //var sortedData = sortPlayers(players, 'initiative');        
                // Display the sorted data in the console
                //console.log(sortedData);  
                for (var i=0, j=i+1;i<players.length;i+=1) {
                    let j = 1 + i;
                    const g = String(j)
                    let count = g.fontsize(8);
                    const r = String(players[i].initiative);
                    let roll = r.fontsize(8);
                    console.log(players[i].name); // shows each player displayed in console
                    const sortDiv = document.createElement("div");
                    sortDiv.classList.add('sortText')
                    sortDiv.innerHTML =  "Name: " + players[i].name + "<br />" + "Count: " + count + "<br />" + "\nInitiative: " + roll;
                    if (i < 4) {
                      initDiv1.appendChild(sortDiv);
                    }
                    else if (i < 8) {
                     initDiv2.appendChild(sortDiv);
                    }
                    else {
                    initDiv3.appendChild(sortDiv);
                    }
                 } 
                }
        function removeAllChildNodes(parent) {
         event.preventDefault()
         while (parent.firstChild) {
            parent.removeChild(parent.firstChild);
         }
        }
        function clearInitiative() {
          event.preventDefault()
          removeAllChildNodes(initDiv1)
          removeAllChildNodes(initDiv2)
          removeAllChildNodes(InitDiv3)
          console.log(players)
        }
        function findNameIndex(arraytosearch, key, valuetosearch) {
        for (var i = 0; i < arraytosearch.length; i++) {
        if (arraytosearch[i][key] == valuetosearch) {
        return i;
        }
        }
        return null;
        }
        function removeInitiative() {
         event.preventDefault()
         var index = findNameIndex(players, "name", document.getElementById('name').value);
         console.log(index);
         const x = players.splice(index, 1);
         console.log(players);
         clearInitiative();
        }
    </script>
</body>