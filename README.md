# Tobías el Perrito Pro

Laboratorio interactivo de medicina veterinaria y zootecnia. Contiene teoría,
evaluaciones, glosario y modelos anatómicos de canino, felino, equino, bovino,
gallina, cocodrilo y tilapia. El progreso se guarda en el navegador de cada
persona.

## Estructura

- `tobias-private/site/`: aplicación web completa, imágenes y modelos.
- `tobias-private/*.php`: control de acceso por PIN y servidor de recursos.
- `public_html/`: entrada PHP y reglas de Apache para Hostinger.
- `scripts/empaquetar_hostinger.py`: genera un ZIP instalable con una clave de
  instalación aleatoria y distinta en cada ejecución.

## Actualizar el sitio de Hostinger que ya tiene PIN

Genera el paquete y actualiza solo `tobias-private/site/` en tu alojamiento.
Conserva `tobias-private/pin-config.php`, la carpeta `attempts/` y los archivos
PHP existentes. No vuelvas a ejecutar la instalación del PIN para actualizar
las lecciones o los modelos.

## Instalar en un alojamiento nuevo

Se necesita PHP 8.1 o posterior, Apache con `.htaccess` y HTTPS. Ejecuta
`python scripts/empaquetar_hostinger.py`, que crea el ZIP fuera del repositorio.
Descomprímelo en la carpeta que **contiene** `public_html`, con `tobias-private`
al mismo nivel y fuera de la raíz pública. Lee la clave generada en
`tobias-private/setup-token.txt` del servidor, abre `/setup.php` y establece
un PIN de 8 a 12 dígitos. Borra el ZIP del servidor después de extraerlo;
puedes borrar `public_html/setup.php` una vez configurado. Nunca dejes
archivos de `tobias-private/site/` dentro de `public_html`.

Una visita sin sesión a `/app.js` o `/assets/nuestra-historia.jpeg` debe
devolver `401`; la ruta `/` debe mostrar la pantalla de PIN. El sitio anterior
que siga publicado en otro dominio tiene su propia configuración de acceso.

## Seguridad y datos

No se suben a GitHub el PIN, el hash del PIN, la clave de instalación, los
intentos de acceso ni los datos de progreso personal. Los archivos de la web
incluyen imágenes y modelos usados por la plataforma; antes de compartir o
hacer público este repositorio revisa esos contenidos, incluida la fotografía
personal incluida en el sitio.

La autenticación por PIN protege el alojamiento PHP configurado: abrir el
HTML directamente o servir `tobias-private/site/` como web pública no aplica
esa protección. Para el servidor, configura los permisos de escritura en
`tobias-private/` y `tobias-private/attempts/` y comprueba el certificado SSL.
