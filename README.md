# Script de Instalación de Odoo 17 con FECOL y Enterprise

Este script automatiza la instalación de Odoo 17 en sistemas Ubuntu, incluyendo la configuración de todos los componentes necesarios y la clonación de los repositorios FECOL y Enterprise.

## Requisitos Previos

- Sistema operativo Ubuntu (preferiblemente Ubuntu 22.04 LTS)
- Privilegios de administrador (sudo)
- Acceso a Internet

## Características Principales

- Instalación completa de Odoo 17 desde GitHub
- Configuración automática de PostgreSQL
- Instalación de todas las dependencias necesarias
- Clonación de repositorios personalizados (FECOL y Enterprise)
- Configuración de entorno virtual Python
- Creación y configuración del servicio systemd

## Detalles de Instalación

El script realiza las siguientes operaciones:

1. Actualización del sistema
2. Instalación de dependencias (PostgreSQL, Node.js, etc.)
3. Configuración de PostgreSQL
4. Creación del usuario dedicado para Odoo
5. Instalación de wkhtmltopdf para reportes PDF
6. Clonación del repositorio oficial de Odoo 17
7. Clonación de repositorios adicionales:
   - FECOL: Módulos específicos para facturación electrónica colombiana
   - Enterprise: Módulos empresariales de Odoo
8. Configuración del entorno virtual Python y dependencias
9. Creación del archivo de configuración de Odoo
10. Configuración del servicio systemd

## Uso

1. Descargue el script de instalación
2. Otorgue permisos de ejecución:
   ```
   chmod +x install_odoo17.sh
   ```
3. Ejecute el script con privilegios de administrador:
   ```
   sudo ./install_odoo17.sh
   ```

## Acceso Post-Instalación

Una vez completada la instalación:
- Acceda a Odoo desde su navegador: http://localhost:8069
- Usuario por defecto: admin
- Contraseña: La especificada como admin_passwd en el archivo de configuración

## Directorios Importantes

- **Instalación de Odoo**: `/opt/odoo17/odoo`
- **Módulos adicionales**: `/opt/odoo17/odoo/extra-addons` (FECOL)
- **Módulos enterprise**: `/opt/odoo17/odoo/enterprise`
- **Archivo de configuración**: `/etc/odoo17.conf`

## Administración del Servicio

```bash
# Iniciar Odoo
sudo systemctl start odoo17

# Detener Odoo
sudo systemctl stop odoo17

# Reiniciar Odoo
sudo systemctl restart odoo17

# Comprobar estado
sudo systemctl status odoo17

# Ver logs
sudo journalctl -u odoo17 -f
```

## Consideraciones de Seguridad

- **IMPORTANTE**: Cambie la contraseña predeterminada `admin_password` en `/etc/odoo17.conf`
- Considere configurar un proxy inverso (Nginx/Apache) con SSL para entornos de producción
- Revise los permisos de archivos y directorios para mayor seguridad

## Tokens de Acceso a Repositorios

El script utiliza tokens de acceso para clonar los repositorios privados. En entornos de producción, se recomienda:

1. Utilizar tokens temporales o específicos para la instalación
2. Eliminar las referencias a los tokens después de la instalación
3. Configurar claves SSH para actualizaciones posteriores

## Resolución de Problemas

Si encuentra errores durante la instalación:

1. Revise los mensajes de error en la salida del script
2. Verifique los logs del sistema: `sudo journalctl -u odoo17`
3. Compruebe los permisos de los directorios y archivos
4. Asegúrese de que los puertos necesarios (8069, 8072) estén disponibles

## Personalización

El script puede ser modificado para adaptarse a necesidades específicas:
- Cambiar puertos
- Ajustar número de workers
- Modificar rutas de instalación
- Agregar repositorios adicionales

---

**Nota**: Este script está diseñado para entornos de desarrollo o pruebas. Para entornos de producción, se recomienda realizar configuraciones adicionales de seguridad y rendimiento.
