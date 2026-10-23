TOUR 20 — compte rendu du Codeur 1 (elijah-dd) : le duel, branche « duel »
main intouché (23ba770, avance rapide sur origin/main à 20h20, grande fusion du Chef). Branche duel = e562458 (rebasée sur 23ba770), un seul commit : le rétroviseur arrière et deux essais laissés éteints. Pas verte (herbe hors erreurs 4471 > 4000), donc elle reste une branche.

Ordre : PAS tenu (mesuré, 9 essais). Le duel passe sur le circuit test avec le bon réglage, mais ce réglage casse les courses à 10 (chocs 19 à 45).

1. Ce que montre la trace du duel (rapide 1,00 à 30 m derrière un lent 0,94, technique) :
   - L'écart en TEMPS reste ~1 s tout le tour : le rapide ne gagne rien, il suit à IA_DISTANCE_SUIVI = 14 m dans chaque virage (donc à la vitesse du lent) et les deux sont en pointe dans les droites. Il ne se rapproche qu'au freinage (l'autre freine avant lui), puis l'écart en mètres regonfle à la sortie (même écart en temps).
   - Du coup chaque préparation d'attaque meurt à sa naissance : « échappée » dès que g > 1 s × u (IA_ATTAQUE_ECART_TEMPS), et il est à 1,0–1,3 s. Seuil à 1,5 s ou 2 s : rien ne change sur le technique.
   - Décalé, il arrive « pas à hauteur » à 25–39 m derrière : il se décale parfois à 54 m (règle « fond sur elle »), et surtout, une fois à côté (ligne d'attaque à ecartSur = 3,5 m, réflexe à IA_REFLEXE_COTE = 4,5 m), le réflexe de côté le fait rouler 1 m/s MOINS vite que la voiture qu'il attaque. Il ne peut pas arriver à sa hauteur.
   - Journal du rapide sur 5 tours : 16 attaques, toutes « échappée », « pas à hauteur », « pas devant au freinage (virage lent) » ou « pas la place » (circuit test : le lent tient l'intérieur, pas de place à côté).

2. Les essais (30 courses, 10 IA, normal ; référence main : dép 33, chocs 3, herbe 2982, vainqueur ≠ poleman 0, top 3 30) :
   | essai | duel test | duel technique | dép | chocs | herbe hors err. | ≠ poleman | top 3 | 20 voit. |
   |---|---|---|---|---|---|---|---|---|
   | A. rétroviseur 40 m + attaquant ne cède pas la vitesse + rattrapé garde sa ligne | tour 1 (0 choc) | non | 107 | 45 | 18 040 | 5 | 30 | 3 / 4 |
   | A + échappée 1,5 s ou 2 s | tour 1 | non (0,98 : tour 4) | — | — | — | — | — | — |
   | B. rétroviseur seul | — | — | 62 | 7 | 13 004 | 1 | 30 | 0 / 5 |
   | C. rétroviseur + garde sa ligne | — | — | 73 | 19 | 9 416 | 2 | 30 | 2 / 1 |
   | D. rétroviseur + ne cède pas | — | — | 99 | 30 | 15 010 | 3 | 30 | 1 / 5 |
   | E. rétroviseur borné (entouré, réflexe : fenêtre de 8 m) seul | — | — | 29 | 2 | 4 471 | 0 | 30 | 0 / 1 |
   | E + garde sa ligne + attaquant à vitesse égale | tour 3 (chocs 10 m/s) | — | 50 | 19 | 6 738 | 4 | 30 | 2 / 2 |
   | E + garde sa ligne | — | — | 56 | 21 | 5 951 | 4 | 30 | 2 / 2 |
   | E + attaquant à vitesse égale | — | — | 30 | 5 | 4 443 | 0 | 30 | 0 / 2 |
   | rétroviseur à 0 m (témoin) | — | — | 34 | 2 | 3 481 | 0 | 30 | 0 / 1 |
   | F. (dernier essai, 20h26) E + gel du seul côté de l'attaquant (< 15 m, dans la droite, jusqu'au freinage) + attaquant à hauteur (≥ 1/3 de longueur) ne cède plus | non (0 choc) | non (0 choc) | 31 | 6 | 4 157 | 0 | 30 | 0 / 1 |
   | G. (20h29) F mais l'attaquant décalé ne se règle plus sur la vitesse de l'attaquée, sauf si l'espace libre de son côté (attaquée → bord) < LARGEUR_VOITURE + IA_ESPACE_LAISSE | non (0 choc) | non (0 choc) | 42 | 9 | 5 137 | 1 | 30 | 1 / 1 |
   - G (l'état final de la branche) : mêmes journaux qu'au départ. Sur le test, l'attaquée tient l'intérieur au freinage, l'espace libre est trop petit (« pas la place » ×8) : la règle le retient, comme avant. Sur le technique, il n'arrive jamais à côté avant le freinage (« échappée » à 1,0–1,3 s, « pas à hauteur » à 30–38 m) : la règle n'a pas l'occasion de jouer. Et en course elle coûte (chocs 9, herbe 5137).
   - F : quasi neutre sur les courses (chocs 6 à la limite, herbe 4157 un peu au-dessus), mais le duel ne passe plus nulle part (16 attaques, aucune réussie, 0 choc) : « à hauteur » n'arrive jamais, puisque c'est avant d'y être que le réflexe le retient (il ne cède plus seulement une fois à hauteur, et il n'y arrive pas). Le gel du côté ne suffit pas non plus : le rapide n'arrive jamais à côté au freinage.
   Ce que ça dit :
   - Le rétroviseur arrière seul (B) triple l'herbe : deux règles réglées sur l'ancienne portée de 8 m lisaient tout ce qui est en vue : « entouré » (une voiture à moins de 9,5 m, devant ou derrière → une seule ligne, plus de « continuer ») et le réflexe de côté. Bornées à l'ancienne fenêtre (E), le rétroviseur ne nourrit plus que les erreurs (68 évitées au lieu de 52) et la règle du rattrapé. Il reste un peu d'herbe en trop (4471 ; témoin à 0 m : 3481, les lignes de rechange ne s'ouvrent plus pour une voiture derrière).
   - « Le rattrapé garde sa ligne jusqu'au point de freinage » (IA_RETRO_GARDER) : c'est ce qui donne des victoires surprises (4) mais 19–21 chocs : des voitures bloquées sur leur ligne dans un peloton. Trop brutal tel quel ; il faudrait ne geler que le côté où arrive l'attaquant et seulement quand il est à moins de ~15 m.
   - « L'attaquant ne cède pas » : sans aucune retenue (A, D), le duel test passe au 1er tour sans choc, mais 30 chocs en course (il fonce sur une voiture qui ne lui laisse pas la place) ; à vitesse égale, il ne passe plus.
   - Le vrai verrou du duel sur le technique reste : à 14 m derrière dans les virages, le rapide ne gagne rien, et il doit déjà être à hauteur à l'entrée du virage. Pour qu'il passe, il faudrait qu'il arrive AU FREINAGE à côté (se décaler avant le freinage, à moins de 20 m, et oser le freinage tardif), et que le lent lui laisse ce côté : c'est la règle « garder sa ligne » à affiner (portée, côté).

3. Ce qui est dans la branche : le rétroviseur arrière (IA_RETRO_DISTANCE 40 m, couloir IA_VISION_COULOIR) dans voituresVues, « entouré » et le réflexe bornés à 8 m derrière, les lignes de rechange seulement pour une voiture devant ou à côté, le suivi dans le rétroviseur (pilote.retro : depuis quand, s'est-elle rapprochée de IA_RETRO_RAPPROCHEMENT en IA_RETRO_DUREE), et les deux essais sous interrupteurs ALLUMÉS dans leur version affinée F (IA_RETRO_GARDER 1, IA_RETRO_PROCHE 15, IA_ATTAQUE_SANS_CEDER 1 ; à 0 pour revenir à E). Test de vision mis à jour (voit 20 m derrière dans le couloir, pas 50 m, pas hors couloir).

Sortie des tests sur la branche rebasée (20h21–20h22, sous le verrou) : moteur 137/137 PARTIE OK ; courses 37/38 (herbe hors erreurs 4471 > 4000), 20 voitures 0 / 1 choc. ecrans et annexes pas lancés (pas le temps avant 20h40). Pas de commit sur main.

Ce que je n'ai pas pu vérifier : ecrans.py et annexes sur la branche ; un deuxième passage des 30 courses.

Règles respectées : branche seule, pas de stash, CLAUDE.md intouché, fichiers du Codeur 2 intouchés, verrou pour chaque mesure ; main mis à jour en avance rapide (23ba770) et duel rebasée dessus.

Aucun essai ne tourne, 0 Chrome --headless.

Réévalue.
