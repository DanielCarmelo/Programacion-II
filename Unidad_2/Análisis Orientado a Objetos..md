 1) Etapa de Análisis Orientado a Objetos (AOO)
El Análisis Orientado a Objetos consiste en examinar los requisitos del sistema desde la perspectiva de las clases y objetos encontrados en el vocabulario del dominio del problema. Su objetivo es desarrollar un modelo que describa qué debe hacer el sistema, identificando los objetos del mundo real y cómo interactúan entre sí.

El Diagrama de Clases Conceptual sirve para representar visualmente las entidades (clases), sus atributos y las relaciones entre ellas. Dentro del AOO, no se enfoca en la implementación técnica (código), sino en capturar las reglas de negocio y la estructura de la información del dominio.

2) Documento vital para el modelo de análisis
El documento vital es la Especificación de Requerimientos (o Casos de Uso). Es fundamental porque allí se detallan las funcionalidades y reglas de negocio que el modelo de objetos debe ser capaz de soportar.

3, 4 y 5) Diagrama de Clases: Fútbol
Restricción (Pregunta 5): Es necesario incorporar una restricción (generalmente mediante una nota o OCL) que indique que el Capitán de un equipo debe ser uno de los jugadores que integra dicho equipo. Sin esta restricción, el modelo permitiría que un jugador capitanee un equipo al que no pertenece.

Fragmento de código
classDiagram
    class EQUIPO {
        string nombre
    }
    class JUGADOR {
        string cedula
        string apellido
    }
    EQUIPO "1" -- "11..*" JUGADOR : integra
    EQUIPO "0..1" -- "1" JUGADOR : capitanea
6 y 7) Alumnos, Exámenes y Profesores (Clase de Asociación)
Cuando la relación entre dos clases tiene atributos propios (como la nota), se utiliza una Clase de Asociación.

Fragmento de código
classDiagram
    class ALUMNO {
    }
    class EXAMEN {
    }
    class PROFESOR {
    }
    class RENDICION {
        date fecha
        float nota
    }
    ALUMNO "*" -- "*" EXAMEN
    (ALUMNO, EXAMEN) .. RENDICION
    RENDICION "*" -- "1" PROFESOR : corregido por
8) Agregación y Composición: Computadora
Composición (Rombo negro): Partes esenciales que no tienen sentido sin el todo (CPU, Discos).

Agregación (Rombo blanco): Partes opcionales o conectadas (Periféricos, Cámara, Parlantes).

Fragmento de código
classDiagram
    class Computadora
    Computadora *-- "1" CPU
    Computadora *-- "1..3" DiscoDuro
    Computadora o-- "2..*" Periferico
    Computadora o-- "0..1" CamaraWeb
    Computadora o-- "0..1" Parlantes
9 y 10) Herencia y Clases Abstractas
Pregunta 9: Sí, si la clase VEHÍCULO es concreta, podrían instanciarse objetos que sean simplemente "Vehículos" sin ser autos ni camiones.

Pregunta 10 (Clase Abstracta): Si VEHÍCULO es abstracta, ya NO pueden existir vehículos puros. Todo objeto debe ser obligatoriamente un AUTO o un CAMIÓN (u otra subclase concreta).

Fragmento de código
classDiagram
    class VEHICULO {
        <<abstract>>
    }
    VEHICULO <|-- AUTO
    VEHICULO <|-- CAMION
11) Dueño y Remolque
¿Los Camiones tienen Dueño? Sí, por herencia de VEHÍCULO.

¿Los Autos tienen Dueño? Sí, por herencia de VEHÍCULO.

¿Los Vehículos comunes tienen Remolque? No, la relación con REMOLQUE es exclusiva de la clase CAMIÓN.

Relaciones heredadas: La asociación con DUEÑO fue heredada por AUTO y CAMIÓN desde la superclase VEHÍCULO.

12) Diagrama Completo: Gerentes y Vendedores
Fragmento de código
classDiagram
    class Empleado {
        <<abstract>>
        string cedula
        string nombre
    }
    class Gerente {
        string departamento
    }
    class Vendedor {
        <<abstract>>
        float comision
    }
    class VendedorFijo {
        string horario
    }
    class VendedorZafral {
        string periodoContratacion
    }
    class Cliente {
        string razonSocial
        string direccion
    }
    class Atencion {
        date fecha
        time hora
    }

    Empleado <|-- Gerente
    Empleado <|-- Vendedor
    Vendedor <|-- VendedorFijo
    Vendedor <|-- VendedorZafral

    Vendedor "1..*" -- "*" Cliente : Atiende
    (Vendedor, Cliente) .. Atencion
