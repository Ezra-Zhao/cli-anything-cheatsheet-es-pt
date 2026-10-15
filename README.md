# 🖥️ Guía rápida: CLI-Anything — convierte cualquier software en una CLI para agentes (ES · PT)

Una sola página para usar **CLI-Anything** (proyecto de HKUDS): instalar CLIs ya hechas desde CLI-Hub o generar la tuya para que un agente de IA pueda operar GIMP, Blender, LibreOffice y programas parecidos desde la terminal.

**Autor:** Guangyi Zhao · Octubre 2026

Proyecto original: https://github.com/HKUDS/CLI-Anything (53.010 estrellas, consultado el 15 de octubre de 2026) · CLI-Hub: https://hkuds.github.io/CLI-Anything/

> **Nota de autoría:** esta guía es una síntesis original, redactada por el autor a partir de la documentación pública del proyecto y de su propio uso. No es una traducción ni una copia de la documentación oficial, y no es un proyecto oficial de HKUDS. Para el detalle completo, ve al repositorio enlazado.

---

## 🇪🇸 Español

### La idea en 30 segundos

CLI-Anything genera, para un programa que ya existe, una interfaz de línea de comandos pensada para agentes: comandos con nombre claro, salida en JSON o en texto legible, modo interactivo (REPL) y un archivo `SKILL.md` para que el agente descubra solo cómo usarla. Hay dos caminos, y se pueden combinar:

| Camino | Para qué | Por dónde empiezas |
|---|---|---|
| Usar el ecosistema ya hecho | Instalar CLIs que la comunidad ya generó | `pip install cli-anything-hub` |
| Generar un CLI nuevo | Envolver un programa que todavía no tiene CLI | El plugin `/cli-anything` en tu agente (Claude Code, etc.) |

### Los 5 comandos que importan

| # | Comando | Qué hace |
|---|---|---|
| 1 | `pip install cli-anything-hub` | Instala **CLI-Hub**, el gestor de paquetes de CLIs |
| 2 | `cli-hub search <texto>` | Busca en el registro (ej.: `cli-hub search image`) |
| 3 | `cli-hub install <nombre>` | Instala un CLI del registro (ej.: `cli-hub install gimp`) |
| 4 | `cli-hub launch <nombre>` | Ejecuta un CLI ya instalado |
| 5 | `/cli-anything ./ruta-del-programa` | Genera un CLI completo para ese programa (7 fases: analizar, diseñar, implementar, planear pruebas, escribir pruebas, documentar, publicar) |

Para el comando 5 primero hay que instalar el plugin dentro del agente:

```bash
/plugin marketplace add HKUDS/CLI-Anything
/plugin install cli-anything
# y después, en la misma sesión:
/cli-anything ./gimp
```

Si la primera versión se queda corta, se amplía sin rehacerla: `/cli-anything:refine ./gimp "quiero más cobertura de filtros y procesamiento por lotes"`. Cada pasada de *refine* es incremental.

### CLI-Hub: buscar e instalar, la tabla completa

| Comando | Qué hace | Cuándo lo usas |
|---|---|---|
| `cli-hub list` | Muestra todo el registro | Para curiosear qué existe antes de buscar |
| `cli-hub search <texto>` | Busca por palabra clave | Cuando sabes la tarea, no el nombre |
| `cli-hub info <nombre>` | Detalle de un CLI | Antes de instalar: qué envuelve y qué pide |
| `cli-hub install <nombre>` | Instala desde el registro | El paso normal |
| `cli-hub update <nombre>` | Actualiza un CLI instalado | Cuando el registro publica mejoras |
| `cli-hub uninstall <nombre>` | Desinstala | Limpieza |
| `cli-hub launch <nombre> [args]` | Lanza el CLI con argumentos | Para probarlo al momento |

### Qué hay en el registro (ejemplos reales)

| Programa envuelto | Tipo de tareas que el agente puede hacer |
|---|---|
| GIMP / Krita / Inkscape | Imagen: filtros, lotes, exportar |
| Blender / FreeCAD / Godot | 3D y CAD: escenas, render, automatizar el editor |
| LibreOffice / Calibre / Joplin / Obsidian / Zotero | Oficina y conocimiento: convertir documentos, gestionar bibliotecas y notas |
| MuseScore / Kdenlive / Shotcut | Audio y vídeo: transponer, exportar, montar |
| n8n / QGIS | Automatización de flujos y mapas |

La lista crece por PRs de la comunidad; comprueba siempre con `cli-hub list`, no con esta tabla.

### ⚠️ Errores típicos

- **Olvidar el programa original.** El CLI *envuelve* el software real: si instalas el CLI de Blender sin tener Blender, no hay nada que operar. Instala primero la aplicación.
- **`Unknown skill: cli-anything`.** Casi siempre es que el plugin no cargó: `/reload-plugins`, comprueba con `/help cli-anything` y, si sigue, reinstala desde el marketplace. Cambiar a la forma antigua `/cli-anything:cli-anything` no arregla un plugin que no cargó.
- **En Windows con Claude Code:** los comandos se ejecutan vía `bash`; sin Git for Windows o WSL fallan con `cygpath: command not found`.
- **Dejar que el agente lea texto libre.** Cuando el CLI lo va a manejar un agente, pide salida JSON: es la mitad de la gracia del sistema.

---

## 🇵🇹 Português

### A ideia em 30 segundos

O CLI-Anything gera, para um programa que já existe, uma interface de linha de comando pensada para agentes: comandos com nome claro, saída em JSON ou em texto legível, modo interativo (REPL) e um arquivo `SKILL.md` para o agente descobrir sozinho como usar. Há dois caminhos, que podem ser combinados:

| Caminho | Para quê | Por onde começar |
|---|---|---|
| Usar o ecossistema pronto | Instalar CLIs que a comunidade já gerou | `pip install cli-anything-hub` |
| Gerar um CLI novo | Envolver um programa que ainda não tem CLI | O plugin `/cli-anything` no seu agente (Claude Code etc.) |

### Os 5 comandos que importam

| # | Comando | O que faz |
|---|---|---|
| 1 | `pip install cli-anything-hub` | Instala o **CLI-Hub**, o gerenciador de pacotes de CLIs |
| 2 | `cli-hub search <texto>` | Busca no registro (ex.: `cli-hub search image`) |
| 3 | `cli-hub install <nome>` | Instala um CLI do registro (ex.: `cli-hub install gimp`) |
| 4 | `cli-hub launch <nome>` | Executa um CLI já instalado |
| 5 | `/cli-anything ./caminho-do-programa` | Gera um CLI completo para esse programa (7 fases: analisar, projetar, implementar, planejar testes, escrever testes, documentar, publicar) |

Para o comando 5, primeiro instale o plugin dentro do agente:

```bash
/plugin marketplace add HKUDS/CLI-Anything
/plugin install cli-anything
# e depois, na mesma sessão:
/cli-anything ./gimp
```

Se a primeira versão ficar curta, amplie sem refazer: `/cli-anything:refine ./gimp "quero mais cobertura de filtros e processamento em lote"`. Cada passada de *refine* é incremental.

### CLI-Hub: buscar e instalar, a tabela completa

| Comando | O que faz | Quando usar |
|---|---|---|
| `cli-hub list` | Mostra todo o registro | Para ver o que existe antes de buscar |
| `cli-hub search <texto>` | Busca por palavra-chave | Quando você sabe a tarefa, não o nome |
| `cli-hub info <nome>` | Detalhe de um CLI | Antes de instalar: o que ele envolve e o que pede |
| `cli-hub install <nome>` | Instala a partir do registro | O passo normal |
| `cli-hub update <nome>` | Atualiza um CLI instalado | Quando o registro publica melhorias |
| `cli-hub uninstall <nome>` | Desinstala | Limpeza |
| `cli-hub launch <nome> [args]` | Roda o CLI com argumentos | Para testar na hora |

### O que há no registro (exemplos reais)

| Programa envolvido | Tipo de tarefas que o agente pode fazer |
|---|---|
| GIMP / Krita / Inkscape | Imagem: filtros, lotes, exportar |
| Blender / FreeCAD / Godot | 3D e CAD: cenas, render, automatizar o editor |
| LibreOffice / Calibre / Joplin / Obsidian / Zotero | Escritório e conhecimento: converter documentos, gerenciar bibliotecas e notas |
| MuseScore / Kdenlive / Shotcut | Áudio e vídeo: transpor, exportar, montar |
| n8n / QGIS | Automação de fluxos e mapas |

A lista cresce com PRs da comunidade; confira sempre com `cli-hub list`, não com esta tabela.

### ⚠️ Erros típicos

- **Esquecer o programa original.** O CLI *envolve* o software de verdade: se você instala o CLI do Blender sem ter o Blender, não há nada para operar. Instale o aplicativo primeiro.
- **`Unknown skill: cli-anything`.** Quase sempre é o plugin que não carregou: `/reload-plugins`, confira com `/help cli-anything` e, se persistir, reinstale pelo marketplace. Trocar para a forma antiga `/cli-anything:cli-anything` não conserta um plugin que não carregou.
- **No Windows com Claude Code:** os comandos rodam via `bash`; sem Git for Windows ou WSL eles falham com `cygpath: command not found`.
- **Deixar o agente ler texto livre.** Quando quem vai usar o CLI é um agente, peça saída JSON: é metade da graça do sistema.

---

## 🇬🇧 English summary

One-page cheat sheet (Spanish + Portuguese) for **CLI-Anything** (HKUDS): how to turn existing software (GIMP, Blender, LibreOffice…) into agent-native CLIs. Covers the two entry paths (install ready-made CLIs from CLI-Hub vs. generate your own with the `/cli-anything` plugin), the 5 core commands, the full `cli-hub` search/install table, real registry examples, and the typical mistakes (missing upstream app, plugin not loaded, Windows bash). Original synthesis by the author from the project's public documentation; not an official HKUDS document and not a translation.

**Author:** Guangyi Zhao · October 2026 · MIT License
