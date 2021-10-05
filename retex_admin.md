# RETEX des administrateurs

c ici kon pren cher (pardonnez on est encore dans l'esprit de Berk Willis de temps à autre, le CTF a laissé des traces aux admins également...)

## Écriture du scenario :

Darcosion :

> Il est très dur d'imaginer un scénario d'OSINT pour un CTF car il y a un élément fondamental qui pose soucis dans les CTF : **les dates quasiment jamais réalistes.**.

> Si on imagine la vie d'un personne x en OSINT, il faut disposer de trace sur internet de cette personne à différentes périodes de sa vie (enfance, adolescence, age adulte par exemple). Or un CTF ne peut pas attendre qu'une vie se déroule. Personne n'attends 20 ans pour diffuser son CTF.

> Par conséquence, au mieux, les données à retrouver daterons d'un ans ou deux, au pire de quelques mois. Et cela donne des facilités, à la fois de recherche pour les participants, car ils savent qu'ils peuvent bien souvent éliminer les résultats qui datent d'avant la création du CTF, mais également de triche, car sur certaines plateforme, il est possible de filtrer par date, il est donc possible d'accéder à des informations du CTF par des moyens détournés en supposant sa date de création.

> C'est une erreur que nous avons fait, et pour éviter cela, plusieurs possibilités :
 - soit créer un CTF où la recherche de donnée ne se fait pas sur des sockpuppets créés sur une période de temps courte.
 - soit décréter que les dates n'ont pas de sens, et s'arranger pour que les traces créées soient sur un segment temporel suffisamment large pour interdire ce genre de technique.

 >Il était également très difficile de faire en sorte que les challenge d'OSINT soient réellement de l'OSINT et non du "guessing", c'est à dire des petits indices parsemés qui permettent de *deviner* le flag. En soit, la voie "évidente" lors d'une investigation en OSINT dépend énormément de l'état d'esprit de l'investigateur. Il faut donc imaginer un état d'esprit à mettre lors du CTF, puis arriver à faire coller le plus de challenge à cet état d'esprit. C'est une grosse difficulté que l'on a rencontré car bien que beaucoup de challenges étaient cohérents avec cela, les challenges "et je me balance", "stock" ou encore la partie 'le cerveau' correspondaient beaucoup moins avec cela.

Raven :
> L'écriture du scénario ça a été en grosse partie de ma patte. Il faut dire que j'ai une capacité à raconter n'importe quoi et il m'en faut pas beaucoup pour démarrer une histoire abracadabrante ^^
Quand on a décidé avec Darco de partir sur une menace d'état, il m'en fallait pas plus, test SIGYCOP, DGSI, SDAT, tout y est passé.

> Un point que je n'avais pas prévu, c'est le fait que l'humain est imprévisible. J'entends par là que ma cartographie du CTF faisait du sens dans ma tête et c'était un chemin disons "standard". Et bien pas du tout ! Bon nombre de personnes m'ont DM pour me dire ouais on a tel et tel flag, ça marche pas. Ma carto est donc tombée à l'eau car les chemins évidents pour moi n'étaient pas les mêmes pour les participants.

Unbatal :
> Arrivé après que les premières lignes du scenario aient été décidées, le plus dur a été de chercher de nouvelles idées en restant cohérent. Avec le type de scenario choisi, la tentation est grande de partir dans tous les sens, et donc de perdre le réalisme global.


## Avant le lancement
Darcosion :

> Pour l'infrastructure, nous avions décidés de mettre en place un serveur [CTFd](https://ctfd.io/).
Le setup du CTFd a pris un peu de temps car nous avons choisi de mettre en place un peu de design à nous. Nous avons à ce moment créé notre bannière, un fichier d'icon pour son onglet, ainsi que quelques fix CSS, le plus important étant le fixe de taille d'image dans les challenges via l'ajout d'une classe bootstrap :
> ```
> class="img-fluid"
> ```

> Ce dernier stockait tout dans une base de donnée sqlite, et il semblerait que de temps en temps, il ai eu du mal à gérer la base de donnée car cette dernière à crash 3 fois durant le CTF.

>Par ailleurs, nous avons fait une chose **qu'il ne faut jamais faire** : lancer le CTFd sous la forme d'un processus en arrière plan et non d'un daemon.

> Basiquement, notre commande de lancement du ctfd était :

> ```bash
> nohup manage.py runserver &
> ```

>Ce qui fait que si le serveur tombait hors ligne, l'un d'entre nous aurait dû se reconnecter manuellement pour le relancer.

>Par ailleurs, les sites onions étaient présents sur un raspberry pi dans mon salon.
>Il n'y avait aucun moyen de s'y connecter à distance, il n'y avait aucun mécanisme de stabilité (en dehors des daemon tor & nginx). On était littéralement à poil et c'est un **MIRACLE** que l'onion soit resté en ligne toute la durée du CTF, sachant que j'ai du partir de chez moi deux semaines, ce qui signifie que je n'aurai eu quasiment aucun moyen de rétablir la situation.

Raven:
> Je n'aurais pas honte de dire que c'est à Darco que revient tout le mérite de l'infra et la gestion du CTFd. Il a géré ça de son côté, mise en place, troubleshooting, mise en place des challs etc. Donc GG à lui, j'ai juste eu à mettre les énoncés, les flags et les hints donc rien de bien compliqué.

Unbatal:
> La partie infra a été magnifiquement gérée par Darco. Pour ma part, il s'est surtout agit de relire les challenges, et de s'assurer qu'un flag n'a pas disparu. Pour la gestion des nombreux comptes, nous aurions mieux fait d'utiliser dès le début un gestionnaire de mots de passes.

## Lancement

darcosion :
>Le lancement du CTF a été un peu catastrophique car nous n'avions pas préparé nos interventions sur le discord et en dehors.

> A ce niveau là, plusieurs situations ont été drôle et ridicules à la fois. Par exemple nous avions fait une première annonce pour indiquer notre CTF mais nous avions oubliés de mettre le lien du CTF dans l'annonce. Puis nous avons placé le code d'accès `osintVPN` au lieu du code `rosoVPN`, ce qui rendait l'inscription impossible.

> Il faut aussi savoir que nous n'avions pas terminés 100% des challenges avant de lancer le CTF (il en manquait quelques unes). Et cela c'est à mon avis ressenti sur le sens du scénario du CTF qui s'est un peu retrouvé amputé d'une part de son sens.


Raven :

> Comme l'a dit Darco, le début du CTF fut un peu chaotique. En effet, le nombre de DM en mode j'ai oublié mon password, je comprends pas, comment on fait, est-ce que c'est le bon flag, etc. sont devenus monnaie courante. Au bout de 3 jours globalement c'était bon et il ne restait plus que les gens qui ne pouvaient pas flag (mauvais flag, mauvais chall, des choses normales dans un CTF quoi)
> Par contre, nous n'avions vraiment pas prévu tant d'engouement, bon nombre de personne s'y sont mise à fond et on a eu des premiers jours très chargés. J'en profite ici pour dire que j'étais assez inquiet de savoir si le CTF allait plaire, si vous alliez vous amuser etc. et j'ai été très vite rassuré. J'ai d'ailleurs beaucoup ri en vous lisant ou en écoutant vos bêtises :D

Unbatal:
> Je n'ai malheureusement pas été disponible pour suivre le lancement du CTF.

## Pendant le CTF

darcosion :

>Une grosse problématique que nous avions était le format des flags.
>La plupart des flags ont le format `CTF{flag}` ou `flag{flag}` (nous ne nous étions pas accordés sur le format générique #DebilosForever).

>Et les flags n'ayant pas ce format étaient souvent des flags avec des localisations.  
>Or nous nous étions accordés sur l'utilisation de google maps pour déterminer le texte exacte des challenges GEOINT.  
>Le format pour cela était donc complexe car beaucoup de gens n'ont pas utilisés google maps, beaucoup de gens ont fait des copié-collé avec des espaces en plus, et parfois nous avions oubliés de rendre le flag insensible à la casse.

>Un autre reproche qu'on peut avoir (en particulier à moi) était d'être trop présent lors du CTF, particulièrement en vocal. D'une part, il y a toujours le risque de laisser échapper un indice accidentellement comme cela, et d'autre part, il y avait le risque de fatiguer tout le monde a être trop enjoué & prolixe sur le vocal.

Raven :
> Pendant que Darco passait sa vie sur le vocal (je pense qu'il a pas dormi en 2 semaines ce fou), j'ai plutôt fait du SAV en DM, donnant un coup de main au besoin et essayant de me rendre disponible au maximum. J'ai également eu droit à du SAV IRL car bon nombre d'amis proches ont participé.

Unbatal :
> Quelques apparitions en vocal ont permis à certains de poser leurs questions, ou de demander un peu d'aide.

## Ressenti

Raven :
> Bon il parait que c'est ici qu'on décrit ce qu'on a ressenti pendant le CTF.
> Pour être tout à fait honnête avec vous, j'ai pris beaucoup de plaisir à créer ce CTF, les longues soirées à raconter de la merde avec mes 2 compères et a trouver des idées plus farfelues les unes que les autres étaient vraiment sympas !
> Tout le long de la préparation, j'ai eu peur que le CTF ne plaise pas, et le poti Darco m'a dit "T'inquiète il est super cool le CTF !"
> Et ba il avait raison ce bougre, jour 1 j'ai eu envie de faire le CTF en tant que participant tant je voyais les autres s'amuser :p
> Et pendant le CTF j'ai également été content de pouvoir aider les gens et cela m'a permis de faire des belles rencontres.
> Pour résumer : je me suis éclaté pendant la prépa et le déroulement du CTF, pour ne rien vous cacher c'était le premier CTF ou j'avais un rôle d'orga comme ça, ça fait plaisir de passer de l'autre côté de la barrière. Je referai sans doute des CTFs dans le futur mais peut-être plus sérieux. Et pourquoi pas avec Darco et UnBatal, on fait une bonne team je trouve.  
> Bisous, le Corbeau

Unbatal :
> La préparation du CTF a été vraiment plaisante. Quelques soirées hilarantes à écrire tout ce qui nous passait dans la tête pour créer de l'activité sur les comptes, des moments plus sérieux pour monter les challenges Dark, à rédiger, à relire.  
> Si la première partie était plutôt détendue, dès que l'on a commencé à annoncer le CTF, et en voyant a quel point ça a intéressé de monde, la pression est montée. Le CTF est-il a la hauteur des attentes ? C'est a vous de nous le dire !  
> Si j'ai un regret, c'est de ne pas avoir pu être suffisamment présent pendant le CTF. Un gros GG à Darco et Raven qui ont magnifiquement tenus la boutique !!  
> Au bilan : c'était le premier CTF auquel j'ai contribué. Ca été un pur plaisir de le faire avec mes deux comparses. Je nous ai trouvé très complémentaires, et l'ambiance que l'on a eu dans la préparation me donne envie de recommencer.  
> la Biz, le Bateau

Darcoion :

> Alors pour ma part, ce CTF a été une grande aventure et un grand défoulement.
> Sur OSINT-FR on avait accumulé un tas de site absurde, un tas d'histoire et de blagues débiles et c'est comme si en un CTF, on avait tout réutilisé d'un coup.  
> Je garderais un souvenir impérissable de nos soirées de rigolades à inventer les challenges, mais aussi des moments d'illumination qu'on a eu à pleins de moment à chaque fois qu'on bloquait, pour trouver une nouvelle idée débile, une nouvelle façon de présenter un challenge ou une nouvelle façon de perturber/traumatiser les participants.  
> Tout au long du CTF, j'ai pu observer des dizaines de personnes se creuser la cervelle, réfléchir, grogner et éclater de rire sur les différents challenges, et quand je vois tout ce que la communauté OSINT-FR a fait en deux semaines, je ne regrette en aucune façon ce CTF.    
> jeeeez, darcosion
