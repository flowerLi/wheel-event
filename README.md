# wheel-event
滚轮事件   
需求：滚轮向上滚，box高度减小
			滚轮向下滚，box高度增加
      ie/chrome : onmousewheel(dom0) 
      firefox : DOMMouseScroll 必须用(dom2的标准模式)

<!DOCTYPE html>
<html>
	<head>
		<meta charset="UTF-8">
		<title></title>
		<style type="text/css">
			*{
				margin: 0;
				padding: 0;
			}
			#box{
				width: 100px;
				height: 100px;
				background: brown;
			}
		</style>
	</head>
	<body style="height: 3000px;">
		<div id="box">
			
		</div>
	</body>
	<script type="text/javascript">
		var box = document.getElementById('box');
		box.onmousewheel = fun;
		if(box.addEventListener){
			box.addEventListener('DOMMouseScroll',fun);
		}
		function fun(ev){
			var ev = ev || event;
			var flag = '';
			if(ev.wheelDelta){
				//ie/chrome
				//console.log(ev.wheelDelta);
				if(ev.wheelDelta>0){
					//向上滚
					flag = 'up';
					//box.style.height = box.offsetHeight - 10 + 'px';
				}else{
					//向下
					flag = 'down';
					//box.style.height = box.offsetHeight + 10 + 'px';
				}
			}else if(ev.detail){
				//firefox
				//.log(ev.detail)
				if(ev.detail>0){
					flag = 'down';
				}else{
					flag = 'up';
				}	
			}
			switch (flag){
				case 'up':
					box.style.height = box.offsetHeight - 10 + 'px';
					break;
				case 'down':
					box.style.height = box.offsetHeight + 10 + 'px';
					break;
			}
			//取消默认行为
			if(ev.preventDefault){
				ev.preventDefault();
			}
			return false;
		}
	</script>
</html>
