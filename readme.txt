Jeu de la vie-------------
Url     : http://codes-sources.commentcamarche.net/source/30376-jeu-de-la-vieAuteur  : coucou747Date    : 06/09/2013
Licence :
=========

Ce document intitulé « Jeu de la vie » issu de CommentCaMarche
(codes-sources.commentcamarche.net) est mis à disposition sous les termes de
la licence Creative Commons. Vous pouvez copier, modifier des copies de cette
source, dans les conditions fixées par la licence, tant que cette note
apparaît clairement.

Description :
=============

un jeu de la vie (tout est expliqu&eacute;)
<br />
<br />Un jeu invent&eacute;
 par MC Conoway.
<br /><a name='source-exemple'></a><h2> Source / Exemple : </h
2>
<br /><pre class='code' data-mode='basic'>
&lt;html&gt;
&lt;head&gt;
&lt
;title&gt;vie artificielle&lt;/title&gt;
&lt;style&gt;

P{
	font-size:10pt;

	color:#000000;
}

P:first-letter {
	font-size:20pt;
	color:#7777FF;
}


.board{
	position: absolute;
	margin-left: 600px;
	margin-top: 5px;
	border
-color:#0077FF;
	color:#000000;
}

.food{
	background-color: rgb(200, 250, 
100);
}

.case{
	background-color: rgb(100, 150, 250);
}

.cellule{
	bac
kground-color: rgb(200, 0, 0);
}

.cellule_dead{
	background-color: rgb(0, 0
, 0);
}
&lt;/style&gt;
&lt;/head&gt;
&lt;body&gt;
&lt;div id=&quot;log&quot
; cols=&quot;50&quot; rows=&quot;7&quot; style=&quot;position:absolute;margin-to
p:5px;margin-left:5px;&quot;&gt;
&lt;/div&gt;
&lt;input type=&quot;button&quot
; id=&quot;acte&quot; value=&quot;stop&quot; onclick=&quot;controle();&quot;  st
yle=&quot;position:absolute;margin-top:105px;margin-left:105px;&quot;/&gt;
&lt;
p style=&quot;position:absolute;margin-top:205px;margin-left:5px;width:550px;&qu
ot;&gt;Ceci est un jeu de la vie ! Le tableau est constitué de cases, ses diment
ions sont de 15*15 cases, (ceci est définit en constantes, mais on peut le chang
er en modifiant les sources, seul deux lignes sont à changer...), chaque case pe
ut contenir une cellule vivante ou morte, de la nouriture ou rien du tout... Les
 cellules se déplacent, elles ne peuvent pas marcher sur de la nouriture, ni sur
 une cellule morte, encore moins sur une autre cellule... Lorsqu'elles trouvent 
de la nouriture, elles commencent à manger, jusqu'a épuisement des stocks. Lorsq
u'elles mangent, elles retrouvent de l'énergie, quand elles se déplacent, elles 
perdent beaucoups d'énergie, quand elles ne font rien, elles en perdent un peu. 
Lorsqu'elles n'ont plus d'énergie, elles meurent, lorsqu'elles en ont plus de 10
0, elles se divisent.&lt;/p&gt;
&lt;script type=&quot;text/javascript&quot;&gt;


const taille_x=15;
const taille_y=15;
var nbr_cellules=5;
var tour=0, sta
rted=1;

cellules=new Array(nbr_cellules);			//le tableau qui contient les cel
lules
tab=new Array(taille_x);				// le tableau qui contient les obstacles
foo
d=new Array(taille_x);				//le tableau qui contient l'emplacement de la nouritur
e

for (i=0;i&lt;taille_x;i++){
	food[i]=new Array(taille_y);
	tab[i]=new Ar
ray(taille_y);
}
function afficher_case_details(vx,vy){
	var i;
	if (tab[vx]
[vy]){
		if (food[vx][vy]){
			alert(&quot;food : &quot;+food[vx][vy]);
		}el
se{
			for (i=0;i&lt;nbr_cellules;i++){
				if (cellules[i].pos_x==vx &amp;&am
p; cellules[i].pos_y==vy){
					alert(cellules[i].details());
				}
			}
		}

	}
}
function controle(){
	/*
	fonction qui permet de faire une pause

<
ul>	<li>/</li></ul>
	if (started==1){
		document.getElementById('acte').value=
&quot;continue&quot;;
		started=0;
	}else{
		document.getElementById('acte').
value=&quot;stop&quot;;
		started=1;
		startmove();
	}
}

function Adn(a,b
,c,d,e){
	/*
	La class ADN

<ul>	<li>/</li></ul>
	this.turn=new Array(4);

	this.want_to_turn=e;
	this.give_turn=Adn_turn;
	this.mute=Adn_muter;
	this.d
etails=Adn_details;
	this.turn[0]=a;
	this.turn[1]=b;
	this.turn[2]=c;
	this
.turn[3]=d;
	return(this);
}

function Adn_details(){
	str=&quot;&quot;;
	
str+=&quot;0=&gt;&quot;+this.turn[0]+&quot;\n&quot;;
	str+=&quot;1=&gt;&quot;+t
his.turn[1]+&quot;\n&quot;;
	str+=&quot;2=&gt;&quot;+this.turn[2]+&quot;\n&quot
;;
	str+=&quot;3=&gt;&quot;+this.turn[3]+&quot;\n&quot;;
	return str;
}

fu
nction Adn_muter(){
	/*
	Fonction qui fait muter l'ADN

<ul>	<li>/</li></ul>

	var e=rnd(5);
	var f=rnd(2)-1;
	if (e&lt;4)
		this.turn[e]+=f;
	else
		t
his.want_to_turn+=f;
}

function Adn_turn(a,b,c,d, direction){
	/*
	les dép
lacements de la cellules sont stoqués dans l'adn

<ul>	<li>/</li></ul>
	var t
abl=new Array(4);
	tabl[0]=a;
	tabl[1]=b;
	tabl[2]=c;
	tabl[3]=d;
	//alert(
&quot; a=&quot;+a+&quot; b=&quot;+b+&quot; c=&quot;+c+&quot; d=&quot;+d);
	var 
chose=-1, e;
	if (a+b+c+d==1){
			if (a==1) chose=0;
			if (b==1) chose=1;
	
		if (c==1) chose=2;
			if (d==1) chose=3;
	}else if (a==1 || b==1 || c==1 || 
d==1){
		if (rnd(this.want_to_turn)!=1 &amp;&amp; tabl[direction]==1){
			chos
e=direction;
		}else{
			while (1)
			{
				e=rnd(4);
				if ( tabl[e]==1 &
amp;&amp; rnd(this.turn[e])==1){ chose=e; break;}
			}
		}
	}
	return chose;

}

function Cellule(pos_x,pos_y, a, b, c, d){
	/*
	La class cellule

<ul
>	<li>/</li></ul>
	this.adn=new Adn(a, b, c, d);
	this.etat=1;
	this.food=50;

	this.pos_x=pos_x;
	this.pos_y=pos_y;
	this.direction=0;
	this.afficher=Cel
lule_afficher;
	this.bouger=Cellule_bouger;
	this.camoufler=Cellule_camoufler;

	this.details=Cellule_details;
	return(this);
}

function Cellule_details(
){
	var str=&quot;&quot;;
	str=(this.etat==1)?&quot;Cellule vivante\n&quot;:&q
uot;Cellule morte\n&quot;;
	str+=&quot;food : &quot;+this.food+&quot;\n&quot;;

	str+=this.adn.details();
	return str;
}

function Cellule_afficher(){
	/*

	la fonction qui permet d'afficher une cellule

<ul>	<li>/</li></ul>
	if (t
his.etat==1)
		document.getElementById('case_x_'+this.pos_x+'_y_'+this.pos_y).s
etAttribute(&quot;class&quot;,&quot;cellule&quot;);
	else
		document.getElemen
tById('case_x_'+this.pos_x+'_y_'+this.pos_y).setAttribute(&quot;class&quot;,&quo
t;cellule_dead&quot;);
	tab[this.pos_x][this.pos_y]=1;
}

function Cellule_c
amoufler(){
	/*
	la fonction qui efface la cellule

<ul>	<li>/</li></ul>
	d
ocument.getElementById('case_x_'+this.pos_x+'_y_'+this.pos_y).setAttribute(&quot
;class&quot;,&quot;case&quot;);
	tab[this.pos_x][this.pos_y]=0;
}

function 
Cellule_bouger(){
	/*
	la fonction qui fait se déplacer la cellule

<ul>	<li
>/</li></ul>
	var retour=0;
	if (this.etat==1){
		var peut_bouger=new Array(4
), i, have_move=1, manger=-1;
		if (this.pos_y!=0)
			if (food[this.pos_x][thi
s.pos_y - 1]!=0)			manger=0;
		if (this.pos_x!=taille_x-1)
			if (food[this.po
s_x + 1][this.pos_y]!=0)			manger=1;
		if (this.pos_y!=taille_y-1)
			if (food
[this.pos_x][this.pos_y + 1]!=0)			manger=2;
		if (this.pos_x!=0)
			if (food[
this.pos_x - 1][this.pos_y]!=0)			manger=3;
		
		if (manger==-1){
			peut_bou
ger[0]=0;
			peut_bouger[1]=0;
			peut_bouger[2]=0;
			peut_bouger[3]=0;
			
if (this.pos_y!=0)
				if (tab[this.pos_x][this.pos_y - 1]==0)			peut_bouger[0]
=1;
			if (this.pos_x!=taille_x-1)
				if (tab[this.pos_x + 1][this.pos_y]==0)
		peut_bouger[1]=1;
			if (this.pos_y!=taille_y-1)
				if (tab[this.pos_x][thi
s.pos_y + 1]==0)		peut_bouger[2]=1;
			if (this.pos_x!=0)
				if (tab[this.pos
_x - 1][this.pos_y]==0)			peut_bouger[3]=1;

			i=this.adn.give_turn(peut_boug
er[0],peut_bouger[1],peut_bouger[2],peut_bouger[3], this.direction);

			switc
h (i){
				case 0 :
					this.pos_y--;
					break;
				case 1 :
					this.p
os_x++;
					break;
				case 2 :
					this.pos_y++;
					break;
				case 3 
:
					this.pos_x--;
					break;
				default :
					have_move=0;
					break
;
			}
			if (i!=-1) this.direction=i;
			
			this.food-=have_move*2+1;

	
	}else{
			this.food+=20;
			switch (manger){
				case 0 :
					food[this.po
s_x][this.pos_y - 1]--;
					if (food[this.pos_x][this.pos_y - 1]==0){
						d
ocument.getElementById('case_x_'+this.pos_x+'_y_'+(this.pos_y-1)).setAttribute(&
quot;class&quot;,&quot;case&quot;);
						tab[this.pos_x][this.pos_y - 1]=0;
	
				}
					break;
				case 1 :
					food[this.pos_x+1][this.pos_y]--;
					i
f (food[this.pos_x+1][this.pos_y]==0){
						document.getElementById('case_x_'+
(this.pos_x+1)+'_y_'+this.pos_y).setAttribute(&quot;class&quot;,&quot;case&quot;
);
						tab[this.pos_x+1][this.pos_y]=0;
					}
					break;
				case 2 :
	
				food[this.pos_x][this.pos_y+1]--;
					if (food[this.pos_x][this.pos_y + 1]
==0){
						document.getElementById('case_x_'+this.pos_x+'_y_'+(this.pos_y+1)).
setAttribute(&quot;class&quot;,&quot;case&quot;);
						tab[this.pos_x][this.po
s_y + 1]=0;
					}
					break;
				case 3 :
					food[this.pos_x-1][this.pos
_y]--;
					if (food[this.pos_x-1][this.pos_y]==0){
						document.getElementB
yId('case_x_'+(this.pos_x-1)+'_y_'+this.pos_y).setAttribute(&quot;class&quot;,&q
uot;case&quot;);
						tab[this.pos_x-1][this.pos_y]=0;
					}
					break;
	
		}
		}
		if (this.food&lt;=0)		//si la cellule doit mourrir...
			this.etat=
0;
		if (100&lt;this.food){		//si la cellule doit se diviser
			this.food-=50;

			retour =1;
		}
	}
	return retour;
}

function startmove(){
	/*
	la 
fonction &quot;main&quot;

<ul>	<li>/</li></ul>
	if (started==1){
		tour++;

		var a=0; log_=&quot;Il y a &quot;+nbr_cellules+&quot; cellules !&lt;br /&gt;&
quot;, en_vie=nbr_cellules, mortes=0;
		for (i=0;i&lt;nbr_cellules;i++){
			ce
llules[i].camoufler();
			a=cellules[i].bouger();
			cellules[i].afficher();

			if (cellules[i].etat==0){
				en_vie--;
				mortes++;
			}
			if (a==1){	
	//fait se diviser la cellule
				cellules[nbr_cellules]=new Cellule(cellules[i
].pos_x,cellules[i].pos_y, cellules[i].adn.turn[0], cellules[i].adn.turn[1], cel
lules[i].adn.turn[2], cellules[i].adn.turn[3], cellules[i].adn.want_to_turn);
	
			cellules[nbr_cellules].adn.mute();
				nbr_cellules++;
				log_+=&quot;La c
ellule &quot;+i+&quot;se divise !&lt;br /&gt;&quot;;
			}
		}
		//affiche le 
log
		log_+=&quot;Nous sommes au tour &quot;+tour+&quot;.&lt;br /&gt;Il y a &qu
ot;+en_vie+&quot;cellules en vie et &quot;+mortes+&quot; cellules mortes...&quot
;;
		document.getElementById(&quot;log&quot;).innerHTML=log_;
		setTimeout('st
artmove();',1000);		//se rapelle
	}
}

function rnd(n){
/*
un nombre au ha
sard

<ul><li>/</li></ul>
	return Math.floor(Math.random()* n);
}

/*
On 
affiche le plateau

<ul><li>/</li></ul>
document.write('&lt;table class=&quot
;board&quot;&gt;');
for (vy=0;vy&lt;taille_y;vy++){
	document.write('&lt;tr&gt
;');
	for (vx=0;vx&lt;taille_x;vx++){
		tab[vx][vy]=0;
		if (rnd(10)==1){
		
	food[vx][vy]=10;
			tab[vx][vy]=1;
			classe=&quot;food&quot;;
		}else{
			
 food[vx][vy]=0;
			 classe=&quot;case&quot;;
		}
		document.write('&lt;td&gt
;&lt;input class=&quot;'+classe+'&quot; id=&quot;case_x_'+vx+'_y_'+vy+'&quot; ty
pe=&quot;text&quot; size=&quot;1&quot; onclick=&quot;afficher_case_details('+vx+
','+vy+');&quot; /&gt;&lt;/td&gt;');
	}
	document.write('&lt;/tr&gt;');
}
do
cument.write('&lt;/table&gt;');
/*
on affiche chaque cellule

<ul><li>/</li>
</ul>
for (i=0;i&lt;nbr_cellules;i++){
	tab[0][i]=1;					//dans tab, on dit si
 la case est OQP
	cellules[i]=new Cellule(0,i, rnd(10)+10, rnd(10)+10, rnd(10)+
10, rnd(10)+10, rnd(10));
	cellules[i].afficher();
}

//commence les déplace
ments
startmove();

&lt;/script&gt;
&lt;/body&gt;
&lt;/html&gt;
</pre>
