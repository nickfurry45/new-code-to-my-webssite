# new-code-to-my-website
HELLO ITS me GARVIT WELCOME TO MY GITHUB ACCOUNT
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Drag Papers ❤️</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Zeyada&display=swap');
    body {
      height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      background-size: cover;
      background-image: url("https://www.w3schools.com/w3images/fjords.jpg"); /* Scenic view background */
      background-position: center center;
      margin: 0;
      padding: 0;
    }
    .paper {
      background-image: url("https://i0.wp.com/textures.world/wp-content/uploads/2018/10/2-Millimeter-Paper-Background-copy.jpg?ssl=1");
      background-size: 500px;
      background-position: center center;
      padding: 20px 100px;
      transform: rotateZ(-5deg);
      box-shadow: 1px 15px 20px 0px rgba(0,0,0,0.5);
      position: absolute;
    }
    .paper.heart {
      position: relative;
      width: 200px;
      height: 200px;
      padding: 0;
      border-radius: 50%;
    }
    .paper.image {
      padding: 10px;
    }
    .paper.image p {
      font-size: 30px;
    }
    img {
      max-height: 200px;
      width: 100%;
      user-select: none;
    }
    .paper.heart::after {
      content: "";
      background-image: url('https://cdn.pixabay.com/photo/2016/03/31/19/25/cartoon-1294994__340.png');
      width: 100%;
      height: 100%;
      position: absolute;
      top: 0;
      left: 0;
      background-size: 150px;
      background-position: center center;
      background-repeat: no-repeat;
      opacity: 0.6;
    }
    p {
      font-family: 'Zeyada';
      font-size: 50px;
      color: rgb(0,0,100);
      opacity: 0.75;
      user-select: none;
    }
  </style>
</head>
<body>
  
  <div class="paper heart"></div>
  
  <div class="paper image">
    <p> and I fallen in</p>
    <p>Love with You 😍</p>
    <img src="C:/IIT M BS/WORK FILES/IIT MADRAS/FINAL/Screenshot 2024-09-23 135216.png" alt="Image 1" />
  </div>
  
  <div class="paper image">
    <p></p>
    <img src="C:/IIT M BS/WORK FILES/IIT MADRAS/FINAL/Screenshot 2024-09-23 135239.png" alt="Image 2" />
  </div>
  
  <div class="paper">
    <p class="p1">Contact me: 9671217538</p>
  </div>
  
  <div class="paper image">
    <p>How can be </p>
    <p> someone so cute ❤️ </p>
    <img src="C:/IIT M BS/WORK FILES/IIT MADRAS/FINAL/WhatsApp Image 2024-09-23 at 15.27.55_bbe9d7f8.jpg" alt="Image 3" />
  </div>
  
  <div class="paper image">
    <p></p>
    <img src="C:/IIT M BS/WORK FILES/IIT MADRAS/FINAL/WhatsApp Image 2024-09-23 at 15.27.56_30e50c0c.jpg" alt="Image 4" />
  </div>

  <!-- "Drag the papers to move!" paper moved to last -->
  <div class="paper">
    <p class="p1">Drag the papers to move!</p>
  </div>

  <script>
    let highestZ = 1;

    class Paper {
      holdingPaper = false;
      mouseTouchX = 0;
      mouseTouchY = 0;
      mouseX = 0;
      mouseY = 0;
      prevMouseX = 0;
      prevMouseY = 0;
      velX = 0;
      velY = 0;
      rotation = Math.random() * 30 - 15;
      currentPaperX = 0;
      currentPaperY = 0;
      rotating = false;

      init(paper) {
        document.addEventListener('mousemove', (e) => {
          if (!this.rotating) {
            this.mouseX = e.clientX;
            this.mouseY = e.clientY;
            this.velX = this.mouseX - this.prevMouseX;
            this.velY = this.mouseY - this.prevMouseY;
          }

          const dirX = e.clientX - this.mouseTouchX;
          const dirY = e.clientY - this.mouseTouchY;
          const dirLength = Math.sqrt(dirX * dirX + dirY * dirY);
          const dirNormalizedX = dirX / dirLength;
          const dirNormalizedY = dirY / dirLength;
          const angle = Math.atan2(dirNormalizedY, dirNormalizedX);
          let degrees = 180 * angle / Math.PI;
          degrees = (360 + Math.round(degrees)) % 360;

          if (this.rotating) {
            this.rotation = degrees;
          }

          if (this.holdingPaper) {
            if (!this.rotating) {
              this.currentPaperX += this.velX;
              this.currentPaperY += this.velY;
            }

            this.prevMouseX = this.mouseX;
            this.prevMouseY = this.mouseY;
            paper.style.transform = `translateX(${this.currentPaperX}px) translateY(${this.currentPaperY}px) rotateZ(${this.rotation}deg)`;
          }
        });

        paper.addEventListener('mousedown', (e) => {
          if (this.holdingPaper) return;
          this.holdingPaper = true;

          paper.style.zIndex = highestZ;
          highestZ += 1;

          if (e.button === 0) {
            this.mouseTouchX = this.mouseX;
            this.mouseTouchY = this.mouseY;
            this.prevMouseX = this.mouseX;
            this.prevMouseY = this.mouseY;
          }

          if (e.button === 2) {
            this.rotating = true;
          }
        });

        window.addEventListener('mouseup', () => {
          this.holdingPaper = false;
          this.rotating = false;
        });
      }
    }

    const papers = Array.from(document.querySelectorAll('.paper'));
    papers.forEach(paper => {
      const p = new Paper();
      p.init(paper);
    });
  </script>
</body>
</html>
