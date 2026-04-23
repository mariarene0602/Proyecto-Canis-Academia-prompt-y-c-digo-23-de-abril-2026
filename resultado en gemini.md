Para elevar tu proyecto **CRUDScanisAcademia** a un nivel profesional, he diseñado una metodología de desarrollo modular. Este enfoque asegura que tu código sea mantenible, escalable y visualmente atractivo.

---

## 1. Roadmap del Proyecto (Entorno Profesional)

### Configuración de Estructura
En tu terminal:
```bash
mkdir xfluttermaria0602
cd xfluttermaria0602
flutter create crudscanisacademia
cd crudscanisacademia
```

### Integración de Librerías (`pubspec.yaml`)
Añade las dependencias necesarias:
```yaml
dependencies:
  flutter:
    sdk: flutter
  firebase_core: ^3.0.0
  cloud_firestore: ^5.0.0
  google_fonts: ^6.1.0 # Para tipografía moderna
```
*Ejecuta `flutter pub get` después de guardar.*

---

## 2. Metodología de Agentes y Roles (Arquitectura)

Para gestionar este proyecto, definiremos los siguientes agentes:

| Agente | Habilidad (Skill) | Responsabilidad |
| :--- | :--- | :--- |
| **Arquitecto de Datos** | Firebase Firestore Logic | Modelado de la colección `Cursos`. |
| **Ingeniero UI/UX** | Flutter Material Design | Creación de widgets con paleta `Deep Purple` y `Teal`. |
| **DevOps Specialist** | Firebase CLI / Config | Gestión de `google-services.json` y flujo de CI/CD. |

### Flujo de Trabajo (Antigravity Approach)
El principio *Antigravity* aquí significa desacoplar la lógica de Firebase del árbol de widgets, permitiendo que la UI "flote" independientemente de la fuente de datos.

---

## 3. Implementación del CRUD (Archivos Clave)

### `lib/models/curso_model.dart`
```dart
class Curso {
  final String id;
  final String nombre;
  final double precio;
  final String duracion;

  Curso({required this.id, required this.nombre, required this.precio, required this.duracion});

  factory Curso.fromFirestore(Map<String, dynamic> data, String id) {
    return Curso(
      id: id,
      nombre: data['nombre'] ?? '',
      precio: (data['precio'] ?? 0).toDouble(),
      duracion: data['duracion'] ?? '',
    );
  }
}
```

### `lib/services/firestore_service.dart`
```dart
import 'package:cloud_firestore/cloud_firestore.dart';
import '../models/curso_model.dart';

class FirestoreService {
  final CollectionReference _cursosRef = FirebaseFirestore.instance.collection('Cursos');

  // CREAR
  Future<void> addCurso(String nombre, double precio, String duracion) =>
      _cursosRef.add({'nombre': nombre, 'precio': precio, 'duracion': duracion});

  // LEER (Stream para actualización en tiempo real)
  Stream<List<Curso>> getCursos() {
    return _cursosRef.snapshots().map((snapshot) => snapshot.docs
        .map((doc) => Curso.fromFirestore(doc.data() as Map<String, dynamic>, doc.id))
        .toList());
  }

  // ACTUALIZAR
  Future<void> updateCurso(String id, String nombre, double precio, String duracion) =>
      _cursosRef.doc(id).update({'nombre': nombre, 'precio': precio, 'duracion': duracion});

  // BORRAR
  Future<void> deleteCurso(String id) => _cursosRef.doc(id).delete();
}
```

---

## 4. UI: Pantalla Principal (Colores Atractivos)

Utiliza un diseño limpio con `ThemeData` para una experiencia de usuario superior.

```dart
// Fragmento de UI para la lista
ListView.builder(
  itemCount: cursos.length,
  itemBuilder: (context, index) {
    final curso = cursos[index];
    return Card(
      elevation: 4,
      margin: EdgeInsets.symmetric(horizontal: 10, vertical: 6),
      color: Colors.white,
      child: ListTile(
        leading: CircleAvatar(backgroundColor: Colors.tealAccent, child: Icon(Icons.book, color: Colors.black)),
        title: Text(curso.nombre, style: TextStyle(fontWeight: FontWeight.bold, color: Colors.deepPurple)),
        subtitle: Text("Precio: \$${curso.precio} | Duración: ${curso.duracion}"),
        trailing: IconButton(icon: Icon(Icons.delete, color: Colors.red), onPressed: () => service.deleteCurso(curso.id)),
      ),
    );
  },
)
```



---

## 5. Práctica Guiada: Metodología Paso a Paso para Estudiantes

1.  **Init Firebase:** Configura el proyecto en la consola, activa *Firestore* en modo prueba.
2.  **Config:** Ejecuta `flutterfire configure` para generar automáticamente los archivos de inicialización (es la forma más rápida y segura).
3.  **Modelar:** Define tu objeto `Curso`.
4.  **Conectar:** Implementa el `FirestoreService`.
5.  **Visualizar:** Usa `StreamBuilder` en tu pantalla principal para escuchar los cambios en tiempo real sin recargar la pantalla.

---

**Resumen de la estructura de archivos sugerida:**
* `lib/`
    * `main.dart` (Configuración inicial)
    * `models/curso_model.dart`
    * `services/firestore_service.dart`
    * `screens/home_screen.dart` (UI)

¿Te gustaría que generemos el código completo del `main.dart` con la inicialización de Firebase incluida, o prefieres que trabajemos en el diseño del formulario para añadir los cursos?
