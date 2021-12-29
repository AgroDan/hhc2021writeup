# RPC Enumeration

I can enumerate users using the rpc client!

on the elfu server, I ran:

`rpcclient 10.128.3.30`

Then logged in with my user. I dumped the following users with the command `enumdomusers`!

```
user:[Administrator] rid:[0x1f4]
user:[Guest] rid:[0x1f5]
user:[krbtgt] rid:[0x1f6]
user:[admin] rid:[0x3e8]
user:[elfu_admin] rid:[0x450]
user:[elfu_svc] rid:[0x451]
user:[remote_elf] rid:[0x452]
user:[ulyssesross] rid:[0x455]
user:[bobolson] rid:[0x457]
user:[raulpenrod] rid:[0x459]
user:[charleneneptune] rid:[0x45b]
user:[xavierzebra] rid:[0x45d]
user:[victoriacharles] rid:[0x45f]
user:[paulyankee] rid:[0x461]
user:[ulyssestrebek] rid:[0x463]
user:[lukeyankee] rid:[0x465]
user:[paulhankerson] rid:[0x467]
user:[quincyjones] rid:[0x469]
user:[maryhankerson] rid:[0x46b]
user:[ulyssespenrod] rid:[0x46d]
user:[charlenesmith] rid:[0x46f]
user:[ulysseslovering] rid:[0x471]
user:[hankqueior] rid:[0x473]
user:[ednamoss] rid:[0x475]
user:[hankgeorge] rid:[0x477]
user:[yolandayankee] rid:[0x479]
user:[wandaneptune] rid:[0x47b]
user:[forrestvictoria] rid:[0x47d]
user:[jorgetrebek] rid:[0x47f]
user:[zeldaellis] rid:[0x481]
user:[samanthazebra] rid:[0x483]
user:[noahgeorge] rid:[0x485]
user:[quincycharles] rid:[0x487]
user:[paulvictoria] rid:[0x489]
user:[xavierirving] rid:[0x48b]
user:[wandayankee] rid:[0x48d]
user:[yolandaabbott] rid:[0x48f]
user:[victoriageorge] rid:[0x491]
user:[forrestcharles] rid:[0x493]
user:[opheliaolson] rid:[0x495]
user:[xavierdruidia] rid:[0x497]
user:[gildapenrod] rid:[0x499]
user:[opheliakilleen] rid:[0x49b]
user:[bobross] rid:[0x49d]
user:[ingridbinford] rid:[0x49f]
user:[yolandabinford] rid:[0x4a1]
user:[trevorbinford] rid:[0x4a3]
user:[samanthatrebek] rid:[0x4a5]
user:[dwanekilleen] rid:[0x4a7]
user:[alicefox] rid:[0x4a9]
user:[marydruidia] rid:[0x4ab]
user:[kimkilleen] rid:[0x4ad]
user:[lukegeorge] rid:[0x4af]
user:[xavierolson] rid:[0x4b1]
user:[maryvictoria] rid:[0x4b3]
user:[opheliazebra] rid:[0x4b5]
user:[quincytrebek] rid:[0x4b7]
user:[bobdruidia] rid:[0x4b9]
user:[opheliasmith] rid:[0x4bb]
user:[zeldacharles] rid:[0x4bd]
user:[gildairving] rid:[0x4bf]
user:[quincyyankee] rid:[0x4c1]
user:[noahfox] rid:[0x4c3]
user:[bobsmith] rid:[0x4c5]
user:[forrestyankee] rid:[0x4c7]
user:[gildajones] rid:[0x4c9]
user:[hankhankerson] rid:[0x4cb]
user:[hankjones] rid:[0x4cd]
user:[zeldaross] rid:[0x4cf]
user:[hankbinford] rid:[0x4d1]
user:[lukefox] rid:[0x4d3]
user:[trevorellis] rid:[0x4d5]
user:[xavierabbott] rid:[0x4d7]
user:[jorgesmith] rid:[0x4d9]
user:[opheliajones] rid:[0x4db]
user:[hankvictoria] rid:[0x4dd]
user:[ulyssesirving] rid:[0x4df]
user:[hankabbott] rid:[0x4e1]
user:[bobulrich] rid:[0x4e3]
user:[kimxavier] rid:[0x4e5]
user:[quincydruidia] rid:[0x4e7]
user:[alicehankerson] rid:[0x4e9]
user:[opheliaellis] rid:[0x4eb]
user:[quincylovering] rid:[0x4ed]
user:[paulxavier] rid:[0x4ef]
user:[victoriawashington] rid:[0x4f1]
user:[bobbinford] rid:[0x4f3]
user:[zeldairving] rid:[0x4f5]
user:[jorgepenrod] rid:[0x4f7]
user:[samanthairving] rid:[0x4f9]
user:[ulyssesgeorge] rid:[0x4fb]
user:[ednabinford] rid:[0x4fd]
user:[jorgehankerson] rid:[0x4ff]
user:[marywashington] rid:[0x501]
user:[raulsmith] rid:[0x503]
user:[quincygeorge] rid:[0x505]
user:[victoriavictoria] rid:[0x507]
user:[ingridzebra] rid:[0x509]
user:[quincyellis] rid:[0x50b]
user:[opheliayankee] rid:[0x50d]
user:[noahyankee] rid:[0x50f]
user:[bobirving] rid:[0x511]
user:[victoriaqueior] rid:[0x513]
user:[charleneellis] rid:[0x515]
user:[samanthaneptune] rid:[0x517]
user:[ednajones] rid:[0x519]
user:[jorgebinford] rid:[0x51b]
user:[wandafox] rid:[0x51d]
user:[alicejones] rid:[0x51f]
user:[luketrebek] rid:[0x521]
user:[samanthaolson] rid:[0x523]
user:[forrestneptune] rid:[0x525]
user:[ingridxavier] rid:[0x527]
user:[maryyankee] rid:[0x529]
user:[lukeirving] rid:[0x52b]
user:[bobmoss] rid:[0x52d]
user:[marykilleen] rid:[0x52f]
user:[kimneptune] rid:[0x531]
user:[yolandaneptune] rid:[0x533]
user:[yolandapenrod] rid:[0x535]
user:[marytrebek] rid:[0x537]
user:[alicewashington] rid:[0x539]
user:[marysmith] rid:[0x53b]
user:[trevorkilleen] rid:[0x53d]
user:[ingridneptune] rid:[0x53f]
user:[charlenexavier] rid:[0x541]
user:[samanthahankerson] rid:[0x543]
user:[paulross] rid:[0x545]
user:[victoriadruidia] rid:[0x547]
user:[ednaulrich] rid:[0x549]
user:[opheliamoss] rid:[0x54b]
user:[noahulrich] rid:[0x54d]
user:[raulgeorge] rid:[0x54f]
user:[maryqueior] rid:[0x551]
user:[quincyfox] rid:[0x553]
user:[dwaneyankee] rid:[0x555]
user:[zeldaabbott] rid:[0x557]
user:[alicedruidia] rid:[0x559]
user:[bobxavier] rid:[0x55b]
user:[zeldalovering] rid:[0x55d]
user:[hankzebra] rid:[0x55f]
user:[rauldruidia] rid:[0x561]
user:[quincywashington] rid:[0x563]
user:[ednalovering] rid:[0x565]
user:[wandabinford] rid:[0x567]
user:[zeldabinford] rid:[0x569]
user:[paulirving] rid:[0x56b]
user:[samanthadruidia] rid:[0x56d]
user:[rauljones] rid:[0x56f]
user:[dwanewashington] rid:[0x571]
user:[gildalovering] rid:[0x573]
user:[dwaneneptune] rid:[0x575]
user:[wandaqueior] rid:[0x577]
user:[ingridqueior] rid:[0x579]
user:[wandaellis] rid:[0x57b]
user:[hankirving] rid:[0x57d]
user:[kimabbott] rid:[0x57f]
user:[wandageorge] rid:[0x581]
user:[victoriazebra] rid:[0x583]
user:[wandawashington] rid:[0x585]
user:[ulyssesfox] rid:[0x587]
user:[charlenecharles] rid:[0x589]
user:[victoriaolson] rid:[0x58b]
user:[jorgejones] rid:[0x58d]
user:[bobtrebek] rid:[0x58f]
user:[noahdruidia] rid:[0x591]
user:[lukeulrich] rid:[0x593]
user:[paulsmith] rid:[0x595]
user:[dwaneross] rid:[0x597]
user:[paulwashington] rid:[0x599]
user:[ednadruidia] rid:[0x59b]
user:[trevorpenrod] rid:[0x59d]
user:[quincyabbott] rid:[0x59f]
user:[paulolson] rid:[0x5a1]
user:[alicebinford] rid:[0x5a3]
user:[kimhankerson] rid:[0x5a5]
user:[dwanehankerson] rid:[0x5a7]
user:[charlenejones] rid:[0x5a9]
user:[yolandakilleen] rid:[0x5ab]
user:[victorianeptune] rid:[0x5ad]
user:[noahvictoria] rid:[0x5af]
user:[opheliahankerson] rid:[0x5b1]
user:[gildakilleen] rid:[0x5b3]
user:[aliceolson] rid:[0x5b5]
user:[trevorolson] rid:[0x5b7]
user:[gildacharles] rid:[0x5b9]
user:[jorgefox] rid:[0x5bb]
user:[kimwashington] rid:[0x5bd]
user:[lukekilleen] rid:[0x5bf]
user:[victoriaabbott] rid:[0x5c1]
user:[ingridgeorge] rid:[0x5c3]
user:[raulyankee] rid:[0x5c5]
user:[dwanemoss] rid:[0x5c7]
user:[zeldakilleen] rid:[0x5c9]
user:[ingridvictoria] rid:[0x5cb]
user:[gildaabbott] rid:[0x5cd]
user:[ulyssesbinford] rid:[0x5cf]
user:[noaholson] rid:[0x5d1]
user:[quincyxavier] rid:[0x5d3]
user:[jorgeolson] rid:[0x5d5]
user:[ulyssesxavier] rid:[0x5d7]
user:[alicequeior] rid:[0x5d9]
user:[ednaabbott] rid:[0x5db]
user:[lukedruidia] rid:[0x5dd]
user:[opheliatrebek] rid:[0x5df]
user:[ingridfox] rid:[0x5e1]
user:[ulyssesolson] rid:[0x5e3]
user:[raultrebek] rid:[0x5e5]
user:[test] rid:[0x60f]
user:[qcljgnpsjl] rid:[0x610]
user:[uwdgunvfln] rid:[0x611]
user:[wjwnojisdx] rid:[0x612]
user:[xdtqjfinpd] rid:[0x613]
user:[aaigvfsuza] rid:[0x614]
user:[cojbecjcwu] rid:[0x615]
user:[jjwxlrkpts] rid:[0x616]
user:[ijshkhssxd] rid:[0x617]
user:[dbevvcejny] rid:[0x618]
user:[xkitgarrir] rid:[0x619]
user:[suglxphqmq] rid:[0x61a]
user:[wsijnjsbkz] rid:[0x61b]
user:[bujantwezh] rid:[0x61c]
user:[xhlfexdkfo] rid:[0x61d]
user:[kncvdvwihq] rid:[0x61e]
user:[qgeuudabpy] rid:[0x61f]
user:[buorotkglg] rid:[0x620]
user:[sdpwxvvakw] rid:[0x621]
user:[wpwoiezhhm] rid:[0x622]
user:[lrosflhrkf] rid:[0x623]
user:[tcudxxoytq] rid:[0x624]
user:[jtmeahxamd] rid:[0x625]
user:[uxezqodsih] rid:[0x626]
user:[csdpjbfhgl] rid:[0x627]
user:[vbqqzyawqq] rid:[0x628]
user:[mqxkrbemnx] rid:[0x629]
user:[tshpyrenlr] rid:[0x62a]
user:[ntrufouxzw] rid:[0x62b]
user:[alnnqyxpob] rid:[0x62c]
user:[pdgmebnfeh] rid:[0x62d]
user:[ofkzvdmdyu] rid:[0x62e]
user:[ynxibxsslc] rid:[0x62f]
user:[svewymuvrd] rid:[0x630]
user:[csqjbuatwr] rid:[0x631]
user:[buzkxchmue] rid:[0x632]
user:[bqzwpvxdpq] rid:[0x633]
user:[uqgyrulses] rid:[0x634]
user:[wogompbfel] rid:[0x635]
user:[nfjhsxqtcz] rid:[0x636]
user:[elbngrsuxb] rid:[0x637]
user:[bmqxdbpepn] rid:[0x638]
user:[zydtxopeuo] rid:[0x639]
user:[nwwepejhol] rid:[0x63a]
user:[ckykfyovrz] rid:[0x63b]
user:[mrakkbnppb] rid:[0x63c]
user:[rfjgncpzqv] rid:[0x63d]
user:[pyzckgcttj] rid:[0x63e]
user:[yxkhnuynqd] rid:[0x63f]
user:[iahtfchxoo] rid:[0x640]
user:[exkktdigim] rid:[0x641]
user:[nxakzmqeet] rid:[0x642]
user:[vmglekhpxv] rid:[0x643]
user:[pxbsvccdcy] rid:[0x644]
user:[lhpllubdfo] rid:[0x645]
user:[ppzvtplkij] rid:[0x646]
user:[yuvegmnrqn] rid:[0x647]
```

Used the following to take that list and turn it into just the users:
`awk -F[ '{print $2}'' ./userlist.txt | awk -F] '{print $1}' > tmp && mv tmp userlist.txt`

Creating the new  `userlist.txt`:

```text
Administrator
Guest
krbtgt
admin
elfu_admin
elfu_svc
remote_elf
ulyssesross
bobolson
raulpenrod
charleneneptune
xavierzebra
victoriacharles
paulyankee
ulyssestrebek
lukeyankee
paulhankerson
quincyjones
maryhankerson
ulyssespenrod
charlenesmith
ulysseslovering
hankqueior
ednamoss
hankgeorge
yolandayankee
wandaneptune
forrestvictoria
jorgetrebek
zeldaellis
samanthazebra
noahgeorge
quincycharles
paulvictoria
xavierirving
wandayankee
yolandaabbott
victoriageorge
forrestcharles
opheliaolson
xavierdruidia
gildapenrod
opheliakilleen
bobross
ingridbinford
yolandabinford
trevorbinford
samanthatrebek
dwanekilleen
alicefox
marydruidia
kimkilleen
lukegeorge
xavierolson
maryvictoria
opheliazebra
quincytrebek
bobdruidia
opheliasmith
zeldacharles
gildairving
quincyyankee
noahfox
bobsmith
forrestyankee
gildajones
hankhankerson
hankjones
zeldaross
hankbinford
lukefox
trevorellis
xavierabbott
jorgesmith
opheliajones
hankvictoria
ulyssesirving
hankabbott
bobulrich
kimxavier
quincydruidia
alicehankerson
opheliaellis
quincylovering
paulxavier
victoriawashington
bobbinford
zeldairving
jorgepenrod
samanthairving
ulyssesgeorge
ednabinford
jorgehankerson
marywashington
raulsmith
quincygeorge
victoriavictoria
ingridzebra
quincyellis
opheliayankee
noahyankee
bobirving
victoriaqueior
charleneellis
samanthaneptune
ednajones
jorgebinford
wandafox
alicejones
luketrebek
samanthaolson
forrestneptune
ingridxavier
maryyankee
lukeirving
bobmoss
marykilleen
kimneptune
yolandaneptune
yolandapenrod
marytrebek
alicewashington
marysmith
trevorkilleen
ingridneptune
charlenexavier
samanthahankerson
paulross
victoriadruidia
ednaulrich
opheliamoss
noahulrich
raulgeorge
maryqueior
quincyfox
dwaneyankee
zeldaabbott
alicedruidia
bobxavier
zeldalovering
hankzebra
rauldruidia
quincywashington
ednalovering
wandabinford
zeldabinford
paulirving
samanthadruidia
rauljones
dwanewashington
gildalovering
dwaneneptune
wandaqueior
ingridqueior
wandaellis
hankirving
kimabbott
wandageorge
victoriazebra
wandawashington
ulyssesfox
charlenecharles
victoriaolson
jorgejones
bobtrebek
noahdruidia
lukeulrich
paulsmith
dwaneross
paulwashington
ednadruidia
trevorpenrod
quincyabbott
paulolson
alicebinford
kimhankerson
dwanehankerson
charlenejones
yolandakilleen
victorianeptune
noahvictoria
opheliahankerson
gildakilleen
aliceolson
trevorolson
gildacharles
jorgefox
kimwashington
lukekilleen
victoriaabbott
ingridgeorge
raulyankee
dwanemoss
zeldakilleen
ingridvictoria
gildaabbott
ulyssesbinford
noaholson
quincyxavier
jorgeolson
ulyssesxavier
alicequeior
ednaabbott
lukedruidia
opheliatrebek
ingridfox
ulyssesolson
raultrebek
test
qcljgnpsjl
uwdgunvfln
wjwnojisdx
xdtqjfinpd
aaigvfsuza
cojbecjcwu
jjwxlrkpts
ijshkhssxd
dbevvcejny
xkitgarrir
suglxphqmq
wsijnjsbkz
bujantwezh
xhlfexdkfo
kncvdvwihq
qgeuudabpy
buorotkglg
sdpwxvvakw
wpwoiezhhm
lrosflhrkf
tcudxxoytq
jtmeahxamd
uxezqodsih
csdpjbfhgl
vbqqzyawqq
mqxkrbemnx
tshpyrenlr
ntrufouxzw
alnnqyxpob
pdgmebnfeh
ofkzvdmdyu
ynxibxsslc
svewymuvrd
csqjbuatwr
buzkxchmue
bqzwpvxdpq
uqgyrulses
wogompbfel
nfjhsxqtcz
elbngrsuxb
bmqxdbpepn
zydtxopeuo
nwwepejhol
ckykfyovrz
mrakkbnppb
rfjgncpzqv
pyzckgcttj
yxkhnuynqd
iahtfchxoo
exkktdigim
nxakzmqeet
vmglekhpxv
pxbsvccdcy
lhpllubdfo
ppzvtplkij
yuvegmnrqn
```

Based on this, I can query a user...

My script to dump all the info I could from RPC

```bash
#!/bin/bash

while read -r user; do
    echo -e 'Anuakviba@\n' | rpcclient --user=nfjhsxqtcz -c "queryuser $user" 10.128.3.30
done < ./userlist.txt
```

I base64'd it so I could more easily copy it to my machine:

`bash ./get_all_users.sh | base64 -w0`

It gave a pretty good dump of all users full names and such, but really...no new information. Was looking for any data an admin could have left behind thinking it was safe to enter and no one but another admin could read, but sadly no dice.

Oh well. In doing all that, I realized that `samrdump.py` existed on the machine. So that was completely unnecessary as I could get the same info from that. But then again, what is information security if not going the long way to obtain something that could be found by simply knocking on the door and asking for what you need?