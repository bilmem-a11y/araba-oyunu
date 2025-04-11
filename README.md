<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8">
  <title>Basit Araba Oyunu</title>
  <style>
    body {
      margin: 0;
      overflow: hidden;
      background: #333;
    }
    #game {
      position: relative;
      width: 400px;
      height: 600px;
      margin: 20px auto;
      background: #222;
      border: 2px solid #fff;
    }
    #car {
      position: absolute;
      width: 50px;
      height: 100px;
      background: red;
      bottom: 10px;
      left: 175px;
    }
    .obstacle {
      position: absolute;
      width: 50px;
      height: 100px;
      background: yellow;
    }
  </style>
</head>
<body>
  <div id="game">
    <div id="car"></div>
  </div>

  <script>
    const game = document.getElementById("game");
    const car = document.getElementById("car");
    let carX = 175;

    document.addEventListener("keydown", (e) => {
      if (e.key === "ArrowLeft" && carX > 0) {
        carX -= 25;
      } else if (e.key === "ArrowRight" && carX < 350) {
        carX += 25;
      }
      car.style.left = carX + "px";
    });

    function createObstacle() {
      const obs = document.createElement("div");
      obs.classList.add("obstacle");
      obs.style.top = "0px";
      obs.style.left = Math.floor(Math.random() * 350) + "px";
      game.appendChild(obs);

      let moveObs = setInterval(() => {
        let top = parseInt(obs.style.top);
        if (top >= 600) {
          obs.remove();
          clearInterval(moveObs);
        } else {
          obs.style.top = top + 5 + "px";

          // Çarpışma kontrolü
          const carRect = car.getBoundingClientRect();
          const obsRect = obs.getBoundingClientRect();
          if (
            carRect.left < obsRect.right &&
            carRect.right > obsRect.left &&
            carRect.top < obsRect.bottom &&
            carRect.bottom > obsRect.top
          ) {
            alert("Çarpıştın! Oyun bitti.");
            location.reload();
          }
        }
      }, 30);
    }

    setInterval(createObstacle, 1500);
  </script>
</body>
</html>
