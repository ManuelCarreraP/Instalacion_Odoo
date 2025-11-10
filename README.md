# Instalacion_Odoo

### 1º PASO
El primer paso seria entrar en nuestro IDE (PyCharm en mi caso) e instalar las extensiones necesarias:  

· **Docker**: Esta extensión es como un contenedor para tu código, empaqueta todo lo que tu aplicación necesita en un paquete ordenado.  
<br>
<img width="1455" height="744" alt="image" src="https://github.com/user-attachments/assets/40d04498-8ed6-4f4a-bd4b-7486a9ef94d0" />

· **YAML**: Esta extensión sirve para tener más facilidad a la hora de crear y escribir nuestros archivos .yml  
<br>
<img width="1455" height="744" alt="image" src="https://github.com/user-attachments/assets/2e49fb90-1ed4-4395-aad2-f2ab55dbb0f1" />

· **.env** (opcional): Esta extensión sirve para que en el caso de que no queramos guardar las variables en el documento yml, nos ayuda a gestionar los .env para guadrar los datos de forma más segura.  
<br>
<img width="1455" height="744" alt="image" src="https://github.com/user-attachments/assets/741047c7-ff6b-4db1-9b8b-89b94581f21c" />

----------

### 2º PASO
Una vez que ya tenemos nuestro IDE preparado para esto, comenzaremos creando un archivo llamado docker-compose.yml e introduciremos lo siguiente:
```bash
services:
  odoo:
    image: odoo:18.0
    container_name: odoo
    depends_on:
      - postgresql
    environment:
      - HOST=postgresql
      - USER=odoo
      - PASSWORD=odoo
      - DATABASE=odoo_db
    volumes:
      - ./odoo/addons:/mnt/extra-addons
      - ./odoo/config:/etc/odoo
      - ./odoo/data:/var/lib/odoo
      - ./odoo/logs:/var/log/odoo
    ports:
      - "8069:8069"
    networks:
      - odoo-network
    restart: unless-stopped

  postgresql:
    image: postgres:15
    container_name: postgresql-odoo
    environment:
      - POSTGRES_DB=odoo_db
      - POSTGRES_USER=odoo
      - POSTGRES_PASSWORD=odoo
      - PGDATA=/var/lib/postgresql/data/pgdata
    volumes:
      - ./postgresql/data:/var/lib/postgresql/data
    networks:
      - odoo-network
    restart: unless-stopped

  pgadmin:
    image: dpage/pgadmin4:latest
    container_name: pgadmin-odoo
    environment:
      - PGADMIN_DEFAULT_EMAIL=admin@odoo.com
      - PGADMIN_DEFAULT_PASSWORD=admin
    ports:
      - "8080:80"
    volumes:
      - ./pgadmin/storage:/var/lib/pgadmin
    networks:
      - odoo-network
    restart: unless-stopped
    depends_on:
      - postgresql

networks:
  odoo-network:
    driver: bridge
```
--------

### 3º PASO
Una vez tenemos el docker-compose-yml creado lo siguiente sería lanzar los contenedores, eso se hace con este comando:
```bash
docker compose up
```
Desde terminal:
<img width="1671" height="638" alt="image" src="https://github.com/user-attachments/assets/e6e55365-6936-4232-bd39-8f245d39afd1" />  
<br>
Desde docker desktop:
<img width="1915" height="637" alt="image" src="https://github.com/user-attachments/assets/417650c5-b9c6-45a5-9421-abe07b54a8c7" />
<br><br>

Ahora verificamos si nos entra tanto en **pgadmin** como en **odoo**:

· **odoo** (http://localhost:8069):  
Rellenamos los apartados con nuestros datos:  
IMPORTANTE: Marca la casilla "Load demonstration data"  
<img width="951" height="862" alt="image" src="https://github.com/user-attachments/assets/0cd0412d-a4b8-4240-a113-03006b518bc3" />  
<br>  
<img width="951" height="862" alt="image" src="https://github.com/user-attachments/assets/2dc89b49-acda-4761-9f57-5627a3cdfa03" />  
<br>  
Verificamos que estamos dentro de Odoo  
<img width="1920" height="1007" alt="image" src="https://github.com/user-attachments/assets/3a661cfe-403a-4adf-907c-7441d340a988" />
<br>
· **pgadmin** (http://localhost:8080):  
<img width="953" height="753" alt="image" src="https://github.com/user-attachments/assets/a72394a3-ee39-426d-bfad-00b5c8e62faa" />  

Una vez que entramos aquí pulsamos click derecho encima de Servers > Register > Servidor..., y aquí crearemos nuestra base d datos:  
<img width="953" height="753" alt="image" src="https://github.com/user-attachments/assets/196c1e59-e0c9-4d90-828c-2c2777eb7273" />  
<br>  
<img width="953" height="753" alt="image" src="https://github.com/user-attachments/assets/889a7328-6d8c-4dee-bc2c-cab67d4c2105" />  
<br>  
<img width="953" height="753" alt="image" src="https://github.com/user-attachments/assets/8121d34a-1093-498c-bc48-72af1d82aa33" />  
<br>    
<br>  
Una vez tenemos la bd creada se nos vera así:  
<img width="1920" height="1009" alt="image" src="https://github.com/user-attachments/assets/da0d0504-23a3-4b2d-b2ce-0e3df1965c4f" />

-------

### 4º PASO
A continuación instalaremos los siguientes modulos  
El primer paso es instalarlos, posteriormente desde el menú de arriba a la izquierda entraremos dentro de cada modulo:  
<br>
· **Ventas**:  
<img width="348" height="120" alt="image" src="https://github.com/user-attachments/assets/7f8636a6-72a9-43e3-b6e4-7283a40ca806" />  
<img width="1920" height="1007" alt="image" src="https://github.com/user-attachments/assets/5ce9d334-8c45-4e5b-87bd-d57e5f5e6756" />   
<img width="1920" height="1009" alt="image" src="https://github.com/user-attachments/assets/ceed2e0b-9571-4470-b084-261fccae88ee" />  

<br>  

· **Compras**:  
<img width="333" height="103" alt="image" src="https://github.com/user-attachments/assets/cd944b81-ae46-4c74-a7e8-2e6863d003ef" />  
<img width="1920" height="1009" alt="image" src="https://github.com/user-attachments/assets/93c42c95-c5a4-466b-abed-134afc544746" />  
<img width="1920" height="1009" alt="image" src="https://github.com/user-attachments/assets/d3dc4fff-fb26-46da-8570-80e854a5b8a2" />  

<br>  

· **Contactos**:  
<img width="348" height="147" alt="image" src="https://github.com/user-attachments/assets/2b12c69f-cf12-4836-a8c0-918c309943d7" />  
<img width="1920" height="1005" alt="image" src="https://github.com/user-attachments/assets/16548f50-1b0a-4fa6-81e7-22b2b5670cbb" />
<img width="1920" height="1009" alt="image" src="https://github.com/user-attachments/assets/2ee6c82b-ba9d-4410-9a8e-c7e4b2e48ac1" />






