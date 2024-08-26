Prasunet_Code_TaskNo.03.HTML
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tic-Tac-Toe</title>
  <link rel="stylesheet" href="style.css">
</head>

<body>
  <div class="main">
      <div class="players">
          <div class="player">
              <h2>Player 1</h2>
              <div class="player__symbol">X</div>
          </div>
          <div class="player">
              <h2>Player 2</h2>
              <div class="player__symbol">O</div>
          </div>
      </div>
      <div class="board-container">
          <div class="board">
              <button class="board__cell" data-cell-index="1"></button>
              <button class="board__cell" data-cell-index="2"></button>
              <button class="board__cell" data-cell-index="3"></button>
              <button class="board__cell" data-cell-index="4"></button>
              <button class="board__cell" data-cell-index="5"></button>
              <button class="board__cell" data-cell-index="6"></button>
              <button class="board__cell" data-cell-index="7"></button>
              <button class="board__cell" data-cell-index="8"></button>
              <button class="board__cell" data-cell-index="9"></button>
          </div>
      </div>

      <button class="game-restart-btn">Restart Game</button>
      <div class="popup hide">
          <p id="message">Sample Message</p>
          <button class="popup__restart-btn">New Game</button>
      </div>

  </div>

  <script src="game.js"></script>
</body>

</html>
Prasunet_Code_TaskNo.03..CSS

// This function is executed when a player wins
const winFunction = (letter) => {
  disableButtons();
  if (letter == "X") {
      msgRef.innerHTML = "&#x1F389; <br> 'X' Wins";
  } else {
      msgRef.innerHTML = "&#x1F389; <br> 'O' Wins";
  }
};
//Function for draw
const drawFunction = () => {
  disableButtons();
  msgRef.innerHTML = "&#x1F60E; <br> It's a Draw";
};
//New Game
newgameBtn.addEventListener("click", () => {
  count = 0;
  enableButtons();
});
restartBtn.addEventListener("click", () => {
  count = 0;
  enableButtons();
});
//Win Logic
const winChecker = () => {
  //Loop through all win patterns
  for (let i of winningPattern) {
      let [element1, element2, element3] = [
          btnRef[i[0]].innerText,
          btnRef[i[1]].innerText,
          btnRef[i[2]].innerText,
      ];
      //Check if elements are filled
      //If 3 empty elements are same and would give win as would
      if (element1 != "" && (element2 != "") & (element3 != "")) {
          if (element1 == element2 && element2 == element3) {
              //If all 3 buttons have same values then pass the value to winFunction
              winFunction(element1);
          }
      }
  }
};
//Display X/O on click
btnRef.forEach((element) => {
  element.addEventListener("click", () => {
      if (xTurn) {
          xTurn = false;
          //Display X
          element.innerText = "X";
          element.disabled = true;
      } else {
          xTurn = true;
          //Display Y
          element.innerText = "O";
          element.disabled = true;
      }
      //Increment count on each click
      count += 1;
      if (count == 9) {
          drawFunction();
      }
      //Check for win on every click
      winChecker();
  });
});
//Enable Buttons and disable popup on page load
window.onload = enableButtons;
