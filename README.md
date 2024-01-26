# Laravel template

## Un template pronto all'uso di Laravel.

### Passi da effettuare: 

1. Eseguire il comando `npm remove postcss` per rimuovere PostCSS
2. Eseguire il comando `npm i` per installare tutti i pacchetti di NPM (comprese le versioni aggiornate di `vite` e `laravel-vite-plugin`)
3. Eseguire il comando `npm i --save-dev sass` per installare SASS
4. Rinominare la cartella `css` che si trova nella cartella `resources/` in `scss`
5. Rinominare il file `app.css` che si trova nella nuova cartella `resources/scss` in `app.scss`
6. Modificare il file vite.config.js:
    - Cambiare la sezione `laravel(...)` in:
    ```
        laravel({
            input: [
                'resources/scss/app.scss',
                'resources/js/app.js'
            ],
            refresh: true
        })
    ```
    per includere i file `resources/scss/app.scss` e `resources/js/app.js` nella compilazione (`npm run dev`/`build`)
    - Aggiungere la sezione:
    ```
        resolve: {
            alias: {
                '~resources': '/resources/',
            }
        },
    ```
    dopo la sezione `plugins: [...]` per creare un alias della cartella `/resources/` (evitandoci di doverla richiamare in questo modo tutte le volte)
7. Aggiungere la riga import `'~resources/scss/app.scss';` nel file `resources/js/app.js` per importare tramite JS il file SCSS principale
8. Aggiungere la direttiva `@vite('resources/js/app.js')` nella sezione `<head>` del file `resources/views/welcome.blade.php` per includere gli asset nella view
9. Aggiungere le righe:
    ```
        import.meta.glob([
            '../img/**'
        ]);
    ```
    nel file `resources/js/app.js` per istruire Vite e Blade affinché processino correttamente i nostri asset
10. Aggiungere la riga `package-lock.json` nel file `.gitignore` che si trova nella `root` del progetto per evitare di pubblicarlo nella repo (è un file che viene generato ed aggiornato automaticamente dopo l'esecuzione del comando `npm i`)
11. Installare `Bootstrap`:
    1. Eseguire il comando `npm i --save bootstrap @popperjs/core` per installare sia la parte `CSS` che la parte `JS` di `Bootstrap`
    2. Aggiungere la riga `import path from path` nel file `vite.config.js`
    3. Aggiungere la riga `'~bootstrap': path.resolve(__dirname, 'node_modules/bootstrap')` nell'oggetto `resolve.alias` nel file `vite.config.js`
    4. Aggiungere la riga `@import "~bootstrap/scss/bootstrap";` in alto nel file `resources/scss/app.scss` per importare la parte `CSS` di Bootstrap
    5. Aggiungere la riga `import * as bootstrap from 'bootstrap';` nel file `resources/js/app.js` per importare la parte `JS` di Bootstrap.