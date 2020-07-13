## SSH
### Windows / Linux
- `ssh-keygen -t rsa -b 4096 -C "tu@email.com"` generar tu llave SSH.
        - `-t` type, elegimos el algorítmo que usaremos (rsa, dsa, ecdsa, ed25519...).
        - `-b` bits, número de bits que debe tener la clave.
        - `-C` comentario.
        
- `eval $(ssh-agent -s)` enciende el "servidor" de llaves SSH de tu ordenador.
- `ssh-add ruta-donde-guardaste-tu-llave-privada` añade tu llave SSH a este "servidor".

### Mac
- `eval "$(ssh-agent -s)"` para encender el "servidor" de llaves SSH de tu computadora.
- Si usas una versión de OSX superior a Mac Sierra (v10.12) debes crear o modificar un archivo "config" en la carpeta de tu usuario con el siguiente contenido (ten cuidado con las mayúsculas):
```
Host *
        AddKeysToAgent yes
        UseKeychain yes
        IdentityFile ruta-donde-guardaste-tu-llave-privada
```
- `ssh-add -K ruta-donde-guardaste-tu-llave-privada` para añadir tu llave SSH al "servidor" de llaves SSH de tu computadora (en caso de error puedes ejecutar este mismo comando pero sin el argumento -K)
