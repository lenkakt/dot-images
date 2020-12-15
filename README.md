Analýza závislostí pro linuxovou distribuci
===========================================

Složka obsahuje grafy závislostí balíků distribuce "ima" sestavené pro desku BBCU 3.0.

Distribuce je skládána pomocí systému Yocto; vychází z úprav pro procesory od společnosti NXP (fsl-community-bsp).

Pro desku byla přidána vrstva meta-ima, jež obsahuje recepty k sestavení obrazu "ima-minimal": to je distribuce Linuxu pro desku.
Pro překlad se užívá jádro upravené na TUL pro desku IMA, U-Boot upravený pro desku - oboje se stahuje ze samostatných projektů na GitHub.

Dále je k desce přidán SW balík bbcu-ws, jenž obsahuje prototyp webové služby jako vzorovou aplikaci pro desku.

Celá distribuce byla přeložena v dockeru upraveném pro překlad Yocto. 

Seznam balíků byl získán příkazem 

bitbake -g ima-minimal

Je uložen v souboru dot-input.

Pro jednotlivé balíky ze seznamu byl příkazem 

bitbake -g "název balíku" 

postupně generován soubor .dot obsahující graf závislostí pro konkrétní balík. Soubory s grafy byly pojmenovány "jméno balíku"-depends.dot a uloženy do samostatného adresáře. Ten je nyní součástí tohoto repozitáře git k další analýze. V adresáři je také skript užitý pro generování těchto souborů.

Co je potřeba analyzovat
========================

1.) Pro budoucí aktualizaci distribuce je nutné vědět, jak se balíky ovlivňují: tedy které z balíků je nutné překládat se změnou verze některého z balíků. Otázka zní: když vyšla nová verze balíku glibc, které další balíky musím přeložit, abych byla distribuce aktuální?

2.) Při úpravách a minimalizaci je nutné vědět: co se stane, kdž odstraním balík libcap? Závisí na něm další balíky z ima-minimal? A jaké to jsou? 

3.) Dále je dobré vědět, které balíky jsou silné uzly: opakují se v mnoha grafech a jsou uzly s mnoha hranami.



