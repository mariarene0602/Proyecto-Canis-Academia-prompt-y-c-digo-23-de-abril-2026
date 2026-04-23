Este es el plan maestro para tu proyecto **CRUDScanisAcademia**. Como tu colaborador de software, he estructurado este plan para que sea ejecutable, escalable y profesional.

---

## 1. Estructura y Configuración Inicial

Para mantener el orden, sigue esta jerarquía en tu entorno de desarrollo:

* `xfluttermaria0602/` (Carpeta raíz)
    * `crudscanisacademia/` (Proyecto Flutter)

### Configuración de `pubspec.yaml`
Para conectar Firebase con Flutter, añade estas dependencias en tu archivo `pubspec.yaml`:

```yaml
dependencies:
  flutter:
    sdk: flutter
  firebase_core: ^3.0.0
  cloud_firestore: ^5.0.0
```
*Ejecuta `flutter pub get` en la terminal para instalarlas.*

---

## 2. Metodología de Agentes y Roles (Arquitectura)

Para gestionar este proyecto, definiremos los siguientes roles de software:

| Rol | Responsabilidad |
| :--- | :--- |
| **Arquitecto de Datos** | Define la estructura de Firestore (Colección: `cursos`). |
| **Ingeniero UI/UX** | Diseña los Widgets con paleta de colores moderna. |
| **DevOps Firebase** | Configura `firebase_options.dart` y reglas de seguridad. |

### Flujo de Trabajo (Pipeline)
1. **Init:** Configuración de Firebase console.
2. **Data Layer:** Modelo de datos `Curso`.
3. **Service Layer:** Métodos CRUD (FireStore).
4. **UI Layer:** Widgets con temas visuales.

---

## 3. Implementación: Modelo y CRUD (Código Dart)

### Modelo: `curso_model.dart`
```dart
class Curso {
  final String id;
  final String nombre;
  final double precio;
  final String duracion;

  Curso({required this.id, required this.nombre, required this.precio, required this.duracion});
}
```

### Servicio: `curso_service.dart`
```dart
import 'package:cloud_firestore/cloud_firestore.dart';

class CursoService {
  final CollectionReference _db = FirebaseFirestore.instance.collection('Cursos');

  // CREAR
  Future<void> addCurso(String nombre, double precio, String duracion) => 
      _db.add({'nombre': nombre, 'precio': precio, 'duracion': duracion});

  // LEER
  Stream<QuerySnapshot> getCursos() => _db.snapshots();

  // ACTUALIZAR
  Future<void> updateCurso(String id, String nombre, double precio, String duracion) =>
      _db.doc(id).update({'nombre': nombre, 'precio': precio, 'duracion': duracion});

  // BORRAR
  Future<void> deleteCurso(String id) => _db.doc(id).delete();
}
```

---

## 4. UI: Pantalla Principal con Colores Atractivos

Utilizaremos una paleta vibrante: `#6200EE` (Primario) y `#03DAC6` (Acento).

```dart
import 'package:flutter/material.dart';

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text("ScanisAcademia"),
        backgroundColor: Color(0xFF6200EE),
      ),
      floatingActionButton: FloatingActionButton(
        backgroundColor: Color(0xFF03DAC6),
        child: Icon(Icons.add),
        onPressed: () => _mostrarDialogo(context),
      ),
      body: _buildListaCursos(),
    );
  }
}
```

---

## 5. Práctica Guiada con "Antigravity"

El concepto de **Antigravity** en desarrollo implica desacoplar la lógica de la UI para que tu aplicación "flote" sin dependencias rígidas.

### Pasos para el estudiante:
1.  **Entorno:** Crea tu proyecto usando `flutter create crudscanisacademia`.
2.  **Firebase:** Ve a [Firebase Console](https://console.firebase.google.com/), crea el proyecto, registra la app y descarga `google-services.json` (Android) o `GoogleService-Info.plist` (iOS).
3.  **Integración:** Coloca el archivo en `android/app/` o `ios/Runner/`.
4.  **Inicialización:** En `main.dart`, asegúrate de inicializar:
    ```dart
    await Firebase.initializeApp(options: DefaultFirebaseOptions.currentPlatform);
    ```
5.  **Refactor:** Separa tus archivos en `lib/models`, `lib/services`, y `lib/screens` para mantener el código "ligero".

---

## Resumen de Estructura de Carpetas

```text
crudscanisacademia/
├── lib/
│   ├── main.dart
│   ├── models/        # curso_model.dart
│   ├── services/      # curso_service.dart
│   └── screens/       # home_screen.dart
├── android/
├── ios/
└── pubspec.yaml
```

¿Te gustaría que profundizáramos en cómo implementar las **reglas de seguridad de Firestore** para proteger tus datos de la academia, o prefieres que generemos los archivos con la interfaz gráfica completa?
