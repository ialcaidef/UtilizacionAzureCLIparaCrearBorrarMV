

## Creacion de la maquina virtual en Azure Cli

### Conectarse desde Azure Cli A Azure

```
az login
```

![01](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/01.png)

![02](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/02.png)

![03](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/03.png)

![05](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/05.png)

### Creando un grupo de recursos

```
az group create -l EastUS -n myRGCLI 
```

![06](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/06.png)

![07](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/07.png)

### Creando una máquina virtual Linux

```
az vm create ^
 --name myVMCLI ^
 --resource-group myRGCLI ^
 --image UbuntuLTS ^
 --location EastUS ^
 --admin-username azureuser ^
 --admin-password Pa$$w0rd1234 ^
 --no-wait
```

![09](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/09.png)

![08](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/08.png)

![10](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/10.png)

Conectarse a la máquina Virtual de Linux

```
ssh azureuser@104.211.52.252
Nota: Dar que si en la creación del certificado SSH
```

Hay que cambiar la password desde el portal de azure para poder conectar por ssh, ya que tiene que tener un mínimo de 12 caracteres entre otras restricciones.

![12](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/12.png)

Una vez cambiada, ya se puede acceder por ssh

![11](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/11.png)

1 - Actualizar en Linux

```
sudo apt-get update
```

![13](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/13.png)

2 - Hacer el upgrade

```
sudo apt upgrade
```

![14](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/14.png)

3 - Instalar un servidor web

```
sudo apt install -y apache2 apache2-utils
```

![15](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/15.png)

4 - Vemos el estatus de Apache

```
systemctl status apache2
```

![16](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/16.png)

5 - Ponemos un mensaje en nuestra página de Apache

```
cd /var/www/html
```

![17](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/17.png)

6 - Poner una nota en la página inde.html

```
sudo vi index.html <ENTER>
<ESC> : 198 <ENTER> // irme a la linea 198 que es donde esta el mensaje de index.html
<i> PONER EL MENSAJE <ESC>
: x <ENTER>

```

![18](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/18.png):

7 - Salir del SSH

```
exit <ENTER>
```

**Nota:**

El puerto 80 deberá ser abierto desde NSG.

Destination PortRanges: 80

Name: Port_80

Probariamos que llegamos a la maquina virtual: con la IP desde cualquier navegador.

![19](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/19.png)

## Parar y "deallocate" la máquina virtual

```
az vm stop --resource-group myRGCLI --name myVMCLI --no-wait
```

```
az vm deallocate -g myRGCLI -n myVMCLI --no-wait
```

![20](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/20.png)

## Iniciar la máquina virtual

```
az vm start -g myRGCLI -n myVMCLI --no-wait
```

![21](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/21.png)

## Borrar la máquina virtual

```
az vm delete -g myRGCLI -n myVMCLI --yes --no-wait
```

![22](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/22.png)

### Mostrar informacion de la máquina virtual

```
az vm show -g myRGCLI -n myVMCLI -d
```

![23](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/23.png)

Borrar el grupo de recursos

```
az group delete -n myRGCLI  --yes --no-wait
```

![24](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/24.png)

![25](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/25.png)

## Desconectamos de Azure

```
az logout
```

![26](https://github.com/ialcaidef/UtilizacionAzureCLIparaCrearBorrarMV/blob/main/Images/26.png)

Mas información:

[Manage Linux or Windows virtual machines.](https://docs.microsoft.com/en-us/cli/azure/vm?view=azure-cli-latest)

