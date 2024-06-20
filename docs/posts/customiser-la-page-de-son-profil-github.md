---
date: 2024-03-07
authors: [c2tz]
description: >
  Tutoriel simple pour apprendre à personaliser les éléments de
  sa page GitHub
categories:
  - Général
  - Développement
comments: true
hide:
  - feedback
---

# Customiser la page de son profil GitHub

L'objectif de ce post va être de vous apprendre à customiser votre page d'accueil GitHub. Il est déstiné à un public débutant donc n'importe qui peut y arriver.

!!! question "GitHub, quezako ?"

    Pour les quelques ploucs (1) comme le **J** ou le **R** qui ne sont pas des nerds tel que le **C**, le **RE** ou encore le **H** voici ma définition simple.
    { .annotate }

    1.  <figure markdown="span">
          ![Plouk couverture](/assets/images/plouk.jpg){ width="200px" }
          <figcaption>Couverture d'un livre pour enfants qui s'appelle "plouk"</figcaption>
        </figure>

    C'est comme un réseau social pour les développeurs, où ils peuvent héberger le code source de leurs projets informatique, suivre les modifications apportées par d'autres personnes, proposer des modifications (appelées "pull requests"), et travailler ensemble pour améliorer des logiciels. ==Un jour== j'essaierai de faire un article plus complet sur le sujet.

Après tout si j'ai réussi n'importe qui peut le faire.

<!-- more -->

Voici un exemple de ce que vous pouvez obtenir facilement en suivant ce tutoriel détailé :
<figure markdown="span">
  ![Image title](/assets/images/github_c2tz_profil_light.png#only-light){ width="auto" }
  ![Image title](/assets/images/github_c2tz_profil_dark.png#only-dark){ width="auto" }
  <figcaption><a href="https://github.com/c2tz">Exemple</a> provenant de ma page d'accueil GitHub</figcaption>
</figure>
    
## A quoi ca sert de customiser son profil ?

Répondons à cette question de la facon la plus objective possible: customiser sa page de profil GitHub ca sert à rien.

Bon nombre de développeur plus chevronné que moi se fiche totalement de l'apparence que cet élément peut avoir. Tant que celui-ci reste pratique, fonctionnel et peu encombrant à leurs yeux, chose que je comprend tout à fait.

C'est en fait un élément de décoration ou une sorte de vitrine.

Mais si des options existes pour améliorer l'apparence que cette vitrine peut avoir alors autant les utilisé si on le souhaite.

Un peu comme un site sans CSS : il fonctionne mais il est laid :stuck_out_tongue_closed_eyes:.

## Par où commencer ?

Il vous faudra 1 PC :

- [ ] Windows 10 et +
    * [ ] SSH [^1] (Faculatif si GIT)
    * [ ] Paint ou alternative
- [ ] 1 Compte GitHub actif
- [ ] [GIT](https://git-scm.com/downloads)
- [ ] [GitHub Desktop](https://desktop.github.com/) [^2] (Faculatif si GIT)
[^1]:
  Dans une certaine mesure SSH n'est pas nécessaire étant donné que GIT embarque déja son propre client SSH. Mais je trouve que le [Terminal Windows](https://learn.microsoft.com/fr-fr/windows/terminal/install) est plus confortable d'utilisation.
[^2]:
  Seulement et si seulement vous êtes ce que l'on appelle un newbie et que vous êtes confrontée à des merge resolve (car bien evidemment vous ne connaissez pas les commandes GIT par :heart:)

### Usage de ces logiciels

#### Windows 10 et +

Linux fonctionne aussi bien et les commandes GIT sont les mêmes.
Tout cela peut même fonctionner avec un téléphone Android et l'application [Termux](https://termux.dev/en/) mais c'est pas pratique mieux vaut donc un PC Windows comme :people_holding_hands: tout le monde.

#### SSH

Comme dit [ici](#fn:1) SSH peut être utilisé si vous avez trouver la CLI de GIT trop peu ergonomique pour vous, ou un peu vieillote mais pour les quelques commandes qui vont être tapé cela est suffisant.

A vous donc de voir si vous voulez utiliser :

- Utiliser OpenSSH (Windows)
- Utiliser GitSSH (GIT)

Si vous utilisez OpenSSH je vous invite à regarder l'info bulle qui est ci-dessous.

??? info "Commande SSH Windows"
    === "Super SSH fonctionne :smiley:"
        Vous avez ceci :

        ![Image title](/assets/images/cmd_ysB4dFypKv.png){ width="auto" }

        <figure markdown="span">
        <iframe width="700" height="315" src="https://www.youtube-nocookie.com/embed/0uU-VkeSswY?si=migZ8NJPmZlSe2lS&amp;controls=0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; "></iframe>
        <figcaption>C'est bien Éléonore on est content</figcaption></figure>

    === "Aïe cela ne fonctionne pas :sob:"
        Vous avez ceci :

        ![Image title](/assets/images/cmd_nlubOX7U8G.png){ width="auto" }

        Ca signifie juste que SSH n'est pas activé, normalement il suffit de faire ceci :
        
        1. ++win+r++ :octicons-arrow-right-16: ` control appwiz.cpl,,2 ` :octicons-arrow-right-16: cocher "OpenSSH"
        2. redemarrer le PC

```
.
├─ docs/
│  └─ stylesheets/
│     └─ extra.css
└─ mkdocs.yml

```

Then, add the following lines to `mkdocs.yml`:

``` yaml
extra_css:
  - stylesheets/extra.css
```

### Additional JavaScript

If you want to integrate another syntax highlighter or add some custom logic to
your theme, create a new JavaScript file in the `docs` directory:

``` { .sh .no-copy }
.
├─ docs/
│  └─ javascripts/
│     └─ extra.js
└─ mkdocs.yml
```

Then, add the following lines to `mkdocs.yml`:

``` yaml
extra_javascript:
  - javascripts/extra.js
```

??? tip "How to integrate with third-party JavaScript libraries"

    It is likely that you will want to run your JavaScript code only
    once the page has been fully loaded by the browser. This means
    installing a callback function subscribing to events on the
    `document$` observable exported by Material for MkDocs.
    Using the `document$` observable is particularly important if you
    are using [instant loading] since it will not result in a page
    refresh in the browser - but subscribers on the observable will be
    notified.

    ``` javascript
    document$.subscribe(function() {
      console.log("Initialize third-party libraries here")
    })
    ```

    `document$` is an [RxJS Observable] and you can call the `subscribe()`
    method any number of times to attach different functionality.

  [instant loading]: setup/setting-up-navigation.md/#instant-loading
  [RxJS Observable]: https://rxjs.dev/api/index/class/Observable

## Extending the theme

If you want to alter the HTML source (e.g. add or remove some parts), you can
extend the theme. MkDocs supports [theme extension], an easy way to override
parts of Material for MkDocs without forking from git. This ensures that you
can update to the latest version more easily.

  [theme extension]: https://www.mkdocs.org/user-guide/customizing-your-theme/#using-the-theme-custom_dir

### Setup and theme structure

Enable Material for MkDocs as usual in `mkdocs.yml`, and create a new folder
for `overrides` which you then reference using the [`custom_dir`][custom_dir]
setting:

``` yaml
theme:
  name: material
  custom_dir: overrides
```

!!! warning "Theme extension prerequisites"

    As the [`custom_dir`][custom_dir] setting is used for the theme extension
    process, Material for MkDocs needs to be installed via `pip` and referenced
    with the [`name`][name] setting in `mkdocs.yml`. It will not work when
    cloning from `git`.

The structure in the `overrides` directory must mirror the directory structure
of the original theme, as any file in the `overrides` directory will replace the
file with the same name which is part of the original theme. Besides, further
assets may also be put in the `overrides` directory:

``` { .sh .no-copy }
.
├─ .icons/                             # Bundled icon sets
├─ assets/
│  ├─ images/                          # Images and icons
│  ├─ javascripts/                     # JavaScript files
│  └─ stylesheets/                     # Style sheets
├─ partials/
│  ├─ integrations/                    # Third-party integrations
│  │  ├─ analytics/                    # Analytics integrations
│  │  └─ analytics.html                # Analytics setup
│  ├─ languages/                       # Translation languages
│  ├─ actions.html                     # Actions
│  ├─ alternate.html                   # Site language selector
│  ├─ comments.html                    # Comment system (empty by default)
│  ├─ consent.html                     # Consent
│  ├─ content.html                     # Page content
│  ├─ copyright.html                   # Copyright and theme information
│  ├─ feedback.html                    # Was this page helpful?
│  ├─ footer.html                      # Footer bar
│  ├─ header.html                      # Header bar
│  ├─ icons.html                       # Custom icons
│  ├─ language.html                    # Translation setup
│  ├─ logo.html                        # Logo in header and sidebar
│  ├─ nav.html                         # Main navigation
│  ├─ nav-item.html                    # Main navigation item
│  ├─ pagination.html                  # Pagination (used for blog)
│  ├─ palette.html                     # Color palette toggle
│  ├─ post.html                        # Blog post excerpt
│  ├─ progress.html                    # Progress indicator
│  ├─ search.html                      # Search interface
│  ├─ social.html                      # Social links
│  ├─ source.html                      # Repository information
│  ├─ source-file.html                 # Source file information
│  ├─ tabs.html                        # Tabs navigation
│  ├─ tabs-item.html                   # Tabs navigation item
│  ├─ tags.html                        # Tags
│  ├─ toc.html                         # Table of contents
│  ├─ toc-item.html                    # Table of contents item
│  └─ top.html                         # Back-to-top button
├─ 404.html                            # 404 error page
├─ base.html                           # Base template
├─ blog.html                           # Blog index page
├─ blog-archive.html                   # Blog archive index page
├─ blog-category.html                  # Blog category index page
├─ blog-post.html                      # Blog post page
└─ main.html                           # Default page
```

  [custom_dir]: https://www.mkdocs.org/user-guide/configuration/#custom_dir
  [name]: https://www.mkdocs.org/user-guide/configuration/#name

### Overriding partials

In order to override a partial, we can replace it with a file of the same name
and location in the `overrides` directory. For example, to replace the original
`footer.html` partial, create a new `footer.html` partial in the `overrides`
directory:

``` { .sh .no-copy }
.
├─ overrides/
│  └─ partials/
│     └─ footer.html
└─ mkdocs.yml
```

MkDocs will now use the new partial when rendering the theme. This can be done
with any file.

### Overriding blocks <small>recommended</small> { #overriding-blocks data-toc-label="Overriding blocks" }

Besides overriding partials, it's also possible to override (and extend)
template blocks, which are defined inside the templates and wrap specific
features. In order to set up block overrides, create a `main.html` file inside
the `overrides` directory:

``` { .sh .no-copy }
.
├─ overrides/
│  └─ main.html
└─ mkdocs.yml
```

Then, e.g. to override the site title, add the following lines to `main.html`:

``` html
{% extends "base.html" %}

{% block htmltitle %}
  <title>Lorem ipsum dolor sit amet</title>
{% endblock %}
```

If you intend to __add__ something to a block rather than to replace it
altogether with new content, use `{{ super() }}` inside the block to include the
original block content. This is particularly useful when adding third-party
scripts to your docs, e.g.

``` html
{% extends "base.html" %}

{% block scripts %}
  <!-- Add scripts that need to run before here -->
  {{ super() }}
  <!-- Add scripts that need to run afterwards here -->
{% endblock %}
```

The following template blocks are provided by the theme:

| Block name        | Purpose                                         |
| :---------------- | :---------------------------------------------- |
| `analytics`       | Wraps the Google Analytics integration          |
| `announce`        | Wraps the announcement bar                      |
| `config`          | Wraps the JavaScript application config         |
| `container`       | Wraps the main content container                |
| `content`         | Wraps the main content                          |
| `extrahead`       | Empty block to add custom meta tags             |
| `fonts`           | Wraps the font definitions                      |
| `footer`          | Wraps the footer with navigation and copyright  |
| `header`          | Wraps the fixed header bar                      |
| `hero`            | Wraps the hero teaser (if available)            |
| `htmltitle`       | Wraps the `<title>` tag                         |
| `libs`            | Wraps the JavaScript libraries (header)         |
| `outdated`        | Wraps the version warning                       |
| `scripts`         | Wraps the JavaScript application (footer)       |
| `site_meta`       | Wraps the meta tags in the document head        |
| `site_nav`        | Wraps the site navigation and table of contents |
| `styles`          | Wraps the style sheets (also extra sources)     |
| `tabs`            | Wraps the tabs navigation (if available)        |

## Theme development

Material for MkDocs is built on top of [TypeScript], [RxJS] and [SASS], and
uses a lean, custom build process to put everything together.[^3] If you want
to make more fundamental changes, it may be necessary to make the adjustments
directly in the source of the theme and recompile it.

  [^4]:
    Prior to <!-- md:version 7.0.0 --> the build was based on Webpack, resulting
    in occasional broken builds due to incompatibilities with loaders and
    plugins. Therefore, we decided to swap Webpack for a leaner solution which
    is now based on [RxJS] as the application itself. This allowed for the
    pruning of more than 500 dependencies (~30% less).

  [TypeScript]: https://www.typescriptlang.org/
  [RxJS]: https://github.com/ReactiveX/rxjs
  [SASS]: https://sass-lang.com

### Environment setup

First, clone the repository for the edition you want to work on. If
you want to clone the Insiders repository, you need to become a
sponsor first to gain access.

  [Insiders]: insiders/index.md

=== "Material for MkDocs"

    ```
    git clone https://github.com/squidfunk/mkdocs-material
    cd mkdocs-material
    ```

=== "Insiders"

    You will need to have a GitHub access token [as described in the
    Insiders documentation] and make it available in the `$GH_TOKEN`
    variable.

    ``` sh
    git clone https://${GH_TOKEN}@github.com/squidfunk/mkdocs-material-insiders.git # (1)!
    ```

    1.  If you are using SSH keys for authenticating with GitHub, you can
        clone Insiders with this command:

        ```
        git clone git@github.com:squidfunk/mkdocs-material-insiders.git
        ```

    [as described in the Insiders documentation]: insiders/getting-started.md#requirements

Next, create a new [Python virtual environment][venv] and
[activate][venv-activate] it:

```
python -m venv venv
source venv/bin/activate
```

!!! note "Ensure pip always runs in a virtual environment"

    If you set the environment variable `PIP_REQUIRE_VIRTUALENV` to
    `true`, `pip` will refuse to install anything outside a virtual
    environment. Forgetting to activate a `venv` can be very annoying
    as it will install all sorts of things outside virtual
    environments over time, possibly leading to further errors. So,
    you may want to add this to your `.bashrc` or `.zshrc` and
    re-start your shell:

    ```
    export PIP_REQUIRE_VIRTUALENV=true
    ```

  [venv]: https://docs.python.org/3/library/venv.html
  [venv-activate]: https://docs.python.org/3/library/venv.html#how-venvs-work

Then, install all Python dependencies:

=== "Material for MkDocs"

    ```
    pip install -e ".[recommended]"
    pip install nodeenv
    ```

=== "Insiders"

    ```
    pip install -e ".[recommended, imaging]"
    pip install nodeenv
    ```

    In addition, you will need to install the `cairo` and `pngquant` libraries in your
    system, as described in the [image processing] requirements guide.

    [image processing]: plugins/requirements/image-processing.md


Finally, install the [Node.js] LTS version into the Python virtual environment
and install all Node.js dependencies:

```
nodeenv -p -n lts
npm install
```

  [Node.js]: https://nodejs.org

### Development mode

Start the watcher with:

```
npm start
```

Then, in a second terminal window, start the MkDocs live preview server with:

```
mkdocs serve --watch-theme
```

Point your browser to [localhost:8000][live preview] and you should see this
very documentation in front of you.

!!! warning "Automatically generated files"

    Never make any changes in the `material` directory, as the contents of this
    directory are automatically generated from the `src` directory and will be
    overwritten when the theme is built.

  [live preview]: http://localhost:8000

### Building the theme

When you're finished making your changes, you can build the theme by invoking:

``` sh
npm run build # (1)!
```

1.  While this command will build all theme files, it will skip the overrides
    used in Material for MkDocs' own documentation which are not distributed
    with the theme. If you forked the theme and want to build the overrides
    as well, e.g. before submitting a PR with changes, use:

    ```
    npm run build:all
    ```

    This will take longer, as now the icon search index, schema files, as
    well as additional style sheet and JavaScript files are built.

This triggers the production-level compilation and minification of all style
sheets and JavaScript files. After the command exits, the compiled files are
located in the `material` directory. When running `mkdocs build`, you should
now see your changes to the original theme.