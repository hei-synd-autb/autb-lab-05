<h1 align="left">
  <br>
  <img src="./img/hei-en.png" alt="HEI-Vs Logo" width="350">
  <br>
  HEI-Vs Engineering School - Industrial Automation Base
  <br>
</h1>

Cours AutB

Author: [Cédric Lenoir](mailto:cedric.lenoir@hevs.ch)

# LAB 05 Mise en service d'un axe électrique avec une vis à bille.

Job start with:

# CtrlX Drive Engineering
Ce logiciel est conçu pour:
-   Visualiser et si nécessaire modifier les paramètres des axes électriques.
-   Visualier le comportement de l'axe à l'aide d'un oscilloscope intégré.
-   Piloter l'axe en mode manuel pour optimiser son comportement.
-   Lancer une procédure de **Auto-Tuning**.

<figure>
    <img src="./img/ctrlX Drive Engineering.png"
         alt="Image lost: ctrlX Drive Engineering">
    <figcaption>Use CtrlX Drive Engineering</figcaption>
</figure>

# Connect

Se connecter au drive avec USB-C, utiliser l’axe X.
Si possible en utilisant son propre PC pour garder le PC labo libre.
 
<figure>
    <img src="./img/DriveSelectConnection.png"
         alt="Image lost: DriveSelectConnection.png">
    <figcaption>Connection to drive with USB-C</figcaption>
</figure>

> Il est possible de se connecter de différentes manières.

# Backup
Sauvegarder les paramètres actuels pour pouvoir les restaurer si nécessaire.

Avant de sauvegarder les paramètres, il est préférable de passer en mode PM, Parameter Mode. Pour cela, le moteur ne doit pas être sous tension.

SelectParameterMode
<figure>
    <img src="./img/SelectParameterMode.png"
         alt="Image lost: SelectParameterMode">
    <figcaption>Set Axis in PM, Parameter Mode</figcaption>
</figure>
 
<figure>
    <img src="./img/Save_Backup_Parameters.png"
         alt="Image lost: /img/Save_Backup_Parameters.png">
    <figcaption>Save a backup of drive parameters to restore them if needed</figcaption>
</figure>

Les paramètres sont numérotés selon le sysème [Sercos](https://www.sercos.org).
Une multitude de paramètres sont accessibles en Realtime ou Non Realtime, en lecture ou en écriture. Certains paramètres ne peuvent être modifiés que quand le moteur est hors couple, voir même quand le drive est en mode Paramter.

- **Backup parameter**s pour les paramètres de configuration.
- **All parameters**, archive absolument tous les paramètres. Ceci est utile pour faire un diagnostic, ou dans le cadre d'un cours pour présenter un axe uniquement sous forme de paramètres.

Après avec archivé les paramètres, restaurer le mode OM.

<figure>
    <img src="./img/ActivateOperatingMode.png"
         alt="Image lost: ActivateOperatingMode">
    <figcaption>Restore OM Operating Mode</figcaption>
</figure>

# Scaling
L'axe doit connaitres les paramètres mécaniques du système pour pouvoir convertir la position du codeur en unités qui conviennent à l'application.

Dans notre cas de figure, la position du codeur est convertie, entre autre, en mm pour la position linéaire de l'axe X.

<figure>
    <img src="./img/AxisMechanicalScaling.png"
         alt="Image lost: AxisMechanicalScaling">
    <figcaption>Go to Axis Mechanical Scaling</figcaption>
</figure>

Pour faciliter l'interprétation des résultats, nous modifions un paramètre afin que le système convertisse le couple du moteur en Force pour la lecture de l'effort linéaire en sortie de la vis à bille.

<figure>
    <img src="./img/ChangeScalingToForce.png"
         alt="Image lost: /img/ChangeScalingToForce">
    <figcaption>Change scaling to force</figcaption>
</figure>

Il faut noter qu'un changement d'unité ne peut pas se faire sous n'importe quelle condition. L'axe doit être en mode **CM**, **Configuration Mode**, pour autoriser un changement d'unité.

<figure>
    <img src="./img/ConfigurationMode.png"
         alt="Image lost: GoToParameterModeAgain">
    <figcaption>You must be in Configuration Mode to modify a scaling parameter</figcaption>
</figure>

# Piloter le moteur en mode manuel


# Trace data
Tracer une courbe classique Position, vitesse, accélération ou torque et erreur de poursuite. 20 minutes.

# Mesurer la force nécessaire a faible vitesse constante
	Comparer avec les spécifications du moteur
# Mesurer la force nécessaire pour vaincre le frottement statique.

# Estimer la masse en mouvement à l’aide de l’auto-tuning.

# Faire un tuning manuel est le comparer avec l’auto-tuning.

> Attention, feed-forward ; P-0-1126.0.0 à 0 !

> Conditions de départ :
- S-0-0100 = 1000 * l’inertie du moteur = 1000 * P-0-0510.
- S-0-0101 = 0 [ms] sans intégrateur
- P-0-0510 = 0.0001600

- Donc 0.16

Avec mon essai S-0-0100, commence à siffler vers 0.5, je mets 0.25
Je passe S-0-0101 à 10 ms pour commencer, siffle vers 0.6, je fixe à 1.2
Ensuite, je trace.
 
Les valeurs à afficher sur la fenêtre de paramètres
On peut aussi importer cette liste, voir WatchListForTuning.ipg ou la sauver.
 
# Visualise your data
 
Tracer les courbes sur 4 secondes pour :
S-0-0084	Force
S-0-0051	Position
S-0-0040	Vitesse
S-0-0347	Erreur de vitesse

 
Start et automatic scaling quand le signal est disponible
 
Commenter le graph
Mesure de vitesse.
 
 
Position
Vérifier ce qui se passe en mode position avec S-0-0104 = 1
 
Passer en mode positionning
 
Tracer cette fois l’erreur de poursuite S-0-0189


Maximiser l’affichage de l’erreur de poursuite
 

Comparer avec l’auto-tuning
 
Configuré sans feed-forward et sans filtre.

 
 
Afficher les résultats et commenter

Comparer Load Inertia : 0.0003421 avec celle du moteur 0.0001600
Votre commentaire…
Tracer à nouveau et comparer
Essayer avec Feed-Forward et comparer
Mon résultat avec Auto-tuning
 
Fin du Tuning
Mesure du frottement dynamique
Utiliser le mode vitesse, mais sur +- 50 mm pour faire cette mesure, augmenter le temps de mesure sur la trace
Faire des mesures à 600 mm/min
Puis 1200, 1800 et 2400…6000 (soit 100 mm/s)
Utiliser click droit pour visualiser les données :
 
Note : j’ai 328 N à 600
386 à 1200	
430 à 1800
462 à 2400
485 à 3000
554 à 6000
Mesurer le courant du moteur à 6000 et à partir du courant nominal estimer la charge du moteur.
Mesurer la température du moteur.
Aller chatouller les limites de couple du drive
Frottement dynamique
Passer en mode couple et prudemment estimer la force minimale pour commencer à bouger le moteur.
 

En finalité
Préparer un mouvement sur +/2 50 mm avec une vitesse de 600 mm.
Proposer votre tunning idéal, le justifier et le commenter.
Ne pas quitter la salle avant le feu vert d’un prof ou assistant qui puisse vérifier que votre tuning permet à l’axe de fonctionner correctement.

# Questions:
-   Quels est la tension sur le bus DC ?
-   Quels sont les registres que le PLC envoie au drive?
-   Quel registre permet au PLC de connaitre la position du moteur ?
-   Pourquoi est-il, dans notre cas, inutile de configurer le codeur ?
-   Combien de points par tour le moteur de l'axe X reçoit-il via le bus Ethercat lorsque la limite de vitesse de l'axe X est atteinte ?
-   Expliquer pourquoi le moteur de l'axe X semble surdimensionné par rapport au couple maximal admissible par la vis à billes.
-   A quoi sert le frein sur l'axe Z ?


# Ne pas quitter la salle avant d'avoir restauré les paramètres !
