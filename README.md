# Intro - Business Garden RUG

Sveiki visi! Aš esu Paulius, Ignitis Duomenų analitikos skyriaus vadovas, ir sveiki atvykę į pirmąjį Business Garden R User Group susitikimą! Šiandien mūsų susitikimo tikslas yra susipažinti su naujovėmis R pasaulyje ir skirti laiko pabendrauti visais R klausimais. Pristatysime du įrankius: pirma, pradėsime nuo pranešimo apie DuckDB, o po to perduosiu estafetę savo kolegai Modestui, kuris papasakos apie targets biblioteką ir jos panaudojimą. Likusį laiką kviesime jus klausimams ir bendravimui kartu.

Prieš pradedant, norėčiau skirti kelias minutes atsakyti į klausimą - o kam tokio susitikimo apskritai reikia? Pirma, aš labai tikiu, jog R ekosistema yra nepamainoma dirbant su duomenimis. Aš pats pradėjau programuoti 2015-ais, kai tidyverse buvo pradėjęs kilti ant bangos. Tuo metu dirbau su SPSS ir buvau tik vangiai girdėjęs apie R. O darbas su SPSS buvo labai nepatogus - turėdavau kopijuoti grafikus ir lenteles į savo dokumentą, išrašyti visas p reikšmes, kartoti tuos pačius 20 mygtuko paspaudimų atlikti testams. O jeigu papildydavai savo duomenų rinkinį, turėdavau kartoti visa tai nuo pradžių.

Pagalvojau, gali būti geriau - negali būti, jog visi trinasi SPSS'u? Pabandžiau R ir daugiau niekada neatsisukau atgal. Pirmą kartą kai sugeneravau Word'o dokumentą iš RMarkdown failo man buvo VAU. Kas nežino, RMarkdown yra failo tipas, kuris leidžia rašyti ir kodą, ir tekstą viename faile. Aš buvau šoke - aš galiu dirbti viename faile, rašyti tekstą ir rašyti kodą, ir visą savo darbą paversti dokumentu. Kurį galiu išsiųsti kitam žmogui! R ir jos ekosistema man iki dabar yra nepamainomas įrankis dirbti su kolegomis ir jų duomenimis.

Antra priežastis, kodėl R yra nuostabi kalba - tai yra jos žmonės. R iki šiol turi aktyvią bendruomenę, kuri kuria naujus įrankius ir dalinasi patirtimi. Aš pats joje dalyvauju mažiau negu norėčiau, bet galiu užtikrinti - tai buvo labai efektyvus būdas sužinoti apie naujus įrankius ir įgyti daug žinių. Šiuo susitikimu noriu grąžinti duoklę tai bendruomenei ir įtraukti daugiau žmonių čia, Vilniuje. R bendruomenė daugiausia gyvena twitteryje ir labai daug žmonių galite surasti per #rstats hashtag'ą. Jeigu norite starterio, ką sekti, galėčiau rekomenduoti šiuos dešimt žmonių:

# Introduction

Taigi, užtenka vieno intro, pabandykime šokti prie kito intro - kas tas DuckDB? DuckDB atsirado užpildyti nišą tarp duomenų bazių. Bendrai, duomenų bazių sistemas galima skirstyti pagal dvi kategorijas: OLTP ir OLAP, ir hostinta vs serverless. Dauguma duomenų bazių yra OLTP: jos yra puikios atlikti operacijas vienam įrašui per aibę skirtingų lentelių, bet jos ne visada gerai susitvarkys su analitinėmis užklausomis, kurios įtraukia visos lentelės duomenis. OLAP yra priešingai: labai gerai sutvarko didelius duomenų kiekius, bet ne pavienius įrašus. Embedded duomenų bazių iki šiol nebuvo daug - geriausias pavyzdys yra SQLite, kuris yra gana mažas kaip programinė įranga skirtas vietiniams procesams. Absoliuti dauguma duomenų bazių šiandien yra programinė įranga, kurią reikia diegti serveryje, ją atnaujinti ir palaikyti. Arba mokėti pinigus už tai.

DuckDB yra atsakymas į nišą, kuomet reikia duomenų bazės analitinėms užklausoms, bet nenorime/negalime host'inti dedikuotos programinės įrangos atskirame serveryje.

## Kas iš to?

Pasirodo, su C++ parašyta programinė įranga, kuri gyvena pas mus vietiniame kompiuterjye, gali būti labai greita. O dar geriau, DuckDB yra labai paprasta įsidiegti.

Kas esate girdėję apie DuckDB? Nuostabu, tuomet pirma turime pradėti nuo duomenų, su kuriais mes kaip profesionalai dirbame. Kai aš dirbu su keliais šimtais ar tūkstančiais įrašų, tikėtina, jog pasinaudosiu Exceliu ir PowerQuery. Jeigu susidursiu su keliais šimtais tūkstančių, griebiu R. Keli milijonai? Be problemų, data.table susitvarko. O ką daryti su keliomis dešimtimis milijonų?