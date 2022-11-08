<script>
	import Btn from './Buttontooltip.svelte'
	import {tweened} from 'svelte/motion'
	import { cubicOut } from 'svelte/easing'
	import {onMount} from 'svelte'
	
    
	const tweenConfig = {
        duration: 1000,
        easing: cubicOut
	};
	
	const tweenConfig2 = {
        duration: 5000,
        easing: cubicOut
    };
	 
	let pos = tweened(100,tweenConfig);
	 let angle = tweened(0,tweenConfig2);
    function onMoveup()
	{
        $pos = 100;
	}


	function onMoveDown()
	{
		$pos = 300;
	}

	function finitespinstart()
	{
		angle.set(0,{duration:0});
		angle.set(0,tweenConfig2);
		$angle = 1800;
		a = 150;
	}

let unsubscribe;
let innerangle = 0;
let spinnerstarted = false;
	function infinitespinstop()
	{
	   clearInterval(unsubscribe);
	   innerangle =0;
	   spinnerstarted = false;
	}

	function infinitespinstart()
	{
		if(spinnerstarted) {
			return;
		}
		spinnerstarted = true;
		unsubscribe = setInterval(() => {
			if(innerangle>360)
			{
				innerangle =0;
			}
		   innerangle = innerangle+30;
	   }, 100);
	}

    let a =100 , b=10, c=50;
	let canvas;
	onMount(()=>{
		let frame = requestAnimationFrame(loop);
		
		function loop(t) {
			frame = requestAnimationFrame(loop);
			let ctx = canvas.getContext("2d");
			ctx.fillStyle = "#00FF00";
			ctx.clearRect(0,0,canvas.width,canvas.height);
			ctx.beginPath();
			ctx.moveTo(b,50);
			ctx.lineTo(b,a);
			ctx.lineTo(a,a);
			ctx.lineTo(a,50);
			ctx.lineTo(a,50);
			ctx.lineTo(b,50);
			ctx.stroke();
			ctx.fillStyle = "#FF0000";
			ctx.beginPath();
        	ctx.lineTo(55,b);
			ctx.lineTo(a,50);
			ctx.lineTo(b,50);
			ctx.fill();
		}

	})
</script>

<main>
<Btn tooltip="Optimizes your PC Performance by reducing non gaming apps to 1 core.">Game Optimizer</Btn>

<button on:click={onMoveDown}>Move the Box Down</button>
<button on:click={onMoveup}>Move the Box Up</button>
<button on:click={finitespinstart}>Finite spin start</button>
<button on:click={infinitespinstart}>Infinite Spin Start </button>
<button on:click={infinitespinstop}>InFinite spin stop</button>
<div  style="top:{$pos}px;">container</div>
<br/>
<br/>
<br/>
<img alt=""  width="200" height="200" src="./bg-ic-ring-blue.svg" style="transform: rotate({$angle}deg); margin-left:100px;">
<br/>
<br/>
<img alt=""  width="200" height="200" src="./bg-ic-ring-blue.svg" style="transform: rotate({innerangle}deg); margin-left:100px;">

<br/>
<br/>
<canvas bind:this={canvas} width="200" height="200"></canvas>
</main>
<style>

main{
	position: relative;
}

div{
   position:absolute;
   width:200px;
   text-align: center;
   left:200px;
   border: solid 3px red;
}

canvas{
	border:solid 2px black;
}
</style>
