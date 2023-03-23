# Fausia lau lava SMTP meli e lafo ai le server

## faatomuaga

E mafai e le SMTP ona fa'atau sa'o mai auaunaga mai fa'atau oloa, e pei o:

* [Amazon SES SMTP](https://docs.aws.amazon.com/ses/latest/dg/send-email-smtp.html)
* [Ali cloud email tulei](https://www.alibabacloud.com/help/directmail/latest/three-mail-sending-methods)

E mafai fo'i ona e fausia lau lava meli - e le fa'atapula'aina le lafo, maualalo le tau atoa.

I lalo, matou te faʻaalia i lea laasaga ma lea laasaga pe faʻapefea ona fausia a matou lava meli meli.

## Filifiliga server

E manaʻomia e le server SMTP faʻafeiloaʻi se IP lautele ma ports 25, 456, ma le 587 tatala.

O ao lautele e masani ona faʻaaogaina ua poloka nei uafu ona o le faaletonu, ma atonu e mafai ona tatalaina i latou e ala i le tuʻuina atu o se poloaiga faigaluega, ae e matua faigata lava.

Ou te fautuaina le faʻatau mai se talimalo o loʻo tatala nei ports ma lagolagoina le faʻatulagaina o igoa faʻailoga.

O iinei, ou te fautuaina [Contabo](https://contabo.com) .

Contabo o se kamupani talimalo e faʻavae i Munich, Siamani, faʻavae i le 2003 ma tau faʻatauvaʻa.

Afai e te filifilia le Euro e avea ma tupe faʻatau, o le tau o le a sili atu ona taugofie (o se 'auʻaunaga ma le 8GB manatua ma le 4 PPU tau e tusa ma le 529 yuan i le tausaga, ma o le tau faʻapipiʻi muamua e leai se totogi mo le tausaga e tasi).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/UoAQkwY.webp)

Pe a tuʻuina se faʻatonuga, faʻamatalaga `prefer AMD` , ma o le server ma le AMD CPU o le a sili atu le faʻatinoga.

I le mea o loʻo mulimuli mai, o le a ou avea Contabo's VPS e fai ma faʻataʻitaʻiga e faʻaalia ai pe faʻapefea ona fausia lau lava meli meli.

## Ubuntu faiga fa'atulagaina

O le faiga faʻaoga iinei o le Ubuntu 22.04

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/smpIu1F.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/m7Mwjwr.webp)

Afai e faʻaalia e le 'auʻaunaga ile ssh `Welcome to TinyCore 13!` (e pei ona faʻaalia i le ata o loʻo i lalo), o lona uiga e leʻi faʻapipiʻiina le faiga. Fa'amolemole motusia le ssh ma fa'atali mo ni nai minute e toe saini ai.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/-qKACz9.webp)

A `Welcome to Ubuntu 22.04.1 LTS` , ua maeʻa le amataga, ma e mafai ona e faʻaauau i laasaga nei.

### [Filifili] Fa'amata le si'osi'omaga atina'e

O lenei laasaga e filifili.

Mo le faʻaogagofie, ou te tuʻuina le faʻapipiʻiina ma le faʻatulagaina o le ubuntu software i le [github.com/wactax/ops.os/tree/main/ubuntu](https://github.com/wactax/ops.os/tree/main/ubuntu) .

Fa'atonu le fa'atonuga e fa'apipi'i i le kiliki e tasi.

```
bash <(curl -s https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

Tagata fa'aoga Saina, fa'amolemole fa'aoga le fa'atonuga lea, ma o le gagana, sone taimi, ma isi o le a otometi lava ona seti.

```
CN=1 bash <(curl -s https://ghproxy.com/https://raw.githubusercontent.com/wactax/ops.os/main/ubuntu/boot.sh)
```

### Contabo e mafai ai le IPV6

Fa'aagaoi le IPV6 ina ia mafai fo'i e le SMTP ona lafo imeli ma tuatusi IPV6.

fa'asa'o `/etc/sysctl.conf`

Suia pe faaopoopo laina nei

```
net.ipv6.conf.all.disable_ipv6 = 0
net.ipv6.conf.default.disable_ipv6 = 0
net.ipv6.conf.lo.disable_ipv6 = 0
```

Toe tulitatao i [le contabo tutorial: Fa'aopoopoina le IPv6 feso'ota'iga i lau 'au'aunaga](https://contabo.com/blog/adding-ipv6-connectivity-to-your-server/)

Faʻasaʻo `/etc/netplan/01-netcfg.yaml` , faʻaopoopo ni nai laina e pei ona faʻaalia i le ata o loʻo i lalo (Contabo VPS default configuration file ua uma ona i ai nei laina, naʻo le le faʻamaonia).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/5MEi41I.webp)

Ona `netplan apply` e fa'amanaia ai le fa'atulagaina o suiga.

A maeʻa le faʻatulagaina, e mafai ona e faʻaogaina `curl 6.ipw.cn` e matamata ai i le tuatusi IPv6 o lau fesoʻotaʻiga i fafo.

## Fa'akomi le fa'aputuga o mea e teu ai

```
git clone https://github.com/wactax/ops.soft.git
```

## Fausia se tusi faamaonia SSL fua mo lou igoa fa'apitonu'u

O le lafoina o meli e mana'omia ai se tusi faamaonia SSL mo fa'ailoga ma saini.

Matou te fa'aogaina [le acme.sh](https://github.com/acmesh-official/acme.sh) e fa'atupu tusi pasi.

acme.sh o se punaoa faʻapipiʻi faʻapipiʻi tusi saini meafaigaluega,

Ulufale i le faleteuoloa ops.soft, tamoʻe `./ssl.sh` , ma o le a faia se faila `conf` i **le lisi pito i luga** .

Su'e lau DNS provider mai [acme.sh dnsapi](https://github.com/acmesh-official/acme.sh/wiki/dnsapi) , edit `conf/conf.sh` .

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Qjq1C1i.webp)

Ona tamo'e lea `./ssl.sh 123.com` e fa'atupu `123.com` ma `*.123.com` tusipasi mo lou igoa ole igoa.

O le taʻavale muamua e otometi lava ona faʻapipiʻi [acme.sh](https://github.com/acmesh-official/acme.sh) ma faʻaopoopo se galuega faʻatulagaina mo le faʻafouina otometi. E mafai ona e vaʻai `crontab -l` , o loʻo i ai se laina faʻapea.

```
52 0 * * * "/mnt/www/.acme.sh"/acme.sh --cron --home "/mnt/www/.acme.sh" > /dev/null
```

O le ala mo le tusi faamaonia na faia e pei o `/mnt/www/.acme.sh/123.com_ecc。`

O le faafouga o le tusi faamaonia o le a valaau `conf/reload/123.com.sh` script, fa'asa'o lenei tusitusiga, e mafai ona e fa'aopoopoina fa'atonuga e pei o le `nginx -s reload` e fa'afou ai le fa'ailoga tusi fa'amaonia o talosaga fa'atatau.

## Fausia le server SMTP ma chasquid

[chasquid](https://github.com/albertito/chasquid) ose fa'aumau SMTP puna'oa e tusia i le gagana Go.

I le avea ai ma sui mo polokalame tuai meli meli e pei o Postfix ma Sendmail, chasquid e faigofie ma faigofie ona faʻaoga, ma e faigofie foi mo le atinaʻe lona lua.

Run `./chasquid/init.sh 123.com` o le a faʻapipiʻiina otometi i le kiliki e tasi (sui le 123.com i lou igoa faʻasalalau).

## Fa'atulaga le Saini imeli DKIM

O le DKIM e fa'aaogaina e lafo ai saini imeli e puipuia ai tusi mai le fa'aogaina o le spam.

A maeʻa le faʻatonuga manuia, o le a faʻamalosia oe e seti le DKIM faamaumauga (e pei ona faʻaalia i lalo).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/LJWGsmI.webp)

Na'o le fa'aopoopoina o se fa'amaumauga TXT i lau DNS (e pei ona fa'aalia i lalo).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/0szKWqV.webp)

## Va'ai tulaga tautua & ogalaau

 `systemctl status chasquid` Va'ai tulaga tautua.

O le tulaga o galuega masani e pei ona faʻaalia i le ata o loʻo i lalo

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/CAwyY4E.webp)

 `grep chasquid /var/log/syslog` poʻo `journalctl -xeu chasquid` e mafai ona vaʻai i le faʻamatalaga sese.

## Toe fesuia'i le faatulagaga o igoa ole igoa

Ole igoa ole igoa ole fa'ataga ole tuatusi IP e fo'ia ile igoa ole igoa ole igoa.

O le fa'atuina o se igoa fa'aliliu'ese e mafai ona taofia ai imeli mai le fa'ailoaina o le spam.

A maua le meli, o le a faia e le server o lo'o talia le su'esu'eina o igoa ole igoa ile tuatusi IP ole 'au'aunaga o lo'o auina atu e fa'amaonia ai pe iai le igoa fa'aliliuga fa'aigoa o le server o lo'o auina atu.

Afai e le o iai se igoa ole igoa ole igoa ole igoa ole igoa ole tuatusi IP ile tuatusi IP ole server ole auina atu, e ono iloa e le server e taliaina le imeli o se spam pe teena.

Asiasi [https://my.contabo.com/rdns](https://my.contabo.com/rdns) ma fetuutuunai e pei ona faaalia i lalo

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/IIPdBk_.webp)

A maeʻa ona faʻatulagaina le igoa faʻasolo, manatua e faʻapipiʻi le faʻaiʻuga i luma ole igoa ole igoa ipv4 ma ipv6 ile server.

## Fa'asa'o le igoa talimalo o chasquid.conf

Suia `conf/chasquid/chasquid.conf` i le tau o le igoa ole igoa.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/6Fw4SQi.webp)

Ona tamoe lea o `systemctl restart chasquid` e toe amata le auaunaga.

## Backup conf i le git repository

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/Fier9uv.webp)

Mo se faʻataʻitaʻiga, ou te toe faʻaleleia le conf folder i laʻu lava github process e pei ona taua i lalo

Fausia muamua se faleteuoloa tumaoti

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ZSCT1t1.webp)

Ulufale i le conf directory ma lafo i le faleteuoloa

```
git init
git add .
git commit -m "init"
git branch -M main
git remote add origin git@github.com:wac-tax-key/conf.git
git push -u origin main
```

## Faaopoopo le tagata e auina atu

tamo'e

```
chasquid-util user-add i@wac.tax
```

E mafai ona fa'aopoopo le sender

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/khHjLof.webp)

### Fa'amaonia ua sa'o le setiina o le upu fa'aoga

```
chasquid-util authenticate i@wac.tax --password=xxxxxxx
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/e92JHXq.webp)

A maeʻa ona faʻaopoopo le tagata faʻaoga, `chasquid/domains/wac.tax/users` o le a faʻafouina, manatua e tuʻuina atu i le fale teu oloa.

## DNS fa'aopoopo fa'amaumauga SPF

SPF ( Sender Policy Framework ) ose imeli faʻamaonia tekinolosi faʻaaogaina e puipuia ai imeli taufaasese.

E fa'amaonia ai le fa'ailoaina o se tagata e lafo meli e ala i le siakiina o le tuatusi IP a le tagata e auina atu e fetaui ma fa'amaumauga DNS o le igoa ole igoa lea e fai mai ai, e taofia ai tagata taufaasese mai le lafoina o imeli pepelo.

O le fa'aopoopoina o fa'amaumauga a le SPF e mafai ona taofia ai imeli mai le fa'ailoaina o le spam i le tele e mafai ai.

Afai e le lagolagoina e lau 'upega tafa'ilagi le ituaiga SPF, na'o le fa'aopoopoina o fa'amaumauga o ituaiga TXT.

Mo se faʻataʻitaʻiga, o le SPF o `wac.tax` e faʻapea

`v=spf1 a mx include:_spf.wac.tax include:_spf.google.com ~all`

SPF mo `_spf.wac.tax`

`v=spf1 a:smtp.wac.tax ~all`

Manatua o loʻo ou `include:_spf.google.com` iinei, e mafua ona o le a ou faʻapipiʻi `i@wac.tax` e avea ma tuatusi lafo i le Google mailbox mulimuli ane.

## DNS configuration DMARC

DMARC o le fa'apu'upu'u o le (Domain-based Message Authentication, Reporting & Conformance).

E fa'aaogaina e pu'e ai fa'afiti SPF (atonu e mafua mai i fa'aletonu o le fa'atulagaina, po'o le fa'afoliga o se isi o oe e lafo le spam).

Fa'aopoopo fa'amaumauga TXT `_dmarc` ,

O le anotusi e faapea

```
v=DMARC1; p=quarantine; fo=1; ruf=mailto:ruf@wac.tax; rua=mailto:rua@wac.tax
```

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/k44P7O3.webp)

O le uiga o ta'iala ta'itasi e fa'apea

### p (Faiga Fa'avae)

Fa'ailoa mai pe fa'afefea ona taulimaina imeli e le mafai ona fa'amaonia SPF (Sender Policy Framework) po'o le DKIM (DomainKeys Identified Mail). O le p parameter e mafai ona seti i se tasi o tau e tolu:

* leai: E leai se gaioiga e faia, na o le faʻamaoniga e toe faʻafoʻi atu i le tagata e auina atu e ala i le faiga o lipoti imeli.
* Quarantine: Tu'u le meli e le'i pasia le fa'amaoniga i totonu o le pusa spam, ae le teena sa'o le meli.
* teena: Te'ena sa'o imeli e le mafai ona fa'amaonia.

### fo (Filifiliga Fa'aletonu)

Fa'amaoti mai le aofa'i o fa'amatalaga na toe fa'afo'i mai e le faiga fa'amatalaga. E mafai ona seti i se tasi o mea taua nei:

* 0: Lipoti i'uga fa'amaonia mo fe'au uma
* 1: Na'o lipoti o fe'au e le mafai ona fa'amaonia
* d: Na'o lipoti le fa'amaonia o igoa ole igoa ole igoa ole laiga
* s: na'o lipoti SPF fa'amaonia le manuia
* l: Na'o lipoti DKIM fa'amaonia faaletonu

### rua & ruf

* rua (Lipoti URI mo Lipoti Tuufaatasi): Tulaga imeli mo le mauaina o lipoti tuufaatasi
* ruf (Lipoti URI mo lipoti Fa'afomai): tuatusi imeli e maua ai lipoti auiliili

## Fa'aopoopo fa'amaumauga MX e lafo atu ai imeli ile Google Mail

Talu ai e le mafai ona ou mauaina se pusameli faʻapitoa e lagolagoina ai tuatusi lautele (Catch-All, e mafai ona maua soʻo se imeli e lafo i lenei igoa faʻapitonuʻu, e aunoa ma se faʻatapulaʻaina i prefixes), na ou faʻaogaina le chasquid e lafo uma imeli i laʻu pusa meli Gmail.

**Afai ei ai sau lava pusa meli pisinisi totogi, faamolemole aua le suia le MX ma faamisi le laasaga lea.**

Fa'asa'o `conf/chasquid/domains/wac.tax/aliases` , seti le pusa meli lafo

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/OBDl2gw.webp)

`*` fa'ailoa mai imeli uma, `i` o le tuatusi imeli muamua a le tagata na auina atu na faia i luga. Ina ia lafo atu le meli, e mana'omia e tagata ta'ito'atasi ona fa'aopoopo se laina.

Ona faaopoopo lea o le faamaumauga MX (Ou te faasino sao i le tuatusi o le reverse domain name iinei, e pei ona faaalia i le laina muamua i le ata i lalo).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/7__KrU8.webp)

A maeʻa le faʻatulagaina, e mafai ona e faʻaogaina isi tuatusi imeli e lafo ai imeli ile `i@wac.tax` ma `any123@wac.tax` e vaʻai pe mafai ona e mauaina imeli ile Gmail.

Afai e leai, siaki le chasquid log ( `grep chasquid /var/log/syslog` ).

## Auina se imeli ile i@wac.tax ile Google Mail

Ina ua uma ona maua e Google Meli le meli, sa masani lava ona ou faamoemoe e tali i le `i@wac.tax` nai lo le i.wac.tax@gmail.com.

Asiasi [https://mail.google.com/mail/u/1/#settings/accounts](https://mail.google.com/mail/u/1/#settings/accounts) ma kiliki "Faaopoopo se isi tuatusi imeli".

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/PAvyE3C.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/_OgLsPT.webp)

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/XIUf6Dc.webp)

Ona, ulufale lea i le code verification na maua e le imeli na lafo i ai.

Ma le mea mulimuli, e mafai ona setiina o le tuatusi o le auina atu (fa'atasi ai ma le filifiliga e tali atu i le tuatusi lava e tasi).

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/a95dO60.webp)

I lenei auala, ua matou faʻamaeʻaina le faʻavaeina o le SMTP mail server ma i le taimi lava e tasi e faʻaaoga le Google Mail e lafo ma maua ai imeli.

## Auina atu se imeli suʻega e siaki pe o manuia le faʻatulagaga

Ulufale `ops/chasquid`

Tafe `direnv allow` e faʻapipiʻi faʻalagolago (ua faʻapipiʻi le direnv i le faʻagasologa muamua o le tasi-ki muamua ma ua faʻaopoopoina se matau i le atigi)

ona tamoe lea

```
user=i@wac.tax pass=xxxx to=iuser.link@gmail.com ./sendmail.coffee
```

O le uiga o fa'amaufa'ailoga e fa'apea

* tagata fa'aoga: igoa ole igoa SMTP
* pasi: SMTP upu faataga
* i: e mauaina

E mafai ona e lafo se imeli su'ega.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/ae1iWyM.webp)

E fautuaina e faʻaoga Gmail e maua ai imeli suʻega e siaki ai pe manuia faʻasalalauga.

### TLS fa'ailoga masani

E pei ona faʻaalia i le ata o loʻo i lalo, o loʻo i ai lenei tamai loka, o lona uiga o le SSL tusi faamaonia ua mafai ona manuia.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/SrdbAwh.webp)

Ona kiliki lea o le "Show Original Email"

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/qQQsdxg.webp)

### DKIM

E pei ona faʻaalia i le ata o loʻo i lalo, o le Gmail original mail page o loʻo faʻaalia DKIM, o lona uiga o le DKIM configuration ua manuia.

![](https://pub-b8db533c86124200a9d799bf3ba88099.r2.dev/2023/03/an6aXK6.webp)

Siaki le Received in the header of the original email, ma e mafai ona e vaʻaia o le tuatusi o le auina atu o le IPV6, o lona uiga o le IPV6 o loʻo faʻatulaga lelei foi.
