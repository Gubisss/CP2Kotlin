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

## ListadeCompras/app/src/main/java/carreiras/com/github/listadecompras/ItemsAdapter.kt

package carreiras.com.github.listadecompras

import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.TextView
import androidx.recyclerview.widget.RecyclerView

// Classe que define o adaptador para o RecyclerView
class ItemsAdapter : RecyclerView.Adapter<ItemsAdapter.ItemViewHolder>() {

    // Lista de itens que serão exibidos no RecyclerView
    private val items = mutableListOf<ItemModel>()

    // Método para adicionar um novo item à lista e notificar o RecyclerView sobre a mudança
    fun addItem(newItem: ItemModel) {
        items.add(newItem)
        notifyDataSetChanged()
    }

    // Método chamado quando o RecyclerView precisa de uma nova ViewHolder para exibir um item
    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ItemViewHolder {
        // Infla o layout do item a partir do XML usando LayoutInflater
        val view = LayoutInflater.from(parent.context).inflate(R.layout.item_layout, parent, false)
        // Retorna uma nova instância de ItemViewHolder com a View inflada
        return ItemViewHolder(view)
    }

    // Método que retorna o número total de itens na lista
    override fun getItemCount(): Int = items.size

    // Método chamado pelo RecyclerView para exibir dados em uma posição específica
    override fun onBindViewHolder(holder: ItemViewHolder, position: Int) {
        // Obtém o item da posição fornecida
        val item = items[position]
        // Liga os dados do item ao ViewHolder
        holder.bind(item)
    }

    // Classe interna que representa a ViewHolder para exibir cada item no RecyclerView
    class ItemViewHolder(view: View) : RecyclerView.ViewHolder(view) {
        // Referência ao TextView dentro do layout do item
        val textView = view.findViewById<TextView>(R.id.textViewItem)

        // Método para ligar os dados do item ao TextView
        fun bind(item: ItemModel) {
            textView.text = item.name
        }
    }
}

## ListadeCompras/app/src/main/java/carreiras/com/github/listadecompras/MainActivity.kt

package carreiras.com.github.listadecompras 

import android.annotation.SuppressLint 
import android.os.Bundle 
import android.widget.Button 
import android.widget.EditText 
import androidx.activity.ComponentActivity 
import androidx.recyclerview.widget.RecyclerView 

// Define a classe MainActivity que herda de ComponentActivity
class MainActivity : ComponentActivity() { 
    // Anotação para remover o aviso de falta de ID inflado
    @SuppressLint("MissingInflatedId") 
    // Função de criação da atividade
    override fun onCreate(savedInstanceState: Bundle?) { 
    // Chama a implementação da função onCreate na superclasse
        super.onCreate(savedInstanceState) 

    // Define o layout da atividade a partir do arquivo XML activity_main, que está em res>layout>activity_main
        setContentView(R.layout.activity_main) 

    // Encontra o RecyclerView no layout, que está em res>id>recyclerView
        val recyclerView = findViewById<RecyclerView>(R.id.recyclerView); 
    // Cria uma instância do ItemsAdapter
        val itemsAdapter = ItemsAdapter() 
    // Define o adapter para o RecyclerView
        recyclerView.adapter = itemsAdapter 

    // Encontra o Button no layout, que está em res>id>button
        val button = findViewById<Button>(R.id.button) 
    // Encontra o EditText no layout, que está em res>id>editText
        val editText = findViewById<EditText>(R.id.editText) 

    // Define o click listener para o botão
        button.setOnClickListener { 
    // Cria o objeto ItemModel
            val item = ItemModel( 
        // Define o nome do item baseando-se no texto no EditText
                name = editText.text.toString() 
            )

    // Adiciona o item ao adapter
            itemsAdapter.addItem(item) 
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

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
//layout_width: largura do layout, definida como 'match_parent' para preencher a largura do pai.
    android:layout_width="match_parent"
//layout_height: altura do layout, definida como '?android:attr/listPreferredItemHeight' para corresponder à altura preferencial de itens de lista do sistema.
    android:layout_height="?android:attr/listPreferredItemHeight"
 //gravity: alinhamento vertical do conteúdo dentro do layout, definido como 'center_vertical' para centralizar o conteúdo verticalmente.
    android:gravity="center_vertical"
//padding: preenchimento do layout, definido como '8dp' para adicionar 8 pixels de preenchimento em todas as direções.
    android:padding="8dp">
    <TextView
       //id: identificador único do TextView.
        android:id="@+id/textViewItem"
       //layout_width: largura do TextView, definida como 'wrap_content'      para ajustar a largura ao conteúdo do texto.
        android:layout_width="wrap_content"
       //layout_height: altura do TextView, definida como 'wrap_content' para ajustar a altura ao conteúdo do texto.
         android:layout_height="wrap_content"
        //textSize: tamanho do texto, definido como '18sp' para 18 unidades de escala independente de pixel.
        android:textSize="18sp"
//textStyle: estilo do texto, definido como 'bold' para tornar o texto em negrito.
        android:textStyle="bold"
//tools:text: texto de exemplo usado apenas durante a pré-visualização do layout no Android Studio, definido como "Novo    Item"./
  tools:text="Novo    Item" />

</LinearLayout>
