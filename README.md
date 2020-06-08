# Skytap-Importacion-de-maquinas-virtuales-

#  ☁️ POC Skytap ☁️
En esta guía encontrará el paso a paso detallado para la importación de sus máquinas a Skytap usando FTP.

### Indice:
1. [Preparación de máquinas virtuales para importar](#1-preparación-de-máquinas-virtuales-para-importar)
- [Máquinas virtuales basadas en VMware](#a-máquinas-virtuales-basadas-en-VMware)
- [Máquinas virtuales no basadas en VMware](#b-máquinas-virtuales-no-basadas-en-VMware)
2. [Crear un trabajo de importación en Skytap](#2-crear-un-trabajo-de-importación-en-Skytap)
3. [Cargar los archivos vía FTP](#3-cargar-los-archivos-vía-FTP)
4. [Inicio del proceso de análisis e importación](#4-inicio-del-proceso-de-análisis-e-importación)
5. [Notas](#Notas-)
6. [Referencias](#Referencias-)


## 1. Preparación de máquinas virtuales para importar
¿Sus máquinas virtuales estan basadas en VMware? Si la respuesta es si, siga las instrucciones del numeral A, de lo contrario siga las instrucciones del numeral B.

### A. Máquinas virtuales basadas en VMware
Skytap admite archivos OVA (recomendado), paquetes OVF y archivos VMX. Lea detenidamente los pasos de importación según la herramienta que utilice. **Apague las máquinas virtuales antes de iniciar el proceso.**

VMware workstation:
* Seleccione _Archivo_ > _Exportar a OVF_.
* Al seleccionar el nombre del archivo cambie la extensión a .ova y seleccione _Guardar_.

vSphere:
* Seleccione _Acciones_ dentro del vSphere Web Client y elija una máquina virtual o vApp.
* Seleccione Exportar plantilla OVF, elija un nombre y ubicación de archivo.
* En el campo _Formato_ seleccione preferiblemente el formato OVA.
* Si habilita el campo opciones avanzadas podrá incluir información adicional o configuraciones en la plantilla exportada. 
Si desea más información sobre importación de máquinas virtuales desde vSphere visite la documentación de [VMware vSphere](https://docs.vmware.com/en/VMware-vSphere/5.5/com.vmware.vsphere.vm_admin.doc/GUID-B05A4E9F-DD21-4397-95A1-00125AFDA9C8.html).

Fusion Pro:
* Elija la máquina virtual, seleccione _Archivo_ > _Exportar a OVF_ y elija un nombre y ubicación de archivo.
* Seleccione el formato del archivo, preferiblemente el formato OVA y haga clic en _Exportar_.

Si no puede crear archivos de tipo OVA es recomendado comprimir los archivos OVF / VMDK o VMX / VMDK en un archivo 7z, utilizando la herramienta [7-zip](https://www.7-zip.org/).

### B. Máquinas virtuales no basadas en VMware

 Las máquinas virtuales no basadas en VMware no pueden importarse directamente a Skytap (por ejemplo máquinas VirtualBox), Esto se debe a que el formato base se la imagen no es compatible con Skytap. Para Solucionar este problema se debe convertir esta imagen, y se puede hacer de las siguinetes maneras:
 
 #### Opción 1:
 
 #### Opción 2:
 
 ## 2. Crear un trabajo de importación en Skytap
 
 Para cada archivo cree un _trabajo de importación_ dentro de Skytap mediante los siguientes pasos:
 
 * Ingrese en _Environments_ ubicado en la barra superior, luego en **VM imports** de clic en el botón **Create VM import job**.
  
  
 <p align="center">
<img width="956" alt="Skytap2" src="https://github.com/JulianaLeonGonzalez/Skytap-POC/blob/master/Imagen2.png">
</p>
 


 * Ingrese la información sobre su importación y al finalizar de clic en el botón _Save import job_.

 
 <p align="center">
<img width="929" alt="Skytap5" src="https://github.com/JulianaLeonGonzalez/Skytap-POC/blob/master/Imagen3.png">
</p>

 
 ## 3. Cargar los archivos vía FTP
 
 Para este paso necesitará un cliente FTP, le recomendamos el uso de [WinSCP](https://winscp.net/eng/index.php) para Microsoft.
 * En la interfaz de Skytap encontrará las credenciales para la conexión FTP.
 


<p align="center">
<img width="929" alt="skytap1" src="https://github.com/JulianaLeonGonzalez/Skytap-POC/blob/master/Imagen4.png">
</p>
 
 
 * Ingrese en su cliente FTP con las credenciales proporcionadas por Skytap, ingrese en la carpeta _UPLOAD_ y arrastre el archivo.

 <p align="center">
<img width="805" alt="skytap3" src="https://github.com/JulianaLeonGonzalez/Skytap-POC/blob/master/Imagen5.png">
</p>
 

 
  ## 4. Inicio del proceso de análisis e importación
  
Una vez el proceso de carga del archivo en WinSCP termine haga clic en el botón _Create environment_, Skytap iniciará un proceso de análisis archivo de la carpeta _UPLOAD_ para luego importar las máquinas virtuales y crear un entorno virtual con su configuración de red.

<p align="center">
<img width="932" alt="Skytap6" src="https://github.com/JulianaLeonGonzalez/Skytap-POC/blob/master/Imagen6.png">
</p>

Podrá encontrar su máquina en el panel principal.

<p align="center">
<img width="944" src="https://github.com/JulianaLeonGonzalez/Skytap-POC/blob/master/Imagen7.png">
</p>
 
## Notas 📑
* Los archivos OVA requieren menos tiempo para cargarse.
* Skytap eliminará la información incluida en el elemento ExtraConfig durante el proceso de importación.

## Referencias 🔗

Encuentre más información sobre el proceso de importación de Skytap en: [Help Skytap](https://help.skytap.com/imports-using-the-vm-imports-page.html).

## Autores ✒️
Equipo IBM Cloud Tech sales Colombia.
