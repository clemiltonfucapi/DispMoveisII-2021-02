# Drawerlayout:
Link do projeto atual: [Clique aqui!](FirebaseApp-home.zip)
## Dependencias:
- Adicione as seguintes dependencias em ``build.gradle(app)``
```java
dependencies{
    .......
    //Material Design
    implementation 'com.google.android.material:material:1.2.0'

    //Rounded Image View
    implementation 'com.makeramen:roundedimageview:2.3.0'
    //Navigation component
    implementation 'androidx.navigation:navigation-fragment-ktx:2.2.0-rc03'
    implementation 'androidx.navigation:navigation-ui-ktx:2.2.0-rc03'
}
```
## Ícones
- Adicione os seguintes ícones na pasta ``res/drawable``
- ``ic_menu_24dp``:
    ```xml
    <vector android:height="24dp" android:tint="#FFFFFF"
        android:viewportHeight="24.0" android:viewportWidth="24.0"
        android:width="24dp" xmlns:android="http://schemas.android.com/apk/res/android">
        <path android:fillColor="#FF000000" android:pathData="M3,18h18v-2L3,16v2zM3,13h18v-2L3,11v2zM3,6v2h18L21,6L3,6z"/>
    </vector>
    ```
- ``ic_account_circle_black_24dp.xml``
    ```xml
    <vector xmlns:android="http://schemas.android.com/apk/res/android"
            android:width="24dp"
            android:height="24dp"
            android:viewportWidth="24.0"
            android:viewportHeight="24.0">
        <path
            android:fillColor="#FF000000"
            android:pathData="M12,2C6.48,2 2,6.48 2,12s4.48,10 10,10 10,-4.48 10,-10S17.52,2 12,2zM12,5c1.66,0 3,1.34 3,3s-1.34,3 -3,3 -3,-1.34 -3,-3 1.34,-3 3,-3zM12,19.2c-2.5,0 -4.71,-1.28 -6,-3.22 0.03,-1.99 4,-3.08 6,-3.08 1.99,0 5.97,1.09 6,3.08 -1.29,1.94 -3.5,3.22 -6,3.22z"/>
    </vector>
    ```

## Criando layout
- Neste tópico iremos criar um ``NavigationView`` que permite o "efeito gaveta" bem comum em apps:
- ![Images](imgs/nav_drawer.jpeg)
- Crie uma nova activity chamada ``NavigationActivity.java``. Nesta activity vamos desenhar a toolbar através do XML. Para isso devemos configurar a activity para nao mostrar a toolbar padrão:
    - Crie um novo estilo (``styles.xml``)
    ```xml
    ....
    <style name="NoActionBar" parent="Theme.AppCompat.Light.NoActionBar">
        <item name="colorPrimary">@color/colorPrimary</item>
        <item name="colorPrimaryDark">@color/colorPrimaryDark</item>
        <item name="colorAccent">@color/colorAccent</item>
    </style>
    ```
    - Em ``AndroidManifest.xml`` modifique:
    ```xml
    ....
    <activity android:name=".NavigationActivity"
        android:theme="@style/NoActionBar">
        <intent-filter>
            <action android:name="android.intent.action.MAIN" />
            <category android:name="android.intent.category.LAUNCHER" />
        </intent-filter>
    </activity>
    ....
    ``` 
- Crie o seguinte layout em activity_navigation.xml
    - ![](imgs/img01.png)
    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <androidx.drawerlayout.widget.DrawerLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".NavigationActivity"
        android:id="@+id/nav_drawerLayout"
        >
        <androidx.constraintlayout.widget.ConstraintLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            >
            <LinearLayout
                android:id="@+id/nav_toolbar"
                android:layout_width="0dp"
                android:layout_height="?actionBarSize"
                android:background="@color/colorPrimary"
                android:orientation="horizontal"
                android:paddingStart="15dp"
                android:paddingEnd="15dp"
                android:gravity="center_vertical"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintTop_toTopOf="parent"
                >
                <ImageView
                    android:id="@+id/navigation_icon"
                    android:layout_width="30dp"
                    android:layout_height="30dp"
                    android:src="@drawable/ic_menu_24dp"
                    />
                <TextView
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:layout_marginStart="15dp"
                    android:text="@string/app_name"
                    android:textColor="@android:color/white"
                    android:textSize="18sp"
                    android:textStyle="bold"
                    />
            </LinearLayout>
        </androidx.constraintlayout.widget.ConstraintLayout>
    </androidx.drawerlayout.widget.DrawerLayout>
    ```
    - DrawerLayout atua como um container que permite o efeito de "gaveta" interativas que são puxadas de uma ou de ambas as bordas verticais da janela. 
    - O posicionamento do DrawerLayout é controlado pelo atributo  ``android:layout_gravity`` no elemento filho, que define em qual posição a ``View`` irá surgir(esquerda ou direita)
- Crie uma nova pasta ``res/menu`` e um arquivo ``navigation_menu.xml``
    - ![](imgs/img02.png)
- Código do menu: ``navigation_menu.xml``
    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <menu xmlns:android="http://schemas.android.com/apk/res/android">
        <item
            android:id="@+id/nav_menu_main"
            android:title="Tela inicial" />
        <item
            android:id="@+id/nav_menu_lista_imagens"
            android:title="Lista de Imagens" />
        <item
            android:id="@+id/nav_menu_storage"
            android:title="Cadastro de Imagens" />
    </menu>
    ```
- Adicione a ``NavigationView`` no DrawerLayout. Ela deve ficar após o Constraint Layout
- ``activity_navigation.xml``:
    ```xml
    .....
        </androidx.constraintlayout.widget.ConstraintLayout>
        
        <com.google.android.material.navigation.NavigationView
            android:id="@+id/navigationView"
            android:layout_width="wrap_content"
            android:layout_height="match_parent"
            app:menu="@menu/navigation_menu"
            android:layout_gravity="start"
            />
        
    </androidx.drawerlayout.widget.DrawerLayout>
    ```
    - O valor ``layout_gravity="start"`` define que a navigation view virá da esquerda para direita. 
- Adicione um novo layout ``res/layout_nav_header.xml``:
    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        android:padding="20dp">
        <ImageView
            android:id="@+id/nav_header_img"
            android:layout_width="70dp"
            android:layout_height="70dp"
            android:src="@drawable/ic_account_circle_black_24dp"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent"
            />
        <View
            android:id="@+id/view"
            android:layout_width="1dp"
            android:layout_height="1dp"
            app:layout_constraintBottom_toBottomOf="@id/nav_header_img"
            app:layout_constraintEnd_toEndOf="@+id/nav_header_img"
            app:layout_constraintStart_toStartOf="@+id/nav_header_img"
            app:layout_constraintTop_toTopOf="@id/nav_header_img"
            />

        <TextView
            android:id="@+id/nav_header_nome"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:text="Nome Usuario"
            android:layout_marginStart="10dp"
            android:textSize="18sp"
            android:textStyle="bold"
            app:layout_constraintBottom_toTopOf="@+id/view"
            app:layout_constraintStart_toEndOf="@+id/nav_header_img" />

        <TextView
            android:id="@+id/nav_header_email"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:text="Email"
            android:layout_marginStart="10dp"
            android:textSize="16sp"
            android:textStyle="bold"
            app:layout_constraintTop_toBottomOf="@+id/nav_header_nome"
            app:layout_constraintStart_toEndOf="@+id/nav_header_img" />
        <LinearLayout
            android:layout_width="0dp"
            android:layout_height="0.1dp"
            android:layout_marginTop="8dp"
            android:background="#6E6A6A"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toBottomOf="@id/nav_header_img"
            />

    </androidx.constraintlayout.widget.ConstraintLayout>
    ```
    - Resultado: ![Image](imgs/img04.png)
- Em ``MainActivity.java`` adicione um evento de clique para a Navigation View aparecer ao clicar no botão de menu
    ```java
    public class NavigationActivity extends AppCompatActivity {
        private ImageView btnMenu;
        private DrawerLayout drawerLayout;
        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_navigation);

            btnMenu = findViewById(R.id.navigation_icon);
            drawerLayout = findViewById(R.id.nav_drawerLayout);

            btnMenu.setOnClickListener( view -> {
                drawerLayout.openDrawer(GravityCompat.START);
            });
        }
    }
    ```
    - Execute o app. Ele deve ficar da seguinte maneira:
    - ![](imgs/img03.png)
# Adicionando Fragments
- Vamos adicionar 3 Fragments() no projeto: 
    - New > Fragments > Fragment(List)
    - ![Image](imgs/img05.png)
    - Modifique os TextView's de cada layout de fragment.
    - ``fragment_main.xml``:
    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".fragment.MainFragment">
        <!-- TODO: Update blank fragment layout -->
        <TextView
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:text="MAIN" />
    </FrameLayout>
    ```
    - ``fragment_storage.xml``
    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".fragment.StorageFragment">
        <!-- TODO: Update blank fragment layout -->
        <TextView
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:text="STORAGE" />
    </FrameLayout>
    ```    
    - ``fragment_uploads.xml``
    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        tools:context=".fragment.UploadsFragment">
        
        <TextView
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:text="UPLOADS" />
    </FrameLayout>
    ```
# Navigation
- O Navigation é um componente que faz parte do Jetpack.
- O Navigation consiste de três partes principais:
    - NavGraph: é um XML que centraliza as informações de navegação de uma feature.
    - NavHost: é um contêiner vazio que mostra destinos do gráfico de navegação. O componente de navegação contém uma implementação NavHostpadrão, NavHostFragment, que mostra os destinos do fragmento.
    - NavController: é um objeto que gerencia a navegação do aplicativo em um NavHost. O NavController organiza a troca do conteúdo de destino no NavHost conforme os usuários se movem pelo aplicativo.
- Fonte: https://movile.blog/como-usar-o-jetpack-navigation-em-projetos-de-varios-modulos/ 
- Documentação: https://developer.android.com/guide/navigation
# NavGraph, NavHost e NavController
- Adicione um ``NavHostFragment`` em ``activity_navigation.xml``. Este componente será utilizado para receber as diferentes fragments selecionadas
- ``activity_navigation.xml``
    ```xml
    .....
            </LinearLayout>
            <!-- ADICIONE AQUI!!! -->
            <fragment
                android:layout_width="match_parent"
                android:layout_height="0dp"
                android:id="@+id/nav_host_fragment"
                android:name="androidx.navigation.fragment.NavHostFragment"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintTop_toBottomOf="@+id/nav_toolbar"
                app:navGraph="@navigation/nav_graph"
                />
            <!-- ********************** -->
        </androidx.constraintlayout.widget.ConstraintLayout>
        <com.google.android.material.navigation.NavigationView
            android:id="@+id/nav_navigationView"
            android:layout_width="wrap_content"
            android:layout_height="match_parent"
            app:menu="@menu/navigation_menu"
            app:headerLayout="@layout/layout_nav_header"
            android:layout_gravity="start"
        />
    </androidx.drawerlayout.widget.DrawerLayout>
    ```
- Adicione um nova pasta em ``res/navigation`` com o arquivo ``nav_graph.xml``.
    - ![](imgs/img06.png)
- Neste arquivo vamos criar uma lista de nós do tipo ``<fragment>`` onde irá representar cada ``Fragment`` criada.
- Os ``id's`` de cada ``<fragment>`` deve ser igual ao dos itens de menu(``navigation_menu.xml``)
- ``nav_graph.xml``:
    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <navigation xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools"
        android:id="@+id/nav_graph"
        app:startDestination="@id/nav_menu_main">

        <fragment
            android:id="@+id/nav_menu_main"
            android:name="com.clemilton.firebaseappsala.fragment.MainFragment"
            tools:layout="@layout/fragment_main"
            />
        <fragment
            android:id="@+id/nav_menu_lista_imagens"
            tools:layout="@layout/fragment_uploads"
            android:name="com.clemilton.firebaseappsala.fragment.UploadsFragment"
            />
        <fragment
            android:id="@+id/nav_menu_storage"
            tools:layout="@layout/fragment_storage"
            android:name="com.clemilton.firebaseappsala.fragment.StorageFragment"
            />
    </navigation>
    ```

- Agora vamos criar um ``NavController`` que permite a navegação pelas fragments
```java
public class NavigationActivity extends AppCompatActivity {
    ......
    btnMenu.setOnClickListener( view -> {
        drawerLayout.openDrawer(GravityCompat.START);
    });

    //Navigation View Menu
    NavigationView navigationView = findViewById(R.id.nav_navigationView);
    
    //NavController
    NavController navController = Navigation.findNavController(this,R.id.nav_host_fragment);

    // Configura um NavigationView para usar como NavController
    NavigationUI.setupWithNavController(navigationView,navController);
}
```
# StorageFragment
- Vamos configurar o StorageFragment com as mesmas funcionalidades de StorageActivity.java
- Copie o Layout de ``activity_storage.xml`` para ``fragment_storage.xml``
```xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".fragment.StorageFragment">
    <androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        >
        <ImageView
            android:id="@+id/storage_image_cel"
            android:layout_width="300dp"
            android:layout_height="200dp"
            android:layout_marginTop="32dp"
            android:src="@drawable/celular"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/storage_edit_nome" />
        <Button
            android:id="@+id/storage_btn_upload"
            style="@style/FormStyle"
            android:layout_marginTop="24dp"
            android:text="Upload"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/storage_image_cel" />
        <EditText
            android:id="@+id/storage_edit_nome"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_marginStart="16dp"
            android:layout_marginTop="32dp"
            android:layout_marginEnd="16dp"
            android:ems="10"
            android:hint="Digite o nome da imagem"
            android:inputType="textPersonName"
            app:layout_constraintEnd_toStartOf="@+id/storage_btn_galeria"
            app:layout_constraintHorizontal_bias="0.5"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent" />
        <ImageButton
            android:id="@+id/storage_btn_galeria"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:src="@drawable/ic_gallery_24dp"
            app:layout_constraintEnd_toStartOf="@+id/storage_btn_camera"
            app:layout_constraintHorizontal_bias="0.5"
            app:layout_constraintStart_toEndOf="@+id/storage_edit_nome"
            app:layout_constraintTop_toTopOf="@+id/storage_edit_nome" />
        <ImageButton
            android:id="@+id/storage_btn_camera"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginEnd="16dp"
            android:src="@drawable/ic_camera_24dp"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintHorizontal_bias="0.5"
            app:layout_constraintStart_toEndOf="@+id/storage_btn_galeria"
            app:layout_constraintTop_toTopOf="@+id/storage_btn_galeria" />

    </androidx.constraintlayout.widget.ConstraintLayout>
</FrameLayout>
```