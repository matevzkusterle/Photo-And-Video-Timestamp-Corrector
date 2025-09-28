📌 Logika obdelave datotek
1. Procesiranje map

Skripta prehodi vse podmape v Arhiv slik.

2. Določitev datuma mape

Če obstaja date.txt → uporabi ta datum (oblika: Weekday, Day Month Year).

Če date.txt ne obstaja → iz imena mape izlušči letnico (2000–2030).

Če letnice ni → nadaljuje brez omejitve leta.

3. Procesiranje datotek
📷 Fotografije (JPG/JPEG/PNG)

Prebere Date Taken iz EXIF (JPG) ali metapodatkov (PNG).

Če obstaja Date Taken in letnica ustreza mapi → poravna filesystem datume na ta datum.

Če Date Taken obstaja, a letnica ne ustreza →

Najprej poišče drugo fotografijo v mapi s pravilnim letom → uporabi ta datum.

Če ne najde → nastavi vse datume (EXIF + filesystem) na 15. junij [leto mape].

Če Date Taken manjka →

Najprej uporabi datum druge fotografije v mapi s pravilnim letom.

Če ne najde → uporabi 15. junij [leto mape].

Če mapa nima letnice →

Če obstaja Date Taken → poravna filesystem datume na ta datum.

Če ne obstaja → uporabi najbližji datum katere koli druge fotografije v isti mapi.

🎥 Videi (MP4)

Prebere Media Created z ExifTool.

Če obstaja Media Created in letnica ustreza mapi → poravna vse datume (interni + filesystem).

Če obstaja, a letnica ne ustreza →

Najprej poišče drug video v mapi s pravilnim letom → uporabi ta datum.

Če ne najde → nastavi vse datume na 15. junij [leto mape].

Če Media Created manjka →

Najprej uporabi datum drugega videa v mapi s pravilnim letom.

Če ne najde → uporabi 15. junij [leto mape].

Če mapa nima letnice →

Če obstaja Media Created → poravna vse datume na ta datum.

Če ne obstaja → uporabi najbližji datum katerega koli drugega videa v isti mapi.

4. Posebni primeri

Pokvarjene datoteke → zabeleži napako, datoteko pusti nedotaknjeno.

Ne-medijske datoteke (TXT, DOC, …) → vedno preskoči.