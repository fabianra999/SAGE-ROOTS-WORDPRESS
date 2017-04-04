# SAGE-ROOTS-WORDPRESS
INSTALAR Y CONFIGURAR SAGE (ROOTS)

<b>características:</b> <br>
Bower Gulp BrowerSync, HTML5 Boilerplate, Mobile-first, responsive, DRY, ARIA Roles, Microformatos, Preparado para Multilenguaje, Bootstrap, Herencia de plantillas.<br>

<b>Requisitos previos.</b> <br>
NoodeJS, Git y PHP, entorno de trabajo como Xampp o Lemp con un WordPress instalado y en funcionamiento.<br>

<b>Clonando el tema desde su repositorio Git</b> <br>
<code>git clone https://github.com/roots/sage.git NOMBRE_DEL_TEMA</code>
Sustituimos NOMBRE_DEL_TEMA por el nombre que queramos darle a nuestro tema, automaticamente se descargarán todos los archivos necesarios para el tema Sage.
Descargaar el tema en (wp-content/themes). <br>
Podemos comprobar que el tema está instalado desde el panel de administración en Apariencia > Temas e instalar “Sage Starter Theme”, el tema de nuestro WordPress cambiará aunque todavia no mostrará un aspecto muy agradable.  <br>

<b>Jerarquía de archivos y carpetas</b> <br>
En la carpeta templates del tema podemos encontrar los archivos principales del tema, como el head.php, footer.php, content.php, content-single.php y los demás archivos que utilizamos habitualmente al crear temas personalizados. <br>
En la carpeta raiz del tema encontramos el archivo 404.php, functions.php, search.php y uno de los más importantes, el archivo base.php <br>
El archivo base.php tiene como objetivo el principio DRY, de forma que nos ahorramos tener que estar escribiendo código repetitivo en todos los archivos del tema, que por otra parte, tampoco tendremos que revisar uno por uno cuando necesitemos hacer cambios, se carga de modo automático en todas la páginas del tema. <br>
La carpeta assets contiene los archivos css, js, fuentes e imágenes para ser compilados en la carpeta dist.<br>
Para dar por terminado el desarrollo del tema y lanzar el proyecto a producción, ejecutamos en la terminal: <br>
<code>gulp –production</code>

1. Nombre del tema <br>
El nombre y los datos del tema podemos modificarlos en el archivo style.css que se encuentra en el directorio raiz del tema.

2. Instalar dependencias <br>
A continuación utilizaremos npm para instalar las dependencias necesarias para el tema, desde la terminal dentro de la carpeta del tema ejecutaremos npm install, se creará la carpeta node_modules.
<code>npm i</code>

3. bower install <br>
A continuación ejecutamos bower install, se creará la carpeta bower_components.
<code>bower install</code>

4. Crear carpeta dist <br>
Por ultimo ejecutamos gulp, se creará la carpeta dist.
<code>gulp</code>

5. manifest.json <br>
A continuación vamos a la carpeta assets y buscamos el archivo manifest.json, buscamos en la linea 25 devUrl en la que el valor es example.dev, cambiamos ese valor por la ruta del proyecto en el que estamos trabajando.
<code>
},
			"config": {
		    	"devUrl": "http://localhost/proyectos/sagetest/"
			}
		}	
</code>

6. gulp watch <br>
Volvemos a la terminal y ejecutamos gulp watch, al hacer cualquier cambio en el css, se abrirá la ventana del navegador automaticamente, si no es así, podemos escribir la ruta directamente en el navegador escribiendo localhost:3000/nombre_ruta/.<br>
Como mencioné anteriormente, Sage utiliza SASS para agilizar el proceso de maquetación

7. Instalar packages con Bower <br>
Abrimos la terminal como siempre dentro de la carpeta del tema o desplazandonos hasta ella con la terminal y ejecutamos:<br>
<code>bower install –save fontawesome</code> <br>
A continuación volvemos a hacer gulp y comprobamos que se ha instalado correctamente en la carpeta bower_components. <br>
Algunas versiones no muestran las fuentes correctamente, si experimentais problemas podeis mover las fuentes directamente a la carpeta fonts.

8. Eliminar CSS, JS y otros componentes <br>
<b>css - sass</b> <br>
Por defecto, Sage tiene pre-instalado Bootstrap, no en vano, es el framework más utilizado actualmente, pero puede que no necesitemos todos los componentes que trae consigo, asi que lo mejor es eliminar todo aquello que no vayamos a utilizar y crea un peso innecesario al cargar nuestro sitio. <br>
Para probar que todo funciona correctamente, podemos insertar código como una barra de progreso para comprobar posteriormente que se han eliminado los estilos: <br>
Abrimos el archivo _bootstrap.scss que se encuentra en : bower_components > bootstrap-sass > assets > stylesheets, las rutas pueden variar según la versión de Sage, a continuación eliminamos la línea siguiente: <br>
<code>@import “bootstrap/progress-bars”;</code> <br>
Volvemos a la terminal y ejecutamos gulp styles, comprobaremos que los estilos han desaparecido <br>
<code>gulp styles</code> <br>
<b>js</b> <br>
Para eliminar componentes JS lo hacemos desde el archivo bower.json que está en la raiz del tema, eliminamos aquellos que no vayamos a utilizar y ejecutamos gulp scripts. <br>
<code>gulp scripts</code>

9. Configurar wp-config <br>
En este archivo enlasamos la base de datos. <br>
configuramos el tema <b>Sage</b> poniendo al final del archivo. <br>
<code> //config tema sage </code><br>
<code>define('WP_ENV', 'development');</code>

<br><br><br>
<b>Crear tpl</b> <br>
1. crea Tpl <br>
crear archivo .php y al inicio referenciarlo <code>?pph /* Template Name: Home */ ?</code> <br>

2. importar section a tpl <br>
si el tpl se compone de varias secciones se pueden llamas de esta forma.<br>
<code>?php get_template_part('home/nosotros'); ? </code><br>
<code>?php get_template_part('home/temas'); ?</code> <br>
<br><br>

<b>Magic field</b><br>
Magic field es un plugin de worpress que ayuda a generar contenidos y campos personalisados. <br>

1. Para llamar post types de magic field el markup <br>
<code>?php query_posts('post_type=beneficios'); </code><br>
<code> while (have_posts()) : the_post(); ?</code><br>
<code><!- mi markup -> </code><br>
<code><!- campo magic field -> </code><br>
<code>?php endwhile; ?</code><br>

2. Traer campo de magic field dentro de post types <br>
<code>?php echo get('quienes_somos_contenido'); ?</code>

3. traer  grupo duplicable con magic field: donde ('listado_beneficios_beneficio'); es el nombre del grupo<br>
<code>
   <!-- Listar los beneficios: repeat --> <br>
                |-?php <br>
                $beneficios = get_field('listado_beneficios_beneficio'); <br>
                foreach($beneficios as $key => $beneficio) : <br>
                $claseB = ($key % 2 == 0) ? 'odd' : 'even'; <br>
                ?-| <br>

                |-div class="col-xs-12 col-sm-5 col-sm-offset-1 alingTop col-centered |-?php echo $claseB; ?-| "-| <br>
                |-p-| |-?php echo $beneficio; ?-| |-/p-| <br>
                |-/div-| <br>
                |-?php endforeach; ?-| <br>
</code>
3. traer campo de un grupo donde get_group('quieres_footer') es el nombre del grupo y 'quieres_footer_btn_url' es el campo.<br>
<code>
  |-div class="content content_btn_footer"-| <br>
                |-?php <br>
                $elements = get_group('quieres_footer'); <br>
                foreach($elements as $key => $element){  <br>
                print "|-a href=".$element['quieres_footer_btn_url'][1].">". $element['quieres_footer_btn_titulo'][1] ."|-/a-|"; <br>
                } <br>
                ?-|
                |-/div-|
</code>



<b>ver</b>
 <a href="https://www.advancedcustomfields.com/resources/"> documentacion advancedcustomfields</a>
