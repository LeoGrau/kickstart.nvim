# Añadir plugins a esta configuración

Esta configuración está basada en **kickstart.nvim**, no en LazyVim. Los plugins se gestionan con `vim.pack` (el gestor integrado de Neovim), no con `lazy.nvim`.

## Instalar un plugin

1. En `init.lua`, añade el repositorio con `vim.pack.add` antes de llamar a `require(...).setup()` para configurarlo. Por ejemplo, para [nvim-ts-autotag](https://github.com/windwp/nvim-ts-autotag):

   ```lua
   vim.pack.add { gh 'windwp/nvim-ts-autotag' }

   require('nvim-ts-autotag').setup {
     opts = {
       enable_close = true,
       enable_rename = true,
       enable_close_on_slash = false,
     },
     per_filetype = {
       html = { enable_close = false },
     },
   }
   ```

2. Guarda `init.lua` y reinicia Neovim. La configuración de kickstart indica que `vim.pack` instala los plugins declarados al iniciar.

3. Para consultar el estado o buscar actualizaciones, usa:

   ```vim
   :lua vim.pack.update(nil, { offline = true })
   ```

   Para descargar actualizaciones:

   ```vim
   :lua vim.pack.update()
   ```

   Según la configuración de `vim.pack`, `:write` aplica las actualizaciones y `:quit` las cancela.

## Entender `module not found`

Un error como `module 'nvim-ts-autotag' not found` al ejecutar `require(...)` suele indicar que el plugin no está instalado o no está disponible en el `runtimepath`. Comprueba que el repositorio del plugin esté declarado en `vim.pack.add`, reinicia Neovim y revisa el estado de los plugins. Si no quieres usarlo, elimina tanto su declaración como su bloque `require(...).setup()`.

## ¿Cómo comprobar si uso LazyVim?

En esta configuración, las declaraciones `vim.pack.add { gh '...' }` son una señal de que se usa el gestor integrado, no LazyVim. El comando `:Lazy` pertenece a `lazy.nvim`; si no existe, no está disponible en esta sesión. No instales plugins siguiendo instrucciones de LazyVim a menos que migres deliberadamente la configuración.
