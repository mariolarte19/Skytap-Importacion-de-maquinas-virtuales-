# ☁️ Skytap-Importacion-de-maquinas-virtuales ☁️

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


Algunas imágenes OVA y OVF no están basadas en VMware y no pueden importarse directamente a Skytap. Por ejemplo, las máquinas virtuales VirtualBox no están basadas en VMware, porque no se exportaron desde un hipervisor VMware (VMware Server, VMware Workstation, VMware ESX, etc.).

Para importar OVA y OVF que no sean de VMware a Skytap, debemos convertir esta imagen y una de las formas es usando VMware vCenter Converter.


**Instrucciones:**

1. Si la VM es un archivo OVF, primero conviértalo al formato VMX. Para obtener instrucciones, consulte [Conversión de archivos OVF a VMX para usar con VMware Converter](https://help.skytap.com/Using_OVF_Converter_Tool.html).


2. Descargue e instale VMware vCenter Converter en su máquina local, para la descarga lo puede hacer desde el siguiente link:

```
https://www.vmware.com/products/converter.html
```

3. Abra VMware vCenter Converter.
4. Haga clic en **Convertir máquina**.
5. En **Tipo de origen**, seleccione **VMware Workstation u otra máquina virtual VMware**. Elija la ubicación del archivo VMX u OVA. Haga clic en **Siguiente**.
6. En **Seleccionar tipo de destino**, seleccione **VMware Workstation u otra máquina virtual VMware**.
7. En **Seleccionar producto VMware**, seleccione **VMware Workstation 11.0**.
8. Ingrese un nombre para su VM en el campo **Nombre**.
9. Seleccione una ubicación de destino para el archivo convertido. Haga clic en **Siguiente**.
10. Para aceptar las opciones predeterminadas, haga clic en **Siguiente**.
11. En la página de resumen, verifique la configuración.
12. Haga clic en **Finalizar** para comenzar el proceso de conversión. Dependiendo del tamaño de la VM, el proceso de conversión puede tardar más de una hora en completarse.
13. **Importe la máquina virtual** convertida en Skytap, Este proceso lo puede realizar siguiendo esta guia siguiendola como si la imagen ya fuera VMware, o si desea información adicionar la puede consultar [aqui](https://help.skytap.com/importing-vms-overview.html).

 
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
<img width="944" src="https://github.com/mariolarte19/Skytap-Importacion-de-maquinas-virtuales-/blob/master/Skytap9.PNG">
</p>

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
