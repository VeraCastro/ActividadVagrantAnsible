# ActividadVagrantAnsible
Implementación de un despliegue con vagrant, virtual box y ansible


#  Generador Automático de Partidos de Tenis - UNIR

Sistema automatizado para generar partidos de tenis aleatorios usando **Vagrant**, **Ansible** y **VirtualBox**.

## Descripción

Este proyecto implementa un sistema que genera automáticamente información de partidos de tenis entre dos tenistas:
- **Primer tenista**: Datos configurados manualmente
- **Segundo tenista**: Datos obtenidos aleatoriamente desde la API de RandomUser.me
- **Fecha del partido**: Generada automáticamente

## Tecnologías Utilizadas

- **Vagrant 2.4+**: Gestión de máquinas virtuales
- **Ansible 2.12+**: Automatización y configuración
- **VirtualBox 7.1+**: Proveedor de virtualización
- **Ubuntu 20.04**: Sistema operativo base

##  Estructura del Proyecto

```
proyecto_tenis/
├── Vagrantfile                     # Configuración de Vagrant
├── playbook.yml                    # Playbook principal de Ansible
├── partido_vars.yml                # Variables del primer tenista
├── partido.txt                     # Archivo generado (resultado)
└── roles/
    └── partido_tenis/
        ├── tasks/
        │   └── main.yml            # Tareas del rol
        ├── templates/
        │   └── partido.txt.j2      # Template del archivo resultado
        └── vars/
            └── main.yml            # Variables del rol
```

##  Instalación y Uso

### Prerrequisitos

Asegúrate de tener instalado:

```bash
# Verificar instalaciones
vagrant --version
vboxmanage --version
ansible --version
```

### Instalación en Debian/Ubuntu

```bash
sudo apt update
sudo apt install vagrant virtualbox ansible
```

### Ejecución

1. **Clonar el repositorio**:
   ```bash
   git clone <tu-repositorio>
   cd proyecto_tenis
   ```

2. **Ejecutar el proyecto**:
   ```bash
   vagrant up
   ```

3. **Ver el resultado**:
   ```bash
   cat partido.txt
   ```

##  Resultado Esperado

El archivo `partido.txt` generado contiene:

```
** INFORMACION DEL PARTIDO UNIR **

First Name: Aitor.
Last Name: Menta.
City: Madrid.
id: 1234.

First Name: Sarah.
Last Name: Johnson.
City: Springfield.
id: a1b2.

Fecha: 2023-05-12T10:04:54Z.
```

##  Configuración

### Variables del Primer Tenista

Edita `playbook.yml` para cambiar los datos del primer tenista:

```yaml
vars:
  first_name: "Tu_Nombre"
  last_name: "Tu_Apellido" 
  city: "Tu_Ciudad"
```

### ID del Primer Tenista

Modifica `partido_vars.yml`:

```yaml
primer_tenista_id: 5678
```

##  Comandos Útiles

```bash
# Crear y ejecutar por primera vez
vagrant up

# Re-ejecutar solo el playbook
vagrant provision

# Conectarse a la VM
vagrant ssh

# Ver el archivo generado desde la VM
vagrant ssh -c "cat /vagrant/partido.txt"

# Destruir la VM
vagrant destroy
```

##  API Utilizada

- **RandomUser.me**: `https://randomuser.me/api/?results=1`
- Genera datos aleatorios de usuarios ficticios
- Campos utilizados: `name.first`, `name.last`, `location.city`, `login.uuid`

##  Solución de Problemas

### Error de vagrant-vbguest

Si obtienes errores relacionados con `vagrant-vbguest`:

```bash
vagrant plugin uninstall vagrant-vbguest
vagrant plugin install vagrant-vbguest
```

### Problemas de conectividad

Si la API no responde, verifica tu conexión a internet desde la VM:

```bash
vagrant ssh -c "curl -I https://randomuser.me/api/"
```

##  Estructura de Ansible

### Rol `partido_tenis`

- **Tasks**: Obtiene datos de la API, genera fecha y crea el archivo
- **Templates**: Formato del archivo de salida usando Jinja2
- **Variables**: URL de la API y configuraciones

### Playbook Principal

- Define las variables del primer tenista
- Carga variables desde archivo externo
- Ejecuta el rol `partido_tenis`

##  Objetivos Cumplidos

- ✅ Desarrollo con Vagrant y Ansible
- ✅ Creación de playbooks y roles
- ✅ Uso de diferentes ubicaciones de variables
- ✅ Integración con APIs REST
- ✅ Generación automática de archivos
- ✅ Templates con Jinja2

## Autor

  Verónica M. Castro
- Universidad Internacional de La Rioja (UNIR)
- Asignatura: Herramientas de Automatización de Despliegues

##  Licencia

Este proyecto es parte de una actividad académica de UNIR.

---

*Generado automáticamente con ❤️ usando Vagrant + Ansible*
