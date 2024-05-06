# CP2Kotlin

##ListadeCompras/app/build.gradle.kts

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
