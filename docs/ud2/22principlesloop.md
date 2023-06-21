# Principios del diseño de bucles

+ Un bucle de conteo se utiliza siempre que se sepa de antemano exactamente cuántas iteraciones se necesitan. La instrucción **_for_** de Java es una estructura apropiada para codificar un bucle de conteo.
+ Se debe usar una estructura **_while_** cuando el problema sugiera que el cuerpo del bucle puede omitirse por completo.
+ Una estructura **_do-while_** debe usarse solo cuando un bucle requiere al menos una o más iteraciones.
+ La variable de bucle se utiliza para especificar la condición de entrada de bucle. Debe inicializarse a un valor inicial apropiado y debe actualizarse en cada iteración del bucle.
+ El límite de un bucle puede ser un recuento, un centinela o, de manera más general, un límite condicional. Debe estar correctamente especificado en la expresión de entrada de bucle y el progreso hacia el límite debe realizarse en el actualizador.
+ Puede producirse un bucle infinito si el inicializador, la expresión de entrada de bucle o la expresión del actualizador no se especifican correctamente.
