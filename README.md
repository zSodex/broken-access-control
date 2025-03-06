# Broken Access Control: Teoría y Ejemplos Prácticos

![image](https://github.com/user-attachments/assets/7a1a54af-ac43-4106-b894-e53b0d72acc3)



## ¿Qué es el Broken Access Control?

El **Broken Access Control** (Control de Acceso Roto) es una vulnerabilidad de seguridad común en aplicaciones web. Ocurre cuando los mecanismos de control de acceso no implementan correctamente las restricciones para que los usuarios accedan solo a los recursos o datos para los cuales tienen permisos. Esto puede permitir a los atacantes eludir estas restricciones y obtener acceso a datos sensibles o a funcionalidades que deberían estar restringidas.

### Tipos de Escalación de Privilegios

1. **Escalación de Privilegios Horizontal**: Un atacante puede acceder a los recursos de otros usuarios con el mismo nivel de privilegios.  
   **Ejemplo**: Un usuario podría acceder al perfil de otro usuario modificando el identificador de usuario en la URL, por ejemplo:  
   `http://example.com/profile.php?id=123` a `http://example.com/profile.php?id=124` para ver el perfil de otro usuario.

2. **Escalación de Privilegios Vertical**: Un atacante puede acceder a recursos o funcionalidades restringidas para un nivel de privilegio superior (por ejemplo, funciones administrativas).  
   **Ejemplo**: Un usuario común puede acceder a una página de administración (como `admin.php`) cambiando un parámetro en la URL, por ejemplo, de `admin=false` a `admin=true`.

3. **Referencias de Objetos Directos Inseguras (IDOR)**: Un atacante puede modificar identificadores de objetos (como URLs o parámetros de la base de datos) para acceder a recursos o datos a los que no tiene acceso.  
   **Ejemplo**: Un atacante puede cambiar el ID de un archivo en una URL como `http://example.com/file.php?id=456` a `http://example.com/file.php?id=457` para ver un archivo al que no debería tener acceso.

4. **Comprobaciones Insuficientes de Acceso**: Las aplicaciones no verifican adecuadamente los permisos de un usuario antes de permitirle acceder a ciertos recursos.  
   **Ejemplo**: Un usuario puede ver datos sensibles sin tener los permisos necesarios, como información de otros usuarios o configuraciones de la aplicación.

## Mecanismos de Control de Acceso

### 1. **Discretionary Access Control (DAC)**

El dueño del recurso determina quién puede acceder a un recurso y qué acciones pueden realizar.  
**Ejemplo**: Un archivo en un sistema operativo donde el propietario puede asignar permisos de lectura, escritura y ejecución a otros usuarios.

### 2. **Mandatory Access Control (MAC)**

Los accesos son controlados por reglas predefinidas y el sistema se asegura de que se cumplan.  
**Ejemplo**: Un sistema en un entorno gubernamental que asegura que solo usuarios con un permiso específico puedan acceder a información clasificada.

### 3. **Role-Based Access Control (RBAC)**

Los usuarios se asignan roles específicos que determinan su acceso a los recursos.  
**Ejemplo**: Un sistema de administración en el que los administradores tienen acceso completo, mientras que los empleados solo tienen acceso a datos limitados según su rol.

### 4. **Attribute-Based Access Control (ABAC)**

Acceso determinado por atributos como la ubicación, la hora, el dispositivo, o el rol.  
**Ejemplo**: Una aplicación en la que solo se permite el acceso a ciertos datos si el usuario está en una ubicación específica o usando un dispositivo autorizado.

## Ejemplos Prácticos de Broken Access Control

### Ejemplo 1: Escalación de Privilegios Horizontal

**Escenario**: Un sistema permite a los usuarios ver su propio perfil, pero un atacante puede cambiar el ID de usuario en la URL para ver el perfil de otro usuario.  
**URL vulnerable**:  
`http://example.com/profile.php?id=1001` (usuario A)  
`http://example.com/profile.php?id=1002` (usuario B)  
**Explotación**: El atacante cambia el ID en la URL de `1001` a `1002` y accede al perfil del usuario B, sin tener permisos para hacerlo.

### Ejemplo 2: Escalación de Privilegios Vertical

**Escenario**: Un usuario normal puede acceder a una página de administración cambiando un parámetro de la URL.  
**URL vulnerable**:  
`http://example.com/admin.php?admin=false` (usuario normal)  
**Explotación**: El atacante cambia el valor de `admin=false` a `admin=true` y obtiene acceso a funcionalidades administrativas.

### Ejemplo 3: Referencias de Objetos Directos Inseguras (IDOR)

**Escenario**: La aplicación utiliza identificadores predecibles en las URLs de recursos. Un atacante puede manipular el ID para acceder a objetos que no le pertenecen.  
**URL vulnerable**:  
`http://example.com/file.php?id=123` (archivo A)  
**Explotación**: El atacante cambia el ID de `123` a `124` y obtiene acceso a un archivo que no debería.

### Ejemplo 4: Comprobaciones Insuficientes de Acceso

**Escenario**: La aplicación permite a un usuario común acceder a información sensible de otros usuarios sin verificar los permisos correctamente.  
**Explotación**: Un usuario puede obtener información de otros usuarios simplemente accediendo a las URLs sin tener permisos para hacerlo.

## Prevención del Broken Access Control

1. **Validación adecuada de permisos**: Asegúrate de que los permisos sean verificados en el servidor y no solo en el lado del cliente.
2. **Uso de controles de acceso granulares**: Implementa controles más detallados para cada recurso, asegurando que solo los usuarios autorizados puedan acceder a ellos.
3. **Pruebas regulares de seguridad**: Realiza auditorías de seguridad y pruebas de penetración para identificar vulnerabilidades de acceso.
4. **Principio de menor privilegio**: Otorga a los usuarios solo los permisos necesarios para realizar su trabajo, reduciendo el riesgo de explotación.

## Conclusión

El **Broken Access Control** es una vulnerabilidad crítica que puede permitir a los atacantes acceder a datos y funcionalidades no autorizadas. Implementar un control de acceso adecuado es fundamental para proteger los recursos de una aplicación y evitar que los atacantes escalen privilegios o accedan a información sensible. 

Es importante realizar auditorías y pruebas de seguridad periódicas para detectar y corregir cualquier fallo en los mecanismos de acceso.

---

**¡Recuerda!** Mantén siempre una política de seguridad sólida y realiza pruebas regulares para identificar cualquier fallo en el control de acceso.
