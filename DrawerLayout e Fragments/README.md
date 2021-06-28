# Drawerlayout:
Link do projeto atual: [Clique aqui!](FirebaseApp-home.zip)
## Dependencias:
- Adicione as seguintes dependencias em ``build.gradle(app)```
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
- Crie uma nova activity chamada NavigationActivity.java
- 