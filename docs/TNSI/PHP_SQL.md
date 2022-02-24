## <center>PHP et SQL </center>

### I] La base de données



![Capture d’écran 2021-11-22 à 23.10.07](/Users/ericgaland/Documents/Capture%20d%E2%80%99e%CC%81cran%202021-11-22%20a%CC%80%2023.10.07.png)

### II ] Accès à la base de données

```php
try
{
$bdd = new PDO('mysql:host=localhost:8080;dbname=test;charset=utf8', 'root', '');
}

catch(Exception $e)
{
        die('Erreur : '.$e->getMessage());
}
```



### III] Passage de la requête SQL

```php
SQL = 'SELECT nom FROM jeux_video'
$reponse = $bdd->query(SQL);
```

### IV] Gestion de l'affichage

```php
while ($donnees = $reponse->fetch())
{
    echo $donnees['nom']. '<br />';
}
```



### V] Code complet

```php
<?php
try
{

	$bdd = new PDO('mysql:host=localhost;dbname=test;charset=utf8', 'root', '');
}
catch(Exception $e)
{
        die('Erreur : '.$e->getMessage());
}


$reponse = $bdd->query('SELECT nom FROM jeux_video');

while ($donnees = $reponse->fetch())
{
    echo $donnees['nom']. '<br />';
}

?>
<?php


$reponse->closeCursor(); 

?>
```



<u>Remarque</u> : il faut enregistrer le fichier PHP sous htdocs.

### IV] Résultat

Super Mario Bros
Sonic
Zelda : ocarina of time
Mario Kart 64
Super Smash Bros Melee
Dead or Alive
Dead or Alive Xtreme Beach Volley Ball
Enter the Matrix
Max Payne 2
Yoshi's Island
Commandos 3
Final Fantasy X
Pokemon Rubis
Starcraft
Grand Theft Auto 3
Homeworld 2
Aladin
Super Mario Bros 3
SSX 3
Star Wars : Jedi outcast
Actua Soccer 3
Time Crisis 3
X-FILES
Soul Calibur 2
Diablo
Street Fighter 2
Gundam Battle Assault 2
Spider-Man
Midtown Madness 3
Tetris
The Rocketeer
Pro Evolution Soccer 3
Ice Hockey
Sydney 2000
NBA 2k
Aliens Versus Predator : Extinction
Crazy Taxi
Le Maillon Faible
FIFA 64
Qui Veut Gagner Des Millions
Monopoly
Taxi 3
Indiana Jones Et Le Tombeau De L'Empereur
F-ZERO
Harry Potter Et La Chambre Des Secrets
Half-Life
Myst III Exile
Wario World
Rollercoaster Tycoon
Splinter Cell

