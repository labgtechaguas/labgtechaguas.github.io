# Sitio web — G-Tech · Grupo de Tecnologías del Agua

Sitio del grupo construido con **Jekyll** y publicado con **GitHub Pages**.
Bilingüe español / inglés, sin base de datos: todo el contenido vive en archivos
YAML dentro de `_data/`.

- **En línea:** <https://labgtechaguas.github.io>
- **Repositorio:** `labgtechaguas/labgtechaguas.github.io`
- **Administrador:** Felipe A. Carreño López
- **Material fuente:** `../informacion/` (fuera del repo — ver su `LEEME.md`)

---

## 1. Dónde está cada cosa

```
pagina_web_gtech/
├── informacion/     Material de trabajo: PDF de proyectos, fotos originales,
│                    INFORMACION-GRUPO.md. NO se versiona ni se publica.
└── github/          ← estás aquí. Es el repositorio git. Todo lo que hay
                     dentro se publica en labgtechaguas.github.io.
```

La separación es deliberada: `informacion/` está un nivel **por encima** del
repositorio, así que ningún `git add` puede alcanzarla. Nada sensible puede
terminar en un commit por descuido.

```
_config.yml               Configuración: nombre, correo, métricas, hero_portrait
_data/
  es.yml / en.yml         Textos de interfaz y plantillas de noticias
  people.yml              Equipo activo. group: lead | postdoc | staff | phd | undergrad
  alumni.yml              Ex integrantes, para la tabla al final de Equipo
  news.yml                Noticias del carrusel; el texto sale de plantillas
  collage.yml             Las tres fotos del collage de "Quiénes somos"
  research.yml            Líneas de investigación
  projects.yml            Proyectos propios: título oficial, periodo, contacto
  collaborations.yml      Proyectos de otros equipos en los que participamos
  publications.yml        Artículos indexados desde 2023
  funding.yml             Logos de la franja: UANDES, ANID, CORFO
_layouts/                 Plantillas de página (home, research, team, news, …)
_includes/
  nav.html footer.html    Cabecera y pie; el pie trae el script del carrusel
  head.html icons.html    Metadatos e íconos SVG
  person-card.html        Ficha ancha: dirección y postdocs
  person-mini.html        Tarjeta compacta: staff y estudiantes
  news-carousel.html      El carrusel; se usa en la portada y en Noticias
  news-slide.html         Una diapositiva del carrusel
  pub-item.html           Una publicación
index.html, equipo.html…  Páginas en español
en/                       Las mismas páginas en inglés
assets/css/style.css      Hoja de estilo única
assets/img/
  logos/ people/          Logos y fotos del equipo, ya optimizados
  news/ collage/          Recortes de las noticias y del collage
```

## 2. Cómo editar el contenido

Casi nada se edita en HTML. Lo habitual:

| Quiero… | Archivo |
|---|---|
| agregar a la dirección o a un postdoc | `_data/people.yml` con `group: lead` o `postdoc` — ficha ancha, usa `bio`, `degree`, `interests` y `metrics` |
| agregar personal técnico o de gestión | `_data/people.yml` con `group: staff` — tarjeta compacta con `role` solamente; `program` y `focus` se dejan vacíos |
| agregar una colaboración | `_data/collaborations.yml` — proyectos de otros grupos en los que participamos, se muestran al final de Proyectos |
| agregar a un estudiante | `_data/people.yml` con `group: phd` o `undergrad` — tarjeta compacta, usa `program` y `focus` (una línea) |
| mover a alguien a ex integrantes | quítalo de `people.yml` y agrégalo a `_data/alumni.yml` |
| agregar una noticia | `_data/news.yml`. El texto no se escribe: se elige una plantilla de `news.templates` en `es.yml`/`en.yml` con el campo `template:`. Usa un índice distinto al de la noticia anterior del mismo tipo |
| cambiar el tono de las noticias | las plantillas en `_data/es.yml` y `_data/en.yml`, no las entradas |
| agregar un paper | `_data/publications.yml`, bloque `indexed` (y su apellido en `group_authors`). **Solo de 2023 en adelante**: es el año en que se formó el grupo |
| agregar o editar un proyecto | `_data/projects.yml` — el `title` va tal cual la postulación, sin traducir. Hoy **ningún** proyecto publica resumen: `abstract:` va vacío y la ficha muestra solo el título y los datos |
| cambiar una línea de investigación | `_data/research.yml` |
| cambiar un texto de la interfaz | `_data/es.yml` y su equivalente en `_data/en.yml` |
| cambiar correo, dirección o cifras de portada | `_config.yml` |
| cambiar el retrato de la portada | `hero_portrait` en `_config.yml`: el `id` de una persona de `people.yml`, o `""` para quitarlo |
| agregar una foto | copia la versión optimizada a `assets/img/people/` y pon el nombre del archivo en el campo `photo:` de la persona (el original se queda en `../informacion/perfiles/`) |

Cada entrada bilingüe tiene la forma:

```yaml
title:
  es: "Texto en español"
  en: "Text in English"
```

Si dejas `photo: ""`, la tarjeta muestra las iniciales en vez de una foto.
Los apellidos listados en `group_authors` (en `publications.yml`) se resaltan
automáticamente en negrita en la lista de publicaciones.

Antes de editar aquí, actualiza los documentos maestros de `../informacion/`:
`INFORMACION-GRUPO.md` para el grupo, los proyectos y los perfiles, y
`perfiles/estudiantes.md` para estudiantes y alumni. Eso evita que el sitio y el
material fuente se desincronicen.

## 3. Ver los cambios antes de publicarlos

```bash
cd ~/Library/CloudStorage/Dropbox/pagina_web_gtech/github
bundle install          # solo la primera vez
bundle exec jekyll serve
```

Y abre <http://127.0.0.1:4000>. Con `--livereload` se recarga al guardar.

## 4. Publicar

```bash
cd ~/Library/CloudStorage/Dropbox/pagina_web_gtech/github

git pull
git add -A
git commit -m "Agrego tesista al equipo"
git push
```

GitHub Pages recompila solo, en un par de minutos.

## 5. Cuentas y credenciales

Este repositorio está deliberadamente aislado del sitio personal
(`../../pagina_web`):

| | Sitio del grupo | Sitio personal |
|---|---|---|
| Autor de los commits | `G-Tech Aguas <labgtechaguas@gmail.com>` | `Felipe Carreño <facarreno@miuandes.cl>` |
| Cuenta de GitHub | `labgtechaguas` | `facarreno` |
| Alias SSH | `github-gtech` | `github-personal` |
| Llave | `~/.ssh/id_gtech` | `~/.ssh/id_facarreno` |

La identidad está fijada con `git config --local` en cada repo, así que ninguno
depende de la configuración global de git. Los alias SSH están definidos en
`~/.ssh/config` y cada uno usa su propia llave, así que el `push` siempre entra
con la cuenta correcta.

Comprobar en cualquier momento:

```bash
git config --local user.email && git remote -v
```

## 6. Notas de operación

**Dropbox + git.** Esta carpeta vive dentro de Dropbox. Para que Dropbox no
toque el historial de git:

```bash
xattr -w com.dropbox.ignored 1 .git
```

Repítelo en cada máquina donde clones el repo. Regla práctica: **una máquina a
la vez**, y `commit` + `push` antes de cambiar de equipo.

## 7. Pendientes

- Una foto de grupo o de laboratorio para la portada y el collage: las tres actuales
  son de congresos y ninguna muestra el trabajo experimental.
- Datos y foto de Judith Quezada; correos y fotos del resto de estudiantes.
- Confirmar si el CORFO 24CVCS-255807 sigue vigente: su periodo termina en 2025.
- Título de la memoria de Margarita Toro, y confirmar las fechas aproximadas de tres
  noticias (ver `../informacion/noticias/LEEME.md`).
- LinkedIn de Santiago Vila y de los estudiantes que aún no lo tienen.
- Definir el rol de Álvaro Samaniego Soto, si va en el equipo.
- Número de oficina, si corresponde sumarlo a la dirección de contacto.

> El correo `labgtechaguas@gmail.com` que aparece en la tabla de identidades de git es el
> de la **cuenta de GitHub**, no el del grupo. El correo institucional del sitio es
> `labgtechaguas@uandes.cl` y vive en `_config.yml`.
