# Compte-rendu TP-03

### Exercice : paramètres

**analyse.sh**

```sh
#!/bin/bash

echo 'Bonjour vous avez rentré ' $# ' paramètres'
echo 'Le nom du script est ' $0
echo 'Le 3ème paramètre est ' $3
echo 'Voici la liste des paramètres : '$@
```

### Exercice : vérification du nombre de paramètres

**concat.sh**

```sh
#!/bin/bash

if [ $# -gt 2 ]
then
  echo 'Vous devez rentrer au maximum 2 paramètres'
else
  concat="$1$2"
  echo $concat
fi

```

### Exercice : argument type et droits

**test-fichier.sh**

```sh
#!/bin/bash

if [ -a $1 ]
then
  echo "Le fichier $0 est un fichier ordinaire"
elif [ -d $1 ]
then
  echo "Le fichier $0 est un répertoire"
else
  echo "Le fichier n'éxiste pas"
fi

if [ -w $1 ]
then
  echo "L'écriture du fichier $0 est possible"
elif [ -r $1 ]
then
  echo "Le fichier $0 est lisible"
else
echo "Le droit d'écrire ou lire le fichier est interdit"
```

### Exercice : Afficher le contenu d’un répertoire

**listedir.sh**

```sh
#!/bin/bash

rep_current=$(pwd)
rep_list=$(ls)

for item in $rep_list
  do
    if [ -d $item ]
    then
      echo $item
    fi
  done

for item in $rep_list
  do
    if [ -f $item ]
    then
      echo $item
    fi
  done
```

### Lecture au clavier

- Comment quitter more ?

La touche **q** permet de quitter more.

- Comment avancer d'une ligne ?

La touche **s** permet d'avancer d'une ligne.

- Comment avancer d'une page ?

La touche **espace** permet d'avancer d'une page.

- Comment remonter d'une page ?

La touche **b** permet de remonter d'une page.

###

**notes.sh**

```sh
echo -n "Veuillez saisir une note : "
read note

if [[ "$note" -ge 16 && "$note" -le 20 ]]
then
  echo "Très bien"
elif [[ "$note" -ge 14 && "$note" -le 16 ]]
then
  echo "Bien"
elif [[ "$note" -ge 12 && "$note" -le 14 ]]
  then
  echo "Assez bien"
elif [[ "$note" -ge 10 && "$note" -le 12 ]]
then
  echo "Moyen"
else
  echo "Insuffisant"
fi

while true; do
  echo -en "Appuyer sur q pour quitter : "
  read input

  if [[ "$input" = "q" ]] || [[ "$input" = "Q" ]]
  then
    break
  else
    echo "Saisie invalide, appuyer sur q."
  fi
done
```
