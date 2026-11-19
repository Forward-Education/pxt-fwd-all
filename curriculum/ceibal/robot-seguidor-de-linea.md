# Robot seguidor de línea

```package
fwd-fifa=github:Forward-Education/pxt-fwd-fifa#v0.1.7
fwd-sonar=github:Forward-Education/pxt-fwd-modules/fwd-sonar#v1.1.12
fwd-line=github:Forward-Education/pxt-fwd-modules/fwd-line#v1.1.12
```

```template
input.onButtonPressed(Button.A, function () {
    manejoActivo = true
})
input.onButtonPressed(Button.B, function () {
    manejoActivo = false
})
let manejoActivo = false
basic.forever(function () {
    if (manejoActivo) {
        if (fwdSensors.sonar1.isPastThreshold(0.15, fwdEnums.OverUnder.Under)) {
            fwdMotors.stopDriving()
        } else if (fwdSensors.line2.isLineSensorState(fwdEnums.OnOff.On)) {
            fwdMotors.tank(30, 30)
        } else if (fwdSensors.line1.isLineSensorState(fwdEnums.OnOff.On)) {
            fwdMotors.tank(0, 30)
        } else if (fwdSensors.line3.isLineSensorState(fwdEnums.OnOff.On)) {
            fwdMotors.tank(30, 0)
        }
    } else {
        fwdMotors.stopDriving()
    }
})
```

## ¡Te damos la bienvenida! @showdialog

En depósitos y fábricas, muchos robots siguen líneas pintadas en el piso para llevar mercadería de un lugar a otro. También tienen que frenar de forma segura cuando algo, o alguien, se cruza en su camino.

Hoy vas a programar un **robot móvil** que sigue una línea y se detiene ante obstáculos.

Armá tu robot antes de empezar. También vas a necesitar una línea oscura sobre un piso claro, por ejemplo cinta aisladora negra.

## Tres partes @showdialog

Este tutorial tiene tres partes:

1. **Usar:** tu código ya está listo. Hacé que tu robot siga la línea.
2. **Modificar:** cambiá el código para ajustar cómo maneja tu robot.
3. **Crear:** inventá algo nuevo por tu cuenta.

Podés parar después de cualquier parte. Tu trabajo queda guardado.

## Preparate @showdialog

Encendé la placa de expansión. Conectá tu micro:bit a la computadora.

## Vinculá tu micro:bit @showdialog

Hacé clic en los tres puntos al lado del botón `|Descargar|`. Hacé clic en **Conectar dispositivo**. Seguí los pasos para vincular tu micro:bit.

## Descargá

Hacé clic en `|Descargar|` para enviar el código inicial a tu micro:bit.

## Parte 1: Usar @showdialog

El código de tu robot ya está en el espacio de trabajo. Vamos a descubrir cómo funciona.

1. Seguí las instrucciones de la parte de arriba de la pantalla.
2. Hacé clic en **¡Contame más!** para tener más información.
3. Hacé clic en la lamparita si necesitás ayuda con el código.

## Usar: paso 1

Mirá tu robot. ¿Podés nombrar sus partes? ¿Qué hace cada una?

~hint ¡Contame más!
- La **micro:bit** es el cerebro. Ejecuta el código y toma decisiones.
- La **placa de expansión** es la columna vertebral. Conecta la micro:bit con todo lo demás y tiene la batería.
- El **sensor de línea** y el **sensor sonar** son los órganos de los sentidos. Le dicen al robot qué hay a su alrededor.
- Los **motores y las ruedas** son las extremidades. Mueven al robot.
hint~

## Usar: paso 2

Mirá debajo de la parte de adelante de tu robot. El sensor de línea tiene **tres** sensores chiquitos en fila: **line1**, **line2** y **line3**.

¿Por qué pensás que necesita tres?

~hint ¡Contame más!
- Cada sensor revisa si está arriba de la línea.
- **line2** está en el medio. Si ve la línea, el robot va bien encaminado.
- **line1** y **line3** están a los costados. Si uno de ellos ve la línea, el robot se está desviando y tiene que girar para volver.
hint~

## Usar: paso 3

Mirá el código dentro de ``||basic:para siempre||``. ¿Qué pensás que va a hacer el robot cuando:

- el sensor del medio vea la línea?
- un sensor del costado vea la línea?
- haya algo delante del robot?

```blocks
basic.forever(function () {
    if (manejoActivo) {
        if (fwdSensors.sonar1.isPastThreshold(0.15, fwdEnums.OverUnder.Under)) {
            fwdMotors.stopDriving()
        } else if (fwdSensors.line2.isLineSensorState(fwdEnums.OnOff.On)) {
            fwdMotors.tank(30, 30)
        } else if (fwdSensors.line1.isLineSensorState(fwdEnums.OnOff.On)) {
            fwdMotors.tank(0, 30)
        } else if (fwdSensors.line3.isLineSensorState(fwdEnums.OnOff.On)) {
            fwdMotors.tank(30, 0)
        }
    } else {
        fwdMotors.stopDriving()
    }
})
```

## Usar: paso 4

¡A probar! Desconectá tu robot. Ponelo sobre la línea, con la línea debajo del centro del sensor de línea.

Presioná **A** para arrancar. Presioná **B** para frenar.

¿Sigue la línea? ¿Acertaste con tu predicción?

## Usar: paso 5

Mirá el bloque ``||fwdMotors:drive left 0 % right 30 %||``. ¿Por qué eso haría girar al robot?

~hint ¡Contame más!
- **left** es la rueda izquierda y **right** es la rueda derecha.
- La rueda izquierda se detiene y la derecha sigue andando, así que el robot gira a la **izquierda**.
- Cuando las dos ruedas van a la misma velocidad, como **left 30 % right 30 %**, el robot va derecho.
hint~

## Usar: paso 6

Ahora poné un obstáculo sobre la línea delante del robot, por ejemplo un libro o tu mano. ¿Qué pasa?

~hint ¡Contame más!
- ``||fwdSensors:sonar1 está por debajo de 0.15 m||`` revisa si hay algo a menos de 0,15 m (15 cm).
- Si hay algo, el robot deja de manejar. Cuando el obstáculo ya no está, el robot sigue la línea otra vez.
hint~

## Usar: paso 7

En el código, el sonar se revisa **primero**, antes que los sensores de línea. ¿Por qué pensás que eso es importante?

~hint ¡Contame más!
- La micro:bit revisa cada regla en orden y ejecuta la **primera** que sea verdadera.
- Revisar los obstáculos primero hace que el robot siempre frene ante algo en su camino, aunque esté sobre la línea. ¡La seguridad es lo primero!
hint~

## Punto de control: ¡Lo lograste! @showdialog

¡Tu robot sigue una línea y frena ante obstáculos!

**Pensá:** ¿En qué otros lugares podría ser útil un robot seguidor de línea?

Podés parar acá. O hacé clic en **Siguiente** para pasar a la **Parte 2: Modificar**.

## Parte 2: Modificar @showdialog

Ahora vas a ajustar cómo maneja tu robot.

Después de cada cambio:

1. Conectá tu micro:bit y hacé clic en `|Descargar|`.
2. Desconectala y probá tu robot sobre la línea.

## Modificar: paso 1

¿Y si el robot frenara **más lejos** de los obstáculos?

Cambiá **0.15** en ``||fwdSensors:sonar1 está por debajo de 0.15 m||`` por **0.3**. Probalo.

~hint ¡Contame más!
- Ahora el robot frena a 0,3 m (30 cm) de distancia.
- ¿Cuál sería una distancia segura para un robot real que trabaja cerca de personas?
hint~

```blocks
basic.forever(function () {
    // @highlight
    if (fwdSensors.sonar1.isPastThreshold(0.3, fwdEnums.OverUnder.Under)) {
        fwdMotors.stopDriving()
    }
})
```

## Modificar: paso 2

Probemos con un robot más rápido. En ``||fwdMotors:drive left 30 % right 30 %||``, cambiá los dos números por **50**. Probalo.

¿Sigue sobre la línea?

~hint ¡Contame más!
- Un robot más rápido puede pasarse de la línea antes de que los sensores se den cuenta.
- Probá varias velocidades. ¿Cuál es la más rápida con la que todavía sigue la línea?
hint~

```blocks
basic.forever(function () {
    if (fwdSensors.line2.isLineSensorState(fwdEnums.OnOff.On)) {
        // @highlight
        fwdMotors.tank(50, 50)
    }
})
```

## Modificar: paso 3

¿Tu robot pierde la línea en las curvas cerradas?

Hacé los giros **más cerrados**. Cambiá **0** por **-20** en los dos bloques de giro, para que una rueda vaya hacia atrás mientras la otra va hacia adelante.

~hint ¡Contame más!
- **left -20 % right 30 %** hace girar al robot hacia la izquierda más rápido.
- **left 30 % right -20 %** lo hace girar hacia la derecha más rápido.
- Los giros más cerrados ayudan en las curvas, pero pueden hacer que el robot se tambalee en las rectas. Probá hasta encontrar los mejores números.
hint~

```blocks
basic.forever(function () {
    if (fwdSensors.line1.isLineSensorState(fwdEnums.OnOff.On)) {
        // @highlight
        fwdMotors.tank(-20, 30)
    } else if (fwdSensors.line3.isLineSensorState(fwdEnums.OnOff.On)) {
        // @highlight
        fwdMotors.tank(30, -20)
    }
})
```

## Modificar: paso 4

Los robots de verdad avisan qué están haciendo. Vamos a mostrar una flecha en la micro:bit.

Abrí ``||basic:Básico||``. Agregá ``||basic:mostrar flecha||`` dentro de cada parte de los sensores de línea: **Norte** para ir derecho, **Oeste** para la izquierda y **Este** para la derecha.

~hint ¡Contame más!
- Ahora cualquiera que mire puede saber hacia dónde va a ir el robot.
hint~

```blocks
basic.forever(function () {
    if (fwdSensors.line2.isLineSensorState(fwdEnums.OnOff.On)) {
        fwdMotors.tank(30, 30)
        // @highlight
        basic.showArrow(ArrowNames.North)
    } else if (fwdSensors.line1.isLineSensorState(fwdEnums.OnOff.On)) {
        fwdMotors.tank(0, 30)
        // @highlight
        basic.showArrow(ArrowNames.West)
    } else if (fwdSensors.line3.isLineSensorState(fwdEnums.OnOff.On)) {
        fwdMotors.tank(30, 0)
        // @highlight
        basic.showArrow(ArrowNames.East)
    }
})
```

## ¡Hora del desafío! @showdialog

Ahora mismo, si algo bloquea la línea, tu robot se queda esperando para siempre.

**Desafío:** hacé que dé la vuelta y regrese por donde vino.

## Desafío: paso 1

Abrí ``||fwdMotors:Motores||``. Arrastrá ``||fwdMotors:turn right for 90 °||`` debajo de ``||fwdMotors:stop driving||``, en la parte del sonar. Cambiá **90** por **180**.

~hint ¡Contame más!
- **turn right** significa girar a la derecha.
- Los motores cuentan cuánto giran las ruedas, así que el robot puede girar una cantidad exacta de grados.
- **180°** es media vuelta, así que el robot queda mirando hacia el lado por donde vino.
hint~

```blocks
basic.forever(function () {
    if (fwdSensors.sonar1.isPastThreshold(0.3, fwdEnums.OverUnder.Under)) {
        fwdMotors.stopDriving()
        // @highlight
        fwdMotors.turnFor(FwdFifaTurn.Right, 180)
    }
})
```

## Desafío: paso 2

Agregá una espera corta antes del giro, para que las personas vean que el robot se detuvo.

Arrastrá ``||basic:pausa (ms)||`` entre ``||fwdMotors:stop driving||`` y el giro. Ponelo en **1000** ms (1 segundo).

```blocks
basic.forever(function () {
    if (fwdSensors.sonar1.isPastThreshold(0.3, fwdEnums.OverUnder.Under)) {
        fwdMotors.stopDriving()
        // @highlight
        basic.pause(1000)
        fwdMotors.turnFor(FwdFifaTurn.Right, 180)
    }
})
```

## Desafío: paso 3

Probá tu robot. Poné un obstáculo sobre la línea.

¿Frena, espera, da la vuelta y encuentra la línea otra vez? ¿Qué cambiarías?

## Punto de control: ¡Buen trabajo! @showdialog

¡Ahora tu robot puede resolver solo un camino bloqueado!

**Pensá:** ¿Qué otros problemas podría encontrar un robot de reparto de verdad?

Podés parar acá. O hacé clic en **Siguiente** para pasar a la **Parte 3: Crear**.

## Parte 3: Crear @showdialog

¡Ahora te toca inventar a vos!

**Desafío:** ¿Cómo podría tu robot ser más seguro, más rápido o más útil? Agregá tu propia idea al código.

Esta vez no hay pasos. Probá tus ideas, cambialas y volvé a probar. Hacé clic en la lamparita si necesitás ideas.

## Crear

Agregá tu propia idea a tu robot. Descargá y probá.

~hint ¿Necesitás ideas?
- **Ir más despacio cerca de obstáculos:** que el robot maneje más lento cuando hay algo a menos de 0,5 m, y que frene cuando está a menos de 0,15 m.
- **Paradas de reparto:** cuando el robot encuentre una línea que cruza (los tres sensores ven la línea), que se detenga 3 segundos y después siga.
- **Control de batería:** usá ``||fwdSensors:battery level||`` para mostrar un ícono de aviso cuando la batería esté baja.
- **Contador de vueltas:** contá cuántas veces el robot pasa por una línea que cruza, y mostrá el total cuando presiones **B**.
hint~

## Reflexión @showdialog

Pensá en tu proyecto:

- ¿Cuál fue un desafío? ¿Cómo lo resolviste?
- ¿Sobre qué te gustaría aprender más?

## ¡Terminaste! @showdialog

¡Excelente trabajo! Hacé clic en `|Listo|` para terminar el tutorial.
