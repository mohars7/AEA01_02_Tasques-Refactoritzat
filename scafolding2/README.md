# Gestor de Tasques

Aplicació feta amb Vue 3 per gestionar tasques, refactoritzada en components.

## Funcionalitats

- Afegir tasques
- Marcar-les com a completades o desmarcar-les
- Eliminar-les (amb confirmació)
- Filtrar per mostrar només les pendents
- Comptador de total, pendents i completades
- Notificacions en afegir, completar o eliminar

## Estructura de components

```
App.vue
├── TaskForm.vue
└── TaskList.vue
    └── TaskItem.vue
```

| Component | Props | Events |
|-----------|-------|--------|
| App.vue | - | - |
| TaskForm.vue | - | `afegir` |
| TaskList.vue | `tasques` | `canviar-estat`, `eliminar` |
| TaskItem.vue | `tasca` | `canviar-estat`, `eliminar` |

`App.vue` guarda l'estat i passa les dades cap avall amb props. Els fills avisen el pare amb events (`emit`).

## Instal·lació i ús

```sh
npm install
npm run dev
```

Per generar la versió de producció:

```sh
npm run build
```