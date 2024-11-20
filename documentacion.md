# 1.4 - Entrega 3: Caso práctico 3
#### Resumen de la tarea:

En esta entrega nos vamos a centrar en restaurar una imagen de nuestro repositorio sobre varios equipos nuevos.

El objetivo es restaurar la imagen de la anterior práctica sobre dos máquinas al mismo tiempo VMR1 y VMR2. Recuerda que ha de tener mayor capacidad que el disco de la VM sobre la que se hizo la imagen.

✨✨Recuerda revisar la rúbrica para saber cómo se va a evaluar.✨✨

👌Recuerda marcar la tarea como entregada cuando hayas subido el vídeo (siempre antes de la hora límite).👌

😡Pasada la fecha de entrega se considerará "Tarea no entregada"😡

---

## Objetivo de la práctica
#### Explicar el objetivo de la práctica y presentar un diagrama que complete la explicación

En esta prácitca como se encuentra citado arriba vamos a **restaurar la imagen de la anterior práctica** sobre dos máquinas al mismo tiempo VMR1 y VMR2.

En primer lugar he creado la **máquina VMS1** que actua como **servidor** para propagar la imagen vía DHCP. En esta máquina adjuntaremos los siguientes discos:
1. Disco de VMS1 (45GB)
2. Disco de VMS2 (45GB)
3. Repositorio (23GB)
4. ISO de Clonezilla Lite
5. ISO de DRBL

En primer lugar iniciamos la máquina con la **ISO de DRBL para entrar a GPARTED y crear tanto la tabla de particiones (GPT) como el sistema de archivos (NTFS)** de los discos de VMR1 y VMR2. Una vez están preparados los discos los eliminamos del servidor y dejamos simplemente esto:
1. Repositorio (23GB)
2. ISO de Clonezilla Lite

Ahora iniciamos de nuevo el servidor y comenzamos a realizar las configuraciones pertinentes que se mostrarán durante esta documentación, en las **máquinas clientes** hay que cambiar el orden de arranque y dejar simplemente vía **red**. 

Una vez todo restaurado con éxito podemos apagar el servidor e iniciar las máquinas con sus discos.

## Diagrama
![alt text](f591dd97-8e71-4aa2-8150-5995d0104c0b-1.png)

---

## PREPARACIÓN DE VMS1, VMR1 Y VMR2

### VMS1 _(Red)_
![alt text](image.png)
### VMS1 _(Almacenamiento)_
![alt text](image-1.png)

---
### VMR1 _(Red)_
![alt text](image-3.png)
### VMR1 _(Almacenamiento)_
![alt text](image-2.png)

---
### VMR2 _(Red)_
![alt text](image-4.png)
### VMR2 _(Almacenamiento)_
>VirtualBox:
![alt text](image-5.png)

>Gparted:
![alt text](image-6.png)

#### Inicio del proceso de configuración en el servidor:

>Iniciamos Clonezilla en el servidor (VMS1)

![alt text]({B129B443-C8A6-46DF-9335-27423BB84F87}.png)

>En este paso debemos elegir que tipo de servicio queremos usar, en este caso iniciaremos Clonezilla Lite Server

![alt text]({B8BE7659-A406-4C7C-833D-22CFAFFB239B}.png)

>Elegimos el **modo DHCP** para propagar a las máquinas que se encuentren en estado PXE.

![alt text]({AE6758C8-F878-4ED8-A5B5-105CF7C06AB6}.png)

>¿Dónde se almacena el repositorio? En este caso en local ya que se encuentra adjuntado como disco a la máquina virtual.

![alt text]({F9561E34-E186-4047-87F0-6818FF000DC2}.png)

>Chequeo previo de la imagen para evitar errores que no nos permitan seguir con la restauración.

![alt text]({8316BF14-636D-4C63-9A0D-0357FEA8E26A}.png)

>Aquí marcamos la imagen a restaurar, en este caso es la única almacenada. En la parte inferior podemos ver las propiedades del repositorio

![alt text]({6DEDE517-B79C-43BC-ADF6-5F0FAE8E1A15}.png)

>En este caso el modo de despliegue será en multicast, así que marcamos la primera opción. Cabe recalcar que multicast es un modo en el que podemos enviar paquetes a la vez a varios dispositivos seleccionados.

![alt text]({63C3A7FD-B3F9-4306-8F41-9B09FAC30F3E}.png)

>Restauramos la imagen al disco completo de los clientes

![alt text]({33840438-8F71-4BF1-91D6-4021C79D138B}.png)

![alt text]({AA26AFA9-D510-42CA-BABE-FC1A3717E336}.png)

> Se crean las tablas de particiones proporcionalmente ya que los discos de origen cuando se realizó la imagen del disco no tienen las mismas propiedades de almacenamiento que los de destino.

![alt text]({1A763BF1-9D27-4CB3-93B2-D469EF5309AB}.png)

>Primera opción, multicast ya explicada anteriormente.

![alt text]({C2110A6F-342B-46DA-B4FF-ABD5656428CB}.png)

>En este caso podemos usar el modo de número de clientes ya que son pocas máquinas (2) y es menos probable que falle alguna de ellas, en casos de clonación masiva es recomendable usar tiempos de espera.

![alt text]({656BF33A-45C9-43DA-8EB3-142F4F6FDCEB}.png)

>Servidor a la espera de que se complete el proceso de restauración

![alt text]({37E2185B-0E98-4F7B-8EDB-43B616CDCA01}.png)

>En este momento las máquinas clientes se encuentran en modo DHCP buscando el servidor para que les propague la restauración de imagen

![alt text]({6C97832D-7569-4A56-9FAF-EA794BC9D1D2}.png)

> Clientes ya conectados al servidor iniciando el proceso.

![alt text]({04BD9B28-1821-494C-994B-7B7228EFA175}.png)


### Inicio del proceso de restauración en las dos máquinas:

>Primer proceso conjunto

![alt text]({DE785484-4ED6-4174-9AB1-87DEE58DB70B}.png)
![alt text]({3BE1816E-24BF-4412-9C2B-15A8E72FD2F4}.png)

>Segundo proceso conjunto

![alt text]({61BABD0E-3FCD-4ECC-AEFA-80206F9D7F7C}.png)

>Proceso de restauración completado con éxito en las dos máquinas clientes.

![alt text]({529E568B-94DD-476D-B8A7-E67478654BB7}.png)
![alt text]({C8324202-7594-4F0A-9B1E-9EEED53C7C76}.png)