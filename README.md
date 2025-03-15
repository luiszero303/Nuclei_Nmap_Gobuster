<h1>📝 Write-up de Pentesting: Escaneo y Análisis de Vulnerabilidades</h1>

<p>Este write-up cubre los pasos básicos para realizar un análisis de seguridad en un sistema objetivo utilizando herramientas como <code>Nmap</code>, <code>Gobuster</code> y <code>Nuclei</code>. Se detallan los comandos utilizados y sus explicaciones.</p>

<h2>📌 Paso 1: Escaneo de Puertos con <code>Nmap</code></h2>
<p>Ejecutamos el siguiente comando para encontrar todos los puertos abiertos en el objetivo:</p>
<pre><code>nmap -p- --open -sS --min-rate 5000 -vvv -n -Pn 192.168.1.34 -oG allports</code></pre>
<h3>🔍 Explicación del comando:</h3>
<ul>
    <li><code>-p-</code>: Escanea todos los puertos (1-65535).</li>
    <li><code>--open</code>: Muestra solo los puertos abiertos.</li>
    <li><code>-sS</code>: Realiza un escaneo SYN.</li>
    <li><code>--min-rate 5000</code>: Establece una velocidad mínima de paquetes para agilizar el escaneo.</li>
    <li><code>-vvv</code>: Muestra información detallada del escaneo.</li>
    <li><code>-n</code>: No resuelve nombres de dominio.</li>
    <li><code>-Pn</code>: Omite la detección de hosts vivos y escanea directamente.</li>
    <li><code>-oG allports</code>: Guarda los resultados en formato greppable.</li>
</ul>
<img src="https://github.com/tuusuario/tuRepositorio/nmap1.png" alt="Escaneo de puertos con Nmap" width="450" height="200">

<h2>📌 Paso 1.2: Reconocimiento de Servicios con <code>Nmap</code></h2>
<p>Realizamos un escaneo detallado en puertos específicos para obtener información sobre servicios y versiones:</p>
<pre><code>nmap -p22,80 192.168.1.34 -sCV -oN targeted</code></pre>
<h3>🔍 Explicación del comando:</h3>
<ul>
    <li><code>-p22,80</code>: Escanea los puertos 22 (SSH) y 80 (HTTP).</li>
    <li><code>-sCV</code>: Realiza detección de versiones y scripts comunes.</li>
    <li><code>-oN targeted</code>: Guarda la salida en formato normal.</li>
</ul>
<img src="https://github.com/tuusuario/tuRepositorio/nmap2.png" alt="Detección de servicios con Nmap" width="450" height="200">

<h2>📌 Paso 2: Descubrimiento de Directorios con <code>Gobuster</code></h2>
<p>Utilizamos Gobuster para enumerar directorios en el servidor web:</p>
<pre><code>gobuster dir -u http://192.168.1.34 -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -x php,html,txt</code></pre>
<h3>🔍 Explicación del comando:</h3>
<ul>
    <li><code>-u http://192.168.1.34</code>: Especifica la URL objetivo.</li>
    <li><code>-w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt</code>: Utiliza un diccionario de directorios comunes.</li>
    <li><code>-x php,html,txt</code>: Busca archivos con extensiones específicas.</li>
</ul>
<img src="https://github.com/tuusuario/tuRepositorio/gobuster.png" alt="Descubrimiento de directorios con Gobuster" width="450" height="200">

<h2>📌 Paso 3: Análisis de Vulnerabilidades con <code>Nuclei</code></h2>
<p>Ejecutamos Nuclei en el directorio principal del sitio web para detectar posibles vulnerabilidades:</p>
<pre><code>nuclei -u "http://192.168.1.34/buscar.php?busqueda=mangos" -t "http/"</code></pre>
<h3>🔍 Explicación del comando:</h3>
<ul>
    <li><code>-u "http://192.168.1.34/buscar.php?busqueda=mangos"</code>: Define la URL objetivo para el análisis.</li>
    <li><code>-t "http/"</code>: Utiliza templates HTTP de Nuclei para la detección de vulnerabilidades.</li>
</ul>
<img src="https://github.com/tuusuario/tuRepositorio/nuclei1.png" alt="Escaneo de vulnerabilidades con Nuclei" width="450" height="200">

<h2>📌 Paso 4: Análisis de Vulnerabilidades en Rutas Específicas</h2>
<p>Ejecutamos Nuclei en una ruta específica identificada con Gobuster:</p>
<pre><code>nuclei -u "http://192.168.1.34/fruits.php?busqueda=mangos" -t "http/"</code></pre>
<h3>🔍 Explicación del comando:</h3>
<ul>
    <li><code>-u "http://192.168.1.34/fruits.php?busqueda=mangos"</code>: Especifica una ruta concreta para el análisis.</li>
    <li><code>-t "http/"</code>: Aplica reglas de análisis HTTP.</li>
</ul>
<img src="https://github.com/tuusuario/tuRepositorio/nuclei2.png" alt="Escaneo de vulnerabilidades en rutas específicas con Nuclei" width="450" height="200">

<h2>🎯 Conclusión</h2>
<ul>
    <li>🔹 Usamos <code>Nmap</code> para identificar puertos abiertos y servicios activos.</li>
    <li>🔹 Descubrimos directorios ocultos con <code>Gobuster</code>, lo que nos permitió conocer posibles rutas de ataque.</li>
    <li>🔹 Analizamos vulnerabilidades con <code>Nuclei</code>, detectando problemas de seguridad en el sitio web.</li>
    <li>🔹 Refinamos nuestro análisis en rutas específicas para encontrar fallos explotables.</li>
</ul>
<p>Este proceso de reconocimiento y escaneo es esencial en una auditoría de seguridad, ayudándonos a identificar y mitigar vulnerabilidades antes de que sean explotadas. 🚀</p>
