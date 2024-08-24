# Utilizando la clase NpgsqlError de la enumeración NpgsqlException.Errors
        
<p align="justify">
Una forma precisa de diagnosticar los errores <a href="http://www.postgresql.org/">PostgreSQL</a> en una aplicación :NET es mediante el uso de la clase NpgsqlError de la cual se pueden obtener detalles adicionales a la excepción generada esta  clase esta incluida en la enumeración Errors la cual al recorrerse y consultar las propiedades de la clase NpgsqlError podemos obtener información específica acerca de los errores y advertencias que se generan al ejecutar los comandos SQL o Store procedures en PostgreSQL por medio de una aplicación .NET que haga uso del driver <a href="http://npgsql.projects.postgresql.org/">Npgsql</a>.
</p>
<p align="justify">
A continuación mostramos una aplicación de consola que se conecta a una base de datos PostgreSQL, ejecuta un comando SQL para crear un nuevo registro en una tabla y envia la excepción generada hacia un archivo de texto.
</p>
<br /><p>Aquí el código para crear la tabla <b>Books</b></p>
            <!--Code -->
<div>
<IMG src="picture_library/npgsqlerrors/201210_books.png" border="0">
</div>

<p align="justify">
            En la clase <em>BooksManager</em>  se encuentra el método estático <em>LogErrors</em> en donde se realiza toda la funcionalidad, aquí es donde se itera por la enumeración Errors de la clase NpgsqlException y se escribe la información en el archivo de texto.<br /></p>
            <div>
<a href="http://clkmein.com/qOU1Px" target="_blank">
<IMG src="picture_library/npgsqlerrors/2012Logerrors.png" border="0">
</a>
</div><br />
<p align="justify">
Antes de compilar y ejecutar la aplicación vamos a ocasionar un error en la sentencia de la consulta SQL. Por ejemplo no escribir correctamente el nombre de la tabla.</p><br />
<pre>
var commandText = "INSERT INTO Books(title,numpages,pubyear,created)
VALUES(:title, :numpages, :pubyear, :created)";<br />
</pre>
            <!--Code-->
            <p align="justify">Al compilar y ejecutar la aplicación veremos la excepción generada a propósito para poder consultar el archivo log y ver más detalles acerca de la excepción generada.<br />Compilamos la aplicación con los siguientes comandos: </p>
            <!--Code-->
            <pre>
            <tt>$ dmcs -t:library -r:System.Data,Npgsql Book.cs BooksManager.cs Logger.cs <br />/out:TestNpgsqlError.dll</tt><br /><tt>$ dmcs -r:TestNpgsqlError.dll Main.cs</tt><br />
            </pre>
            <!--Code-->
            <div>
<IMG src="picture_library/npgsqlerrors/img1.png" border="0">
</div>
            <p>Ejecutamos la aplicación, como se muestra en la siguiente imagen: </p>
            <div>
<IMG src="picture_library/npgsqlerrors/img2.png" border="0">
</div>
<p align="justify">
Otra prueba es si escribimos erróneamente los parámetros de la cadena de conexión, por ejemplo cambiar el usuario de la base de datos o no teclear correctamente el nombre de la base de datos.</p>
<br />
<pre>
string connStr = "Server=127.0.0.1;Port=5432;Database=testBooks;User ID=postgressss;Password=Pa$$W0rd";
</pre>
<p align="justify">Podemos consultar la bitácora y ver como por cada excepción se genera un código y los detalles de la excepción.
</p>
<div>
<IMG src="picture_library/npgsqlerrors/img3.png" border="0">
</div>
