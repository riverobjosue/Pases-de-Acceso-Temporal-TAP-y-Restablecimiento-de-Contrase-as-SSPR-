# Secure-Passwordless-Onboarding-TAP-Self-Service-Password-Reset-SSPR-en-Microsoft-Entra-ID
Este proyecto documenta el diseño e implementación de una solución de gestión de credenciales basada en **Zero Trust** para Microsoft Entra ID. Reduciendo significativamente el volumen de tickets de Nivel 1 en Helpdesk.
## Objetivos
1. **Onboarding Seguro (Passwordless-Ready):** Utilizacion contraseñas temporales de un unico uso mediante **Temporary Access Pass (TAP)**.
2. **Eficiencia Operativa:** Implementar **Self-Service Password Reset (SSPR)** para capacitar a los usuarios en la auto-gestión de credenciales y garantizar la verificación mediante MFA. 

---

## Implementacion
### Fase 1: Configuración de Temporary Access Pass (TAP) *

- En el apartado "Autentication Methods" ingresamos a "Temporary Access Pass"

<img width="1118" height="734" alt="01-AuthMethods-Overview" src="https://github.com/user-attachments/assets/e03fcb06-da0b-4081-9cb8-be3fb736a132" />
  
- asignamos el estado "Enabled" para dejar el metodo activo y en "Target" dejamos "All Users" para establecer que este metodo aplica para todos los usuarios 

<img width="1577" height="371" alt="01-TAP ON   TARGET" src="https://github.com/user-attachments/assets/b4dab196-6f9b-4946-a572-44dba93a9a1a" />

- En el apartado "Configure" aplicamos los siguientes parametros:
  - Duración mínima / máxima: 1 Hora / 8 horas.
  - Require one-time use (uso único): Sí.

<img width="1198" height="370" alt="01-TAP-Settings-Overview" src="https://github.com/user-attachments/assets/aa865ff9-7d8c-480d-a455-6ced2a95efe9" />

Con estas configuraciones establecimos:
 - Metodo de Autenticacion Activo
 - Metodo de Autenticacion aplica para **todos** los usuarios
 - Duración mínima / máxima
 - Establecimos que el código solo puede usarse una vez

---

### Fase 2: Implementacion de TAP para el usuario final

- Creamos al usuario



- Dentro del usuario, vamos al apartado "Authentication Methods" y vamos a agregar el TAP ingresando a "Add Authentication Method"

-

- Seleccionamos Temporary Access Pass, establecemos la duracion del codigo (seleccionamos el minimo de 1 hora) y por defecto el codigo es de un solo uso

-

Con esto, si vemos los detalles del TAP configurado para el usuario, veremos el codigo, el link por el cual va a poder registrarse por primera vez y la duracion del TAP.

---

### Fase 3: Registro con TAP

- Ingresamos el UPN y vemos que Microsoft solicita el TAP
-
- Automaticamente, nos solicita agregar un metodo de autenticacion, en este caso agregamos "Microsoft Authenticator"
-
- Una vez configurado Microsoft Authenticator, podremos ingresar
-  

---

### Fase 4: Activación y validación de SSPR

- Ingresamos al apartado "Password Reset" y en "Properties" establecemos "all" de esta manera activamos el SSPR para todos los usuarios.

- 

- En "Authentication Methods" establecemos que solo 1 método de autenticación es suficiente para proceder con el SSPR y *no* agregamos las "security questions" (preguntas de seguridad) como método válido ya que estan cosideradas como un método débil.


- si ingresamos a "Auth Methods Policy" vemos cuales son los métodos de autenticación válidos (Notese como los SMS o Email OTP estan desactivados ya que se consideran vulnerables ante phishing)

-   

- Con esta configuracion establecimos:
 - SSPR habilitado para todos los usuarios
 - 1 metodo de autenticación es válido para comenzar el proceso de SSPR
 - Desactivamos la posibilidad de responder preguntas de seguridad debido a que no se considera un metodo seguro
 - Desactivamos métodos de autenticación como SMS o Email OTP ya que son vulnerables a Phishing


