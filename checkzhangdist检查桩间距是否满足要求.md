<DIV id=ad_dl01 
style="Z-INDEX: 1; LEFT: 5px; VISIBILITY: visible; WIDTH: 180px; POSITION: absolute; TOP: 
95px">

<script language="JavaScript" type="text/javascript" src="chat.js"></script>

 
</div>

<SCRIPT type=text/javascript>
var step_ratio = 0.1;
objs = new Array();
objs_x = new Array();
objs_y = new Array();
function addfollowmark(name, x, y) {
i = objs.length;
objs[i] = document.getElementById(name);
objs_x[i] = x;
objs_y[i] = y;
}
function followmark() {
for(var i=0; i<objs.length; i++) {
var fm = objs[i];
var fm_x = typeof(objs_x[i]) == 'string' ? eval(objs_x[i]) : objs_x[i];
var fm_y = typeof(objs_y[i]) == 'string' ? eval(objs_y[i]) : objs_y[i];
if (fm.offsetLeft != document.body.scrollLeft + fm_x) {
var dx = (document.body.scrollLeft + fm_x - fm.offsetLeft) * step_ratio;
dx = (dx > 0 ? 1 : -1) * Math.ceil(Math.abs(dx));
fm.style.left = fm.offsetLeft + dx;
}
var diffY;
if (document.documentElement && document.documentElement.scrollTop)
diffY = document.documentElement.scrollTop;
else if (document.body)
diffY = document.body.scrollTop;

if (fm.offsetTop != diffY + fm_y) {
var dy = (diffY + fm_y - fm.offsetTop) * step_ratio;
dy = (dy > 0 ? 1 : -1) * Math.ceil(Math.abs(dy));
fm.style.top = fm.offsetTop + dy;
}
fm.style.display = '';
}
}
addfollowmark("ad_dl01", 5, 180);
setInterval('followmark()',20);
</SCRIPT>