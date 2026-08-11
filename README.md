# Actor Model + Serverless Prototype

Proyecto académico desarrollado para la **Actividad Semana 14: Modelo de Actores y Arquitecturas Serverless**.

## Descripción

Este proyecto implementa un prototipo del **Modelo de Actores** utilizando Python y la biblioteca **Pykka**.

La arquitectura incluye:

* `WorkerActor`: procesa las tareas recibidas.
* `SupervisorActor`: administra al Worker y lo reinicia cuando ocurre un error.
* `lambda_handler`: simula el punto de entrada de una función serverless.

## Funcionamiento

El flujo principal es:

```text
Request JSON
    ↓
lambda_handler
    ↓
SupervisorActor
    ↓
WorkerActor
    ↓
Respuesta JSON
```

El Worker recibe un texto y lo transforma a mayúsculas.

Ejemplo:

```python
lambda_handler({"payload": "hola mundo"})
```

Resultado:

```json
{
  "status": "success",
  "result": "HOLA MUNDO",
  "worker_id": 1
}
```

## Tolerancia a fallos

Si el Worker recibe:

```python
{"payload": "FAIL"}
```

se genera intencionalmente una excepción.

El `SupervisorActor` detecta el fallo, detiene el Worker anterior y crea uno nuevo automáticamente, demostrando un mecanismo básico de **supervisión y recuperación ante errores**.

## Tecnologías

* Python
* Pykka
* Google Colab / Jupyter Notebook
* JSON
* Logging

## Ejecución

Instalar Pykka:

```bash
pip install pykka
```

Después, ejecutar las celdas del notebook en orden.

## Limitaciones

Este proyecto es un prototipo académico. La función `lambda_handler` representa el funcionamiento de una función serverless, pero el notebook no incluye un despliegue real en AWS Lambda, Google Cloud Functions o Azure Functions.

## Conclusión

El proyecto demuestra conceptos básicos del **Modelo de Actores**, como comunicación mediante mensajes, aislamiento, supervisión y recuperación ante fallos, además de su posible integración con una arquitectura serverless.
