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
_config.yml               Configuración: nombre, correo, métricas y hero_portrait
_data/
  es.yml / en.yml         Todos los textos de interfaz, en cada idioma
  people.yml              Equipo activo. group: lead | postdoc | phd | undergrad
  alumni.yml              Ex integrantes, para la tabla al final de Equipo
  news.yml                Noticias del carrusel; el texto sale de plantillas
  research.yml            Líneas de investigación
  projects.yml            Proyectos: título oficial, abstract, periodo, contacto
  publications.yml        Artículos indexados
  funding.yml             Logos de la franja de financiamiento
_layouts/                 Plantillas de página (home, research, team, …)
_includes/
  nav.html footer.html    Cabecera y pie
  head.html icons.html    Metadatos e íconos SVG
  person-card.html        Ficha ancha: dirección y postdocs
  person-mini.html        Tarjeta compacta: estudiantes
  news-slide.html         Una diapositiva del carrusel de noticias
  pub-item.html           Una publicación
index.html, equipo.html…  Páginas en español
en/                       Las mismas páginas en inglés
assets/css/style.css      Hoja de estilo única
assets/img/               Logos, fotos del equipo y favicon YA optimizados
```

## 2. Cómo editar el contenido

Casi nada se edita en HTML. Lo habitual:

| Quiero… | Archivo |
|---|---|
| agregar a la dirección o a un postdoc | `_data/people.yml` con `group: lead` o `postdoc` — ficha ancha, usa `bio`, `degree`, `interests` y `metrics` |
| agregar a un estudiante | `_data/people.yml` con `group: phd` o `undergrad` — tarjeta compacta, usa `program` y `focus` (una línea) |
| mover a alguien a ex integrantes | quítalo de `people.yml` y agrégalo a `_data/alumni.yml` |
| agregar una noticia | `_data/news.yml`. El texto no se escribe: se elige una plantilla de `news.templates` en `es.yml`/`en.yml` con el campo `template:`. Usa un índice distinto al de la noticia anterior del mismo tipo |
| cambiar el tono de las noticias | las plantillas en `_data/es.yml` y `_data/en.yml`, no las entradas |
| agregar un paper | `_data/publications.yml`, bloque `indexed` (y su apellido en `group_authors`) |
| agregar o editar un proyecto | `_data/projects.yml` — el `title` va tal cual la postulación, sin traducir |
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

- Abstract oficial del Fondecyt Regular de César: el que está publicado lo redactamos
  a partir de su propuesta, porque el PDF no trae sección de abstract. También falta
  confirmar su periodo (hoy dice 2026–2029).
- Datos y foto de Judith Quezada; correos y fotos del resto de estudiantes.
- Columna `now:` de `alumni.yml` (dónde está hoy cada ex integrante) y sus LinkedIn.
- Título de la memoria de Margarita Toro, y confirmar las fechas aproximadas de tres
  noticias (ver `../informacion/noticias/LEEME.md`).
- Procesar el material nuevo de `../informacion/perfiles/estudiantes/`: memorias de
  Mariano Guajardo y María José Núñez, que aún no están en el sitio.
- Una foto de portada del laboratorio o de los reactores.
- Correo institucional del grupo (hoy figura el Gmail `labgtechaguas@gmail.com`).
- Confirmar si César dirige el Doctorado en Ciencias de la Ingeniería (dato sin
  verificar, retirado del sitio).
- Dirección y oficina exactas para la página de contacto.
- Completar el histórico de publicaciones (hay 5 de partida; César tiene 89 productos).
- Confirmar el año de fundación del grupo (`lab.founded` en `_config.yml`, hoy 2022).
- Confirmar el nombre en inglés del grupo (hoy *Water Technologies Group*).
