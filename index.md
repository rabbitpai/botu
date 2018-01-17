
<html>

	<head>
		<meta charset="UTF-8">
		<title></title>
		<style>
			#mycanvas {
				border: 1px solid red;
			}
		</style>
	</head>

	<body>
		<canvas id="mycanvas" width="500" height="500">
			
		</canvas>
	</body>
	<script type="text/javascript">
		var rand = (min, max) => parseInt(Math.random() * (max - min) + min);

		var myCanvas = document.querySelector("#mycanvas");
		var ctx = myCanvas.getContext("2d");
		const canvasWidth = myCanvas.width;
		const canvasHeight = myCanvas.height;

		class Ball {
			constructor(ctx, canvasWidth, canvasHeight) {
				this.ctx = ctx;
				this.color = `rgb(${rand(1,256)},${rand(1,256)},${rand(1,256)})`;

				var r = rand(2, 30);
				this.r = r;

				this.x = rand(r, canvasWidth - r);
				this.y = rand(r, canvasHeight - r);

				this.maxWidth = canvasWidth - r;
				this.maxHeight = canvasHeight - r;

				var speedx = rand(2, 6);
				this.speedx = rand(0, 2) > 0 ? speedx : -speedx;
				var speedy = rand(2, 6);
				this.speedy = rand(0, 2) > 0 ? speedy : -speedy;
			}
			draw() {
				this.ctx.beginPath();
				this.ctx.fillStyle = this.color;
				this.ctx.arc(this.x, this.y, this.r, 0, Math.PI * 2, true);
				this.ctx.closePath();
				this.ctx.fill();
			}
			move() {
				this.x += this.speedx;
				if(this.x >= this.maxWidth) {
						this.speedx*=-1;
						
				}else if(this.x < this.r){
					this.speedx*=-1;
				}
				
				this.y += this.speedy;
				if(this.y >= this.maxHeight) {
						this.speedy*=-1;
						
				}else if(this.y < this.r){
					this.speedy*=-1;
				}
				
			}
		}
		var balls = [];
		for(var i = 0; i < 555; i++) {
			var ballnum = new Ball(ctx, canvasWidth, canvasHeight);
			balls.push(ballnum);
		}
		
		setInterval(function(){
			ctx.clearRect(0,0,canvasWidth,canvasHeight);
			
			for(var i = 0; i < balls.length; i++) {
			balls[i].draw();
			balls[i].move();
		}
		},30);
		
	</script>

</html>
