# CP2Kotlin

## ListadeCompras/app/build.gradle.kts

plugins {
    // Plugin para aplicativo Android
    id("com.android.application")
    // Plugin para suporte ao Kotlin
    id("org.jetbrains.kotlin.android")
}

android {
    // Namespace do aplicativo
    namespace = "carreiras.com.github.listadecompras"
    // Versão do SDK de compilação
    compileSdk = 34

    defaultConfig {
        // ID do aplicativo
        applicationId = "carreiras.com.github.listadecompras"
        // Versão mínima do Android suportada
        minSdk = 27
        // Versão de destino do Android
        targetSdk = 34
        // Número da versão do aplicativo
        versionCode = 1
        // Nome da versão do aplicativo
        versionName = "1.0"
        // Runner para testes instrumentados
        testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"
        // Configuração para usar bibliotecas de suporte para vetores
        vectorDrawables {
            useSupportLibrary = true
        }
    }

    buildTypes {
        release {
            // Minificação desabilitada
            isMinifyEnabled = false
            // Arquivos de configuração do ProGuard
            proguardFiles(
                getDefaultProguardFile("proguard-android-optimize.txt"),
                "proguard-rules.pro"
            )
        }
    }

    compileOptions {
        // Versão do Java usada
        sourceCompatibility = JavaVersion.VERSION_1_8
        targetCompatibility = JavaVersion.VERSION_1_8
    }

    kotlinOptions {
        // Versão do bytecode JVM gerado pelo Kotlin
        jvmTarget = "1.8"
    }

    buildFeatures {
        // Habilita recursos do Jetpack Compose
        compose = true
    }

    composeOptions {
        // Versão da extensão do compilador Kotlin para Compose
        kotlinCompilerExtensionVersion = "1.5.1"
    }

    packaging {
        resources {
            // Exclui arquivos de licença do pacote final
            excludes += "/META-INF/{AL2.0,LGPL2.1}"
        }
    }
}

## ListadeCompras/app/src/main/res/layout/activity_main.xml

<?xml version="1.0" encoding="utf-8"?>
<!-- Declaração de propriedades do XML -->
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto" <!-- Declaração do namespace para atributos definidos pelo aplicativo -->
    xmlns:tools="http://schemas.android.com/tools" <!-- Declaração do namespace para atributos específicos da ferramenta -->
    android:layout_width="match_parent" <!-- Largura do layout igual à largura do elemento pai -->
    android:layout_height="match_parent" <!-- Altura do layout igual à altura do elemento do pai -->
    android:orientation="vertical" <!-- Orientação vertical para que os elementos fiquem igual uma coluna -->
    android:padding="16dp" <!-- Preenchimento de 16dp em todas as direções -->
    tools:context=".MainActivity"> <!-- Contexto da ferramenta -->

    <!-- Campo para entrada de texto -->
    <EditText
        android:id="@+id/editText" <!-- ID exclusivo para que possamos usar no código Java -->
        android:layout_width="match_parent" <!-- Largura total -->
        android:layout_height="wrap_content" <!-- Altura variável conforme o conteúdo -->
        android:hint="Nome do produto" /> <!-- Texto exibido apenas no preview -->

    <!-- Botão -->
    <Button
        android:id="@+id/button" <!-- ID exclusivo para que possamos usar no código Java -->
        android:layout_width="match_parent" <!-- Largura total -->
        android:layout_height="wrap_content" <!-- Altura variável conforme o conteúdo -->
        android:text="inserir" /> <!-- Texto exibido apenas no preview -->

    <!-- RecyclerView para exibição de uma lista de itens -->
    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/recyclerView" <!-- ID exclusivo para que possamos usar no código Java -->
        android:layout_width="wrap_content" <!-- Largura total -->
        android:layout_height="wrap_content" <!-- Altura variável conforme o conteúdo -->
        app:layoutManager="androidx.recyclerview.widget.LinearLayoutManager" /> <!-- Gerenciador de layout para o RecyclerView -->
</LinearLayout>

## ListadeCompras/app/src/main/res/layout/item_layout.xml

/
 
Esta classe representa um item de lista em um layout LinearLayout.*/
class ListItemView : View {

    /
     
O TextView que exibe o texto do item.*/
  private val textViewItem: TextView

    /
     
Construtor da classe ListItemView.*
@param context O contexto da aplicação.*/
constructor(context: Context) : super(context) {// Inicializa o TextView
    textViewItem = findViewById(R.id.textViewItem)}

    /
     
Define o texto do item.*
@param text O texto a ser exibido.*/
fun setText(text: String) {
    textViewItem.text = text}
}
