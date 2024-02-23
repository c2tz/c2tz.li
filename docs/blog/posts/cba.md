---
authors:
  - c2tz
categories:
  - Windows
  - Batch
  - Développement
comments: true
date: 2024-02-20
---

# Bulk task avec ffmpeg

## Problématique

Je me suis récemment retrouvé face à une petite problématique. Un ami que je nommerai : __*_"rateulere"_*__, se met à regarder des animes japonais.

<!-- more -->

Cette fois-ci il a choisi de regarder un **bon** anime japonais à savoir GTO(1).
{ .annotate }

1.  <figure markdown="span">
      ![Image title](../../assets/images/gto_onizuka_face.jpg){ width="300" loading=lazy }
    <figcaption>Onizuka qui fait une grimace</figcaption>
    </figure>
    
    ??? info "Synopsis GTO"
        Eikichi Onizuka, 22 ans, « célibataire et libre comme l'air », est un jeune professeur au passé douteux qui est nommé pour son premier poste dans une classe difficile ; il montre rapidement une vision de l'enseignement totalement décalée avec les pratiques habituelles. Ses réactions anticonformistes et directes, souvent humoristiques, sont l'axe central de cette série. Il va évoluer avec cette classe, dont la spécialité est de faire craquer moralement leurs professeurs, en tentant de la rallier peu à peu à sa cause.


Je ne vais pas aborder ici ce qu'est ce chef d'oeuvre de l'animation. J'en ferais surement un resumé dans un classement (un jour).

Non ici on va parler code. Revenons en à nos moutons et voyons ensemble le soucis.

Donc ce camarade me demande si par hasard je n'aurai pas à ma disposition ces classiques de l'animation :flag_jp:, j'ai donc décidé de faire les choses bien.

Tout d'abord il faut savoir que je dispose d'un serveur PeerTube(1), celui ci me permet d'y publier des vidéos. Je suis donc en mesure de partager à mon ami rateulere mes épisodes de GTO acquis légalement.
{ .annotate }

1.  <figure markdown="span">
      ![Image title](../../assets/images/logo.svg){ width="150" loading=lazy }
    <figcaption>Logo Peertube</figcaption>
    </figure>
    
    ??? info "C'est quoi peertube ?"
        Eikichi Onizuka, 22 ans, « célibataire et libre comme l'air », est un jeune professeur au passé douteux qui est nommé pour son premier poste dans une classe difficile ; il montre rapidement une vision de l'enseignement totalement décalée avec les pratiques habituelles. Ses réactions anticonformistes et directes, souvent humoristiques, sont l'axe central de cette série. Il va évoluer avec cette classe, dont la spécialité est de faire craquer moralement leurs professeurs, en tentant de la rallier peu à peu à sa cause.

Cependant ces épisodes acquis légalement son au format .mkv avec des .srt intégré à celui ci, en effet tout le monde n'a pas la culture nipone au point de lire couramment des symboles flou pour nous occidentaux.

1- Problème
Le format mkv c'est bien mais c'est aussi une charge supplémentaire pour serveur PeerTube car le transcodage c'est long ca consomme et pour 43 épisodes c'est pas très optimal.

2- Problème
Les .srt ne se mettent pas en sous titre par defaut sur les vidéo peertube. En fait lorsque l'on publie une vidéo sur peertube le transcodage a beau se faire ou ne pas se faire la vidéo que l'on voit n'a pas de sous titre ni incrsuté ni disponible dans les reglage de la vidéo.

Il faut donc rmédier à ces deux petits soucis.

Heuresement j'ai à ma disposition :

- 1 ordinateur **windows**

## Les outils

### ffmpeg

Alors qu'est-ce donc que ces lettres dispatché aleatoirement sur mon ecran. Non en réalité cela signifie quelque chose : (def ffmpeg a mettre)

Cet utilitaire tres puissant c'est un couteau suisse pour l'encodage video. Il peut pratiquement tout faire

etc ... a completer

  [GitHub Pages]: https://pages.github.com/

### batch

Avec l'arrivé de powershell etc ...

=== "test.cmd"

    ``` bash linenums="1"
    @echo off
    chcp 65001 > NUL
    setlocal enabledelayedexpansion

    for /l %%i in (1,1,43) do (
    set "lesson=%%i"
    if %%i lss 10 set "lesson=0%%i"
    set "filename=GTO.-.Leçon.!lesson!.DVDRip.(x264-Ac3)(Fr-5.1+2.0-Jap-2.0)(Sub.Fr).mkv"
    set "filenamenew=GTO.-.Leçon.!lesson!.DVDRip.(x264-Ac3)(Fr-5.1+2.0-Jap-2.0)(Sub.Fr).mp4"
    echo Conversion et extraction des sous-titres pour !filename!...
    ffmpeg -i "!filename!" -c:v copy -c:a copy "!filenamenew!"
    ffmpeg -i "!filename!" -map 0:s:0 "!filename:.mkv=.srt!"
    ffmpeg -i "!filenamenew!" -vf "subtitles=!filename:.mkv=.srt!" "!filenamenew:.mp4=_sub.mp4!"
    del "!filename:.mkv=.srt!"
    )

    echo Conversion et extraction des sous-titres terminées.
    pause
    ```

    The `#!python range()` function is used to generate a sequence of numbers.