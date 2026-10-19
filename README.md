# Secure-Passwordless-Onboarding-TAP-Self-Service-Password-Reset-SSPR-en-Microsoft-Entra-ID
Este proyecto documenta el diseño e implementación de una solución de gestión de credenciales basada en **Zero Trust** para Microsoft Entra ID. Reduciendo significativamente el volumen de tickets de Nivel 1 en Helpdesk.
## Objetivos
1. **Onboarding Seguro (Passwordless-Ready):** Utilizacion contraseñas temporales de un unico uso mediante **Temporary Access Pass (TAP)**.
2. **Eficiencia Operativa:** Implementar **Self-Service Password Reset (SSPR)** para capacitar a los usuarios en la auto-gestión de credenciales, 

---

## Implementacion
### Fase 1: Configuración de Temporary Access Pass (TAP) *
 **Objetivo:** Permitir el registro inicial de usuarios y dispositivos sin necesidad de una contraseña permanente.
**Configuración:** 
  * Habilitación de TAP en la directiva de *Authentication Methods* de Entra ID.
    
  * Definición de políticas: Duración del pase (ej. 1 a 8 horas), uso único (*One-time use*) y longitud del código. * 
**Flujo Operativo:** 
1. El Helpdesk genera un TAP para el nuevo usuario. 
2. El usuario inicia sesión por primera vez únicamente con su UPN y el código TAP. 
3. El sistema exige registrar un método fuerte (Microsoft Authenticator / SSPR) antes de continuar. 
