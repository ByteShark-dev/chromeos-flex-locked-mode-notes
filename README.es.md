# ChromeOS Flex en QEMU/KVM — Investigación de compatibilidad

**ByteShark · Notas experimentales · 9 de noviembre de 2026**

[English version](README.md)

> Esta es una observación de compatibilidad en una sola máquina. **No se afirma haber descubierto una vulnerabilidad**, ni que el entorno cumpla todas las garantías del modo bloqueado de Google Forms, ni se recomienda usar dispositivos no autorizados en evaluaciones reales.

## Objetivo

Ejecutar ChromeOS Flex sin reemplazar Linux y comprobar su funcionamiento en QEMU/KVM. Una vez iniciada la VM, se utilizó **un cuestionario de demostración creado por el propio investigador** para observar su comportamiento con Google Forms en modo bloqueado.

## Entorno probado

| Componente | Configuración |
| --- | --- |
| Anfitrión | CachyOS / Hyprland (Linux x86-64) |
| Kernel | `7.3.3-1-cachyos` |
| Hipervisor | QEMU `11.1.3` con KVM (Intel VT-x) |
| Invitado | ChromeOS Flex actualizado a `156.0.8078.93` (64 bits) |
| Imagen original | Recuperación Reven `16805.36.0` |
| Recursos | 6144 MiB de RAM, 2 vCPU, disco QCOW2 de 32 GiB |
| Gráficos | GTK/OpenGL y `virtio-vga-gl` |
| Entrada | Tableta USB virtual |
| Red | NAT de usuario de QEMU, adaptador e1000 |
| Configuración del dispositivo | Modo personal; inscripción empresarial no completada |

ChromeOS Flex se instaló en un disco **virtual independiente**, sin sustituir el sistema anfitrión. Durante la configuración se resolvió un problema inicial de conectividad y el sistema recibió una actualización.

## Resultados observados

Las pruebas se hicieron **exclusivamente con un formulario de prueba propio**.

| Función | Resultado |
| --- | --- |
| Instalación e inicio de ChromeOS Flex | Correctos |
| Inicio de sesión con cuenta educativa | Correcto |
| Aparición de la interfaz de cuestionario bloqueado | Confirmada |
| Envío de respuesta de prueba | Confirmado |
| Registro de reapertura | Confirmado |
| Notificación por correo sobre reapertura | Recibida |
| Apertura de pestañas dentro del invitado | Restringida |
| Interfaz de extensiones durante el cuestionario | Restringida |
| Copiar y pegar dentro del cuestionario | Restringido en la prueba |
| Equivalencia de seguridad con Chromebook administrada | **No comprobada** |

**Poder abrir y responder el formulario no demuestra que todos los mecanismos de confianza o seguridad se hayan validado.** Las políticas recibidas por una cuenta educativa tampoco demuestran inscripción del dispositivo. No se extrapolan estos resultados a exámenes reales.

## Limitaciones

- Solo una configuración de VM y un formulario propio; falta reproducción independiente.
- No hubo comparación controlada con una Chromebook administrada.
- Los controles del anfitrión y del hipervisor no equivalen a los de un equipo físico.
- No poder abrir la interfaz de una extensión no prueba que todos sus procesos estén detenidos.
- La VM no tenía portapapeles compartido con Linux; ese comportamiento no puede atribuirse al modo bloqueado.
- La ausencia de un aviso visible no demuestra ausencia de otros mecanismos de detección.
- La virtualización de ChromeOS Flex es experimental y no sustituye un dispositivo escolar autorizado.

## Capturas

Se conservaron capturas como evidencia, pero **no se incluyen en esta primera publicación** porque algunas contienen correo institucional y datos de cuenta. Solo se considerarán versiones anonimizadas para una revisión futura.

## Referencias

- [Google: Usar el modo bloqueado para cuestionarios](https://support.google.com/docs/answer/7634943?hl=es-419)
- [Google: Diferencias entre ChromeOS Flex y ChromeOS](https://support.google.com/chromeosflex/answer/11542901?hl=es)
- [QEMU: parámetros de ejecución](https://www.qemu.org/docs/master/system/invocation.html)

## Discusión responsable

Este documento presenta investigación de compatibilidad, no instrucciones para eludir controles de evaluación. Para exámenes reales deben seguirse las indicaciones y autorizaciones de la institución. Se agradecen reproducciones independientes y correcciones.

*ChromeOS, ChromeOS Flex y Google Forms son productos de Google. ByteShark no está afiliado a Google ni al proyecto QEMU.*
