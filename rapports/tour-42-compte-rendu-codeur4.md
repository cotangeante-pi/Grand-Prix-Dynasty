TOUR 42 — compte rendu du Codeur 4 (les IA en voiture vivante, reprise du travail du Codeur 1 ; branche ia-vivante)
Commits : 6f66c6f, 3160c56 (« en cours »), main 932832b fusionné. Rien à fusionner : objectif pas atteint. ia.js rendu au Codeur 1.
Décision du Chef (2026-10-30) : on ne touche pas à physique.js ce soir ; les IA restent hors voiture vivante (VIVANTE_IA = 0).

Ajouté dans ia.js (tout derrière VIVANTE_IA ; à 0 rien n'est lu), réglages dans donnees.js :
  - IA_VIVANTE_BRAQUAGE (0,3) : au-delà de ce braquage, l'IA freine d'autant moins (rien à fond de braquage) ;
  - IA_VIVANTE_BRAQUAGE_FREIN (0 = coupé) : l'autre façon, au-dessus de ce frein elle ne braque plus qu'à IA_VIVANTE_BRAQUAGE ;
  - IA_VIVANTE_MARGE (1) : la marge de freinage de sa ligne (plus petite = elle freine plus tôt) ;
  - IA_VIVANTE_VIRAGE (1) : la vitesse visée dans les virages (× la limite du pilote).

Mesures (calcul pur, osascript, IA seule, légende, circuit test, 3 tours ; outil : scratchpad codeur4/iav/jxa.py + iav.js) :
  | réglage (VIVANTE_IA = 1) | tours (s) | herbe | barrières |
  |---|---|---|---|
  | sans voiture vivante (VIVANTE_IA = 0) | 52,35 / 47,44 / 47,49 | 0 | 0 |
  | départ du Codeur 1 (frein 0,6, gaz en rampe) | 64,9 / 239,7 / 205,5 | 40 481 | 37 198 |
  | + frein réduit au-delà de 0,3 de braquage | 226,6 / 205,7 / 175,6 | 52 363 | 48 151 |
  | + IA_VIVANTE_MARGE 0,8 | 58,3 / 162,0 / 227,8 | 33 792 | 31 865 |
  | braquage limité à 0,3 au-dessus de 0,2 de frein | 159,5 / 216,2 / 57,0 | 31 457 | 29 095 |
  | VIRAGE 0,9 + MARGE 0,8 | 347,7 / 261,4 / 130,7 | 67 133 | 61 837 |
  | VIRAGE 0,85 + MARGE 0,8 | 396,1 / 187,8 / 441,4 | 100 796 | 96 257 |
  | VIRAGE 0,8 + MARGE 0,7 | 141,9 / 285,7 / 186,6 | 51 030 | 47 725 |

Diagnostic : ni freiner droit, ni freiner plus tôt, ni viser 10 à 20 % moins vite dans les virages n'empêchent les tête-à-queue. Les
glissades partent aussi sans frein et même plus lentement (44 à 54 m/s, gaz 0 à 0,35, braquage 0,8 à 1) : c'est l'arrière de la voiture
vivante qui décroche au lever de pied et en plein braquage, pas seulement le freinage de l'IA. La suite est dans physique.js (le délestage
de l'arrière, VIVANTE_ADHERENCE_ARRIERE, VIVANTE_CERCLE_ARRIERE), ce qui changerait aussi la voiture du joueur : à décider par Elijah.
