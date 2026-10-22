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

<img width="492" height="419" alt="03-UserSignIn-TAP" src="https://github.com/user-attachments/assets/f7c94402-3dc5-469a-86a4-6b051cd46a8d" />

- Automaticamente, nos solicita agregar un metodo de autenticacion, en este caso agregamos "Microsoft Authenticator"

<img width="547" height="425" alt="03-UserSignIn-NewAuthMethod" src="https://github.com/user-attachments/assets/51321b94-e785-41f0-8e9b-fd0a026d7e13" />


- Una vez configurado Microsoft Authenticator, podremos ingresar

<img width="508" height="560" alt="03-UserSignIn-AuthMethodOK" src="https://github.com/user-attachments/assets/891f0250-219f-4332-8542-8386867b5f89" />

---

### Fase 4: Activación y validación de SSPR

- Ingresamos al apartado "Password Reset" y en "Properties" establecemos "all" de esta manera activamos el SSPR para todos los usuarios.

<img width="503" height="189" alt="04-PasswordReset" src="https://github.com/user-attachments/assets/22f20c82-985c-464b-adfe-31819d32ab75" />


- En "Authentication Methods" establecemos que solo 1 método de autenticación es suficiente para proceder con el SSPR y *no* agregamos las "security questions" (preguntas de seguridad) como método válido ya que estan cosideradas como un método débil.

<img width="967" height="458" alt="04-AuthMethods" src="https://github.com/user-attachments/assets/1e8ce45e-3cf2-4ad9-b66b-70f0c6ebd203" />

- si ingresamos a "Auth Methods Policy" vemos cuales son los métodos de autenticación válidos (Notese como los SMS o Email OTP estan desactivados ya que se consideran vulnerables ante phishing)

<img width="1055" height="660" alt="04-AuthMethods-Policy" src="https://github.com/user-attachments/assets/0ea5ab1d-fdcf-47e5-826b-8dbf712a1be1" />
   
- Con esta configuracion establecimos:
  - SSPR habilitado para todos los usuarios
  - 1 método de autenticación es suficiente para comenzar el proceso de SSPR
  - Desactivamos la posibilidad de responder preguntas de seguridad debido a que no se considera un metodo seguro
  - Desactivamos métodos de autenticación como SMS o Email OTP ya que son vulnerables a Phishing

**Verificación**

-  Mediante el link de recuperacion de contraseña, ingresamos el UPN 

<img width="394" height="381" alt="04-USER-SSPR" src="https://github.com/user-attachments/assets/01fa45ab-5823-46c1-82a1-e06554ed012b" />

- Como anteriormente registramos Microsoft Authenticator como metodo autenticacion, podemos seleccionar esta variente para que nos llegue un código. 

<img width="532" height="499" alt="04-UserSSPR-Auth" src="https://github.com/user-attachments/assets/a109eb21-f7cc-46ac-82d1-cc505664d7fc" />

- Una vez ingresado el codigo, ya podemos generar una nueva contraseña

<img width="365" height="370" alt="04-UserSSPR-Password (1)" src="https://github.com/user-attachments/assets/5d7733de-c39e-4c99-89cd-f0a06e84a371" />

- Una vez aprobado el cambio de contraseña, el usuario podra ingresar a su cuenta. 
<img width="368" height="171" alt="04-UserSSPR-OK" src="https://github.com/user-attachments/assets/42139e99-a779-4a22-a6c6-31451039d2ac" />
<img width="1682" height="735" alt="04-UserSSPR-AccessOK" src="https://github.com/user-attachments/assets/81e54d27-2043-4f2f-808c-3859b04cd92e" />

---

### Auditoría y Trazabilidad de Eventos (Logs Analysis)

## Auditoría del Pase de Acceso Temporal (TAP)

- Habilitación del metodo TAP para los usuarios

<img width="792" height="419" alt="Auditoria-TAP" src="https://github.com/user-attachments/assets/b8a96cc5-4c88-4c00-ba44-c9e639a304bb" />

- Logs correspondientes al inicio de sesión del user:  

<img width="874" height="418" alt="Audit-User-Overview" src="https://github.com/user-attachments/assets/6a91601b-6ed5-45ff-a4db-4c2a70e70a9d" />

- El primer log se encuentra en estado “Interrupted”. El usuario ingreso con su codigo TAP, pero como Entra ID no le dio acceso debido a que necesitaba ingresar un nuevo metodo de Verificacion (agregamos Microsoft Authenticator) interrumpio el ingreso y redirigio a la a configuracion de este nuevo metodo.

<img width="830" height="670" alt="Audit-User-TAP" src="https://github.com/user-attachments/assets/912fd37b-1a96-4fae-ade8-d9f870b6ee77" />
<img width="829" height="218" alt="Audit-User-TAP-Detail" src="https://github.com/user-attachments/assets/6a844168-a005-432d-b8d6-c5840777f188" />

- En el segundo log vemos que se vinculo exitosamente Microsoft Authenticator como método de autenticación

<img width="678" height="633" alt="Audit-User-MicrosoftAuthApp" src="https://github.com/user-attachments/assets/20625659-a03e-43f9-a20c-b63f3b3b87a2" />

- El tercer Log tambien se muestra en estado “Interrupted” debido a que Microsoft interrumpe el acceso para preguntar si el usuario quiere mantener su sesión abierta.

<img width="713" height="704" alt="Audit-User-RemainSigIn" src="https://github.com/user-attachments/assets/0ac64572-401a-4b53-b961-bc42bbfdb534" />

- El cuarto Log, ,muestra un inicio de sesion exitoso y la redireccion a “my profile”

<img width="683" height="637" alt="Audit-User-OK" src="https://github.com/user-attachments/assets/d1d010c3-6d35-4d9f-886a-c95d46552879" />

- El ultimo log es la redireccion a "my profile" realizada con exito

<img width="679" height="637" alt="Audit-User-OKMyProfile" src="https://github.com/user-attachments/assets/f46e67b0-a965-4964-8e2b-40b313ac2a4a" />

#### Auditoría de Autoservicio de Contraseñas (SSPR)

- Habilitación del uso del SSPR para todos los Users

<img width="522" height="459" alt="Audit-SSPR-All" src="https://github.com/user-attachments/assets/b55a507e-2fe5-41bd-8ed1-c329b1b14d90" />
<img width="563" height="274" alt="Audit-SSPR-AllDetails" src="https://github.com/user-attachments/assets/f4e0b2d2-bff3-40d9-be2c-f86dc6d86608" />

- Luego, vemos el proceso del SSPR documentado por Microsoft Entra ID:
  - El user ingresa su UPN
  - Entra ID muestra las opciones de para verificar su identidad (Mediante Microsoft Authenticator)
  - Se documenta el inicio y la culminación de la verificacion mediante un codigo en Microsoft Authenticator
  - Se documenta que el usuario completo exitosamente los pasos requeridos para reestablecer la contraseña
  - El user agrega la nueva contraseña
  - Se documenta que el usuario reseteo su contraseña exitosamente

<img width="1531" height="511" alt="Audit-SSPR-Overview" src="https://github.com/user-attachments/assets/d96238b8-6b3e-4fbc-8f59-0294bd7bd9c6" />

##  Conclusiones y Consideraciones de Seguridad

**Eliminación del Vector de Phishing Inicial:** El uso de un Pase de Acceso Temporal (TAP) de un solo uso o duración limitada permite resolver el problema clásico del "bootstrap" o contraseña temporal enviada por canales inseguros, garantizando que el primer ingreso se realice mediante credenciales fuertes, atadas al dispositivo físico del usuario.

**Trazabilidad y Visibilidad:** Gracias al análisis detallado de los Audit Logs y Sign-in Logs, se comprobó que es posible auditar cada etapa vista en este proyecto, desde la emisión de políticas (PolicyManagement), pasando por las interrupciones esperadas de cumplimiento normativo, hasta la resolución autónoma de incidentes mediante SSPR.

**Optimización de Costos Operativos para Help Desk:** La correcta configuración y habilitación masiva de SSPR combinada con MFA reduce drásticamente la fricción operativa y los tiempos de atención del HelpDesk ante bloqueos o pérdidas de credenciales, trasladando la responsabilidad de recuperación de forma segura al usuario final.





