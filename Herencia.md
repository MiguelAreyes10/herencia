# ==============================================================
# Actividad: Extensión de aplicación usando Herencia
# Asignatura: Programación Orientada a Objetos
# Descripción: Se define una clase base y dos subclases que heredan,
# reutilizan, sobrescriben y amplían funcionalidades.
# ==============================================================

# ------------------------------
# Clase Base: Aplicacion
# Contiene atributos y métodos comunes a cualquier aplicación
# ------------------------------
class Aplicacion:
    """Clase base que representa una aplicación genérica"""
    
    def __init__(self, nombre, version, desarrollador):
        """Constructor de la clase base
        Args:
            nombre (str): Nombre de la aplicación
            version (str): Versión actual
            desarrollador (str): Autor o empresa creadora
        """
        # Atributos comunes a todas las aplicaciones
        self.nombre = nombre
        self.version = version
        self.desarrollador = desarrollador
        self.estado = "Inactiva"  # Valor por defecto

    def iniciar(self):
        """Método común: cambia el estado a Activa"""
        self.estado = "Activa"
        return f"✅ {self.nombre} ha iniciado correctamente."

    def cerrar(self):
        """Método común: cambia el estado a Inactiva"""
        self.estado = "Inactiva"
        return f"❌ {self.nombre} se ha cerrado."

    def mostrar_informacion(self):
        """Método común: devuelve datos básicos de la app"""
        return (
            f"📦 Nombre: {self.nombre}\n"
            f"🔢 Versión: {self.version}\n"
            f"👤 Desarrollador: {self.desarrollador}\n"
            f"🔌 Estado: {self.estado}"
        )


# ------------------------------
# Subclase: AplicacionMovil
# Hereda de Aplicacion → reutiliza sus atributos y métodos
# Agrega atributo propio: plataforma
# ------------------------------
class AplicacionMovil(Aplicacion):
    """Subclase para aplicaciones móviles, hereda de Aplicacion"""
    
    def __init__(self, nombre, version, desarrollador, plataforma):
        """Constructor de la subclase: llama al constructor de la clase base
        y agrega un atributo exclusivo de aplicaciones móviles
        """
        # Llamada al método __init__ de la clase base para reutilizar código
        super().__init__(nombre, version, desarrollador)
        # Atributo exclusivo de esta subclase
        self.plataforma = plataforma  # Ej: "Android", "iOS"

    def mostrar_informacion(self):
        """Sobreescritura del método de la clase base: amplía la información"""
        info_base = super().mostrar_informacion()  # Reutiliza el método original
        return f"{info_base}\n📱 Plataforma: {self.plataforma}"

    def notificar_usuario(self, mensaje):
        """Método EXCLUSIVO de AplicacionMovil: envía notificación"""
        return f"🔔 Notificación en {self.plataforma}: {mensaje}"


# ------------------------------
# Subclase: AplicacionEscritorio
# Hereda de Aplicacion → reutiliza, sobrescribe y agrega funcionalidad
# ------------------------------
class AplicacionEscritorio(Aplicacion):
    """Subclase para aplicaciones de escritorio, hereda de Aplicacion"""
    
    def __init__(self, nombre, version, desarrollador, sistema_operativo):
        """Constructor: reutiliza la clase base y agrega atributo propio"""
        super().__init__(nombre, version, desarrollador)
        self.sistema_operativo = sistema_operativo  # Ej: "Windows", "macOS"

    def iniciar(self):
        """Sobreescritura TOTAL del método iniciar de la clase base"""
        self.estado = "Activa (en ventana)"
        return f"🖥️ {self.nombre} abierta en {self.sistema_operativo}."

    def realizar_actualizacion(self, nueva_version):
        """Método EXCLUSIVO: gestiona la actualización de la app de escritorio"""
        version_anterior = self.version
        self.version = nueva_version
        return (
            f"🔄 Actualizando {self.nombre}: "
            f"v{version_anterior} → v{self.version} en {self.sistema_operativo}"
        )


# ------------------------------
# Programa Principal: Instanciación y pruebas
# ------------------------------
if __name__ == "__main__":
    print("=" * 50)
    print("PRUEBA DE HERENCIA EN APLICACIONES")
    print("=" * 50)

    # Instancia de la subclase AplicacionMovil
    app_movil = AplicacionMovil(
        nombre="App Finanzas",
        version="2.1.0",
        desarrollador="Estudiante POO",
        plataforma="Android"
    )
    print("\n--- Aplicación Móvil ---")
    print(app_movil.iniciar())          # Heredado de la clase base
    print(app_movil.mostrar_informacion())  # Sobreescrito
    print(app_movil.notificar_usuario("Tu saldo ha sido actualizado"))  # Exclusivo
    print(app_movil.cerrar())           # Heredado

    # Instancia de la subclase AplicacionEscritorio
    app_escritorio = AplicacionEscritorio(
        nombre="Editor de Proyectos",
        version="1.5.2",
        desarrollador="Equipo Desarrollo",
        sistema_operativo="Windows 11"
    )
    print("\n--- Aplicación de Escritorio ---")
    print(app_escritorio.iniciar())      # Sobreescrito
    print(app_escritorio.mostrar_informacion())  # Heredado
    print(app_escritorio.realizar_actualizacion("1.6.0"))  # Exclusivo
    print(app_escritorio.cerrar())       # Heredado

    print("\n✅ Todas las pruebas finalizadas — Herencia aplicada correctamente.")
