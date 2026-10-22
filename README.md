# Secure-Passwordless-Onboarding-TAP-Self-Service-Password-Reset-SSPR-en-Microsoft-Entra-ID
Este proyecto documenta el diseño e implementación de una solución de gestión de credenciales basada en **Zero Trust** para Microsoft Entra ID. Reduciendo significativamente el volumen de tickets de Nivel 1 en Helpdesk.
## Objetivos
1. **Onboarding Seguro (Passwordless-Ready):** Utilizacion contraseñas temporales de un unico uso mediante **Temporary Access Pass (TAP)**. 
2. **Eficiencia Operativa:** Implementar **Self-Service Password Reset (SSPR)** para capacitar a los usuarios en la auto-gestión de credenciales y garantizar la verificación mediante MFA. 

---

## Implementacion
### Fase 1: Configuración de Temporary Access Pass (TAP) *

- En el apartado "Autentication Methods" ingresamos a "Temporary Access Pass"

<img width="1118" height="734" alt="01-AuthMethods-Overview" src="https://github.com/user-attachments/assets/36cf618c-1f69-4f7a-b3a4-3fae64544fbb" />
  
- asignamos el estado "Enabled" para dejar el metodo activo y en "Target" dejamos "All Users" para establecer que este metodo aplica para todos los usuarios 

<img width="1577" height="371" alt="01-TAP ON   TARGET" src="https://github.com/user-attachments/assets/ef3e7c37-2b01-4d4a-b46e-cd8a17a3c014" />

- En el apartado "Configure" aplicamos los siguientes parametros:
  - Duración mínima / máxima: 1 Hora / 8 horas.
  - Require one-time use (uso único): Sí.

<img width="1198" height="370" alt="01-TAP-Settings-Overview" src="https://github.com/user-attachments/assets/a371590c-e32b-48b2-a975-04e2a1b7abee" />
<img width="428" height="858" alt="01-TAP Settings" src="https://github.com/user-attachments/assets/042eed19-8722-401e-9739-2e5251d54b23" />

**Con estas configuraciones establecimos:**
 - Metodo de Autenticacion Activo
 - Metodo de Autenticacion aplica para **todos** los usuarios
 - Duración mínima / máxima
 - Establecimos que el código solo puede usarse una vez

---

### Fase 2: Implementacion de TAP para el usuario final

- Creamos al usuario

<img width="685" height="565" alt="02-CreacionUser" src="https://github.com/user-attachments/assets/e2f222cf-e0f0-4b42-a988-a26aae839129" />


- Dentro del usuario, vamos al apartado "Authentication Methods" y vamos a agregar el TAP ingresando a "Add Authentication Method"

<img width="1530" height="668" alt="02-UserAuthMethod-Overview" src="https://github.com/user-attachments/assets/b7febce4-000c-43a0-ae60-5dd3ddfa7c2d" />


- Seleccionamos Temporary Access Pass, establecemos la duracion del codigo (seleccionamos el minimo de 1 hora) y por defecto el código es de un solo uso

<img width="579" height="252" alt="02-UserTAP" src="https://github.com/user-attachments/assets/ba84421a-de57-4f2b-904c-badc4b1b98db" />
<img width="578" height="338" alt="02-UserTAP-1HR" src="https://github.com/user-attachments/assets/1df69add-7f34-4cb7-8a0d-a611626d323c" />

Con esto, si vemos los detalles del TAP configurado para el usuario, veremos el codigo, el link por el cual va a poder registrarse por primera vez y la duracion del TAP.

<img width="1152" height="671" alt="02-UserTAP-FinishSettings" src="https://github.com/user-attachments/assets/4c292e1f-5b16-48eb-8266-a239d8c85806" />

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
 - 1 método de autenticación es suficiente para comenzar el proceso de SSPR
 - Desactivamos la posibilidad de responder preguntas de seguridad debido a que no se considera un metodo seguro
 - Desactivamos métodos de autenticación como SMS o Email OTP ya que son vulnerables a Phishing

**Verificación**

Mediante el link de recuperacion de contraseña, ingresamos el UPN 

-

Como anteriormente registramos Microsoft Authenticator como metodo autenticacion, podemos seleccionar esta variente para que nos llegue un codigo. 

-

Una vez ingresado el codigo, ya podemos generar una nueva contraseña

-

Una vez aprobado el cambio de contraseña, el usuario podra ingresar a su cuenta. 



