# VPC Key-Protect VSI Encription

En esta guía encontrará como crear en IBM Cloud un  Virtual Server (VSI) en un Virtual Private Cloud (VPC) que utilice cifrado gestionado por el cliente para volúmenes de almacenamiento de bloques, este cifrado protege los datos en tránsito y en reposo. De igual manera, la instancia del servidor virtual se suministra con un volumen de arranque que de igual manera incluye este cifrado gestionado por el cliente, que para este caso es Key Protect.

### 1. Creación del servicio de Key Protect.

Para crear una instancia de Key Protecta través de la consola de IBM Cloud, siga los siguientes pasos:

  1. Inicie sesión en su cuenta de IBM Cloud.
  
  2. Escriba dentro del buscador de IBM Cloud _Key Protect_.
  3. Seleccione la región, añada el nombre del servicio y el grupo de recursos donde inició sesión.
  4. Política de red permitida: El acceso a la red pública y privada es la configuración predeterminada y se usa si no se establece una política. Y la opción de solo acceso a la red privada de la instancia de Key Protect  cepta solicitudes de API solo de puntos finales privados, no de red externa a IBM.
  
  ![1](https://user-images.githubusercontent.com/60628267/93503526-d13b3280-f8dd-11ea-92ec-3c8fa9ddaf7a.gif)
  
### 2. Creación de clave en IBM Key Protect.

Mediante los siguientes pasos podrá crear una clave raíz en la consola de IBM Cloud ya con el Key Protect provisto.

  1. En el menú desplegable de la izquierda, seleccione > Lista de recursos.
  2. Dentro de la lista de recursos de IBM Cloud, seleccione su instancia creada de Key Protect.
  3. Seleccione_Manage keys_ y haga clic en _Agregar clave_.
  
  ![2](https://user-images.githubusercontent.com/60628267/93505463-84a52680-f8e0-11ea-967a-2fa603f960e4.gif)


### 3. Cree acceso desde el servicio origen y Key Protect.

A través de IBM Cloud Identity and Access Management (IAM), autorice el acceso entre Cloud Block Storage (servicio de origen) y Key Protect (servicio de destino).
El acceso al servicio origen -> destino va a tener rol de lector.

![3](https://user-images.githubusercontent.com/60628267/93506247-a0f59300-f8e1-11ea-9a89-0ddf312d4347.gif)

### 4. Suministro del servidor virtual con volúmenes que utilizan cifrado gestionado por el cliente (Key Protect).

Al momento de crear una instancia de servidor virtual, se debe especificar el cifrado gestionado por el cliente para el volumen de arranque y para cualquier volumen de datos que se desee añadir, esto es importante realizarlo en este momento, pues son datos a los que no se podrá tener acceso una vez creada la instancia. El cifrado gestionado por el cliente - Key Protect, protege los datos en tránsito y en reposo.

  1. En la consola de IBM Cloud, dentro del menú > Infraestructura de VPC > Cálculo > Instancias de servidor virtual. Pulse en Nueva instancia y complete los campos.
  
  ![5](https://user-images.githubusercontent.com/60628267/93508790-73f6af80-f8e4-11ea-9ce8-052960cdb69a.gif)

   2. Cree un nuevo volúmen de datos para el cual proporcione el nombre, tamaño, cifrado, nombre de la instancia de cifrado y el nombre de la clave; estos últimos campos son los pertenecientes al Key Protect. Esto tambien debe tenerlo en cuenta para el volúmen de arranque.
   
   ![6](https://user-images.githubusercontent.com/60628267/93511409-64796580-f8e8-11ea-8dd1-7c48832beed0.gif)

    


