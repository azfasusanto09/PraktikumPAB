# Tugas Praktikum 4: Android Beginner 2

## Kelompok 5:
1. Azfa Rahma Putra Susanto (L0324008)
2. Hammam Ibnu Adi'Abdillah (L0324015)
3. Indra Fata Azhari L0324017)

## Source Code yang digunakan:

###
1. MainActivity.kt:
   ~~~kt
   package com.example.josparcoffee

    import android.os.Bundle
    import androidx.activity.ComponentActivity
    import androidx.activity.compose.setContent
    import com.example.josparcoffee.navigation.AppNavigation

    class MainActivity : ComponentActivity() {
        override fun onCreate(savedInstanceState: Bundle?) {
            super.onCreate(savedInstanceState)

            setContent {
                AppNavigation()
            }
        }
    }


2. AppNavigation.kt:
   ~~~kt
   package com.example.josparcoffee.navigation

    import androidx.compose.runtime.Composable
    import androidx.navigation.compose.*
    import com.example.josparcoffee.ui.screen.home.HomeScreen
    import com.example.josparcoffee.ui.screen.menu.MenuScreen
    import com.example.josparcoffee.ui.screen.profile.ProfileScreen

    @Composable
    fun AppNavigation() {

       val navController = rememberNavController()

        NavHost(navController = navController, startDestination = "home") {

            composable("home") {
                HomeScreen(navController)
            }

            composable("menu") {
                MenuScreen(navController)
            }

            composable("profile") {
                ProfileScreen()
            }
        }
    }


3. Coffee.kt:
   ~~~kt
    package com.example.josparcoffee.data

    import com.example.josparcoffee.R

    data class MenuItem(
      val name: String,
      val price: String?,
      val priceHot: String?,
      val priceIce: String?,
      val category: String?,
      val imageRes: Int
    )

      val menuList = listOf(
      
          // Coffee Based
          MenuItem("Cappuccino", null ,"22", "20", "Coffee", R.drawable.cappuccino),
          MenuItem("Americano", null ,"18", "17", "Coffee",R.drawable.americano),
          MenuItem("Mochaccino", null ,"22", "20", "Coffee",R.drawable.mochaccino),
          MenuItem("Caramel Latte",null ,"20", "20", "Coffee",R.drawable.caramel_latte),
          MenuItem("Vanilla Latte", null ,"20", "20", "Coffee",R.drawable.vanilla_latte),
      
          // Milk Based
          MenuItem("Chocolate", null ,"19", "17", "Milk",R.drawable.chocolate),
          MenuItem("Matcha", null ,"19", "17", "Milk",R.drawable.matcha),
          MenuItem("Milo Dino Favorito",null ,"19", "17", "Milk",R.drawable.milo),
          MenuItem("Red Velvet", null ,"19", "17", "Milk",R.drawable.redvelvet),
      
          // Tea Based
          MenuItem("Japanese Tea", null ,null, "18", "Tea",R.drawable.japanese_tea),
          MenuItem("Lemon Tea", null ,null, "18", "Tea",R.drawable.lemon_tea),
          MenuItem("Thai Tea", null ,null, "18", "Tea",R.drawable.thai_tea),
          MenuItem("Lychee Tea", null ,null, "18", "Tea",R.drawable.lychee_tea),
      
          // Snack
          MenuItem("French Fries", "15" ,null, null, "Makanan Ringan",R.drawable.french_fries),
          MenuItem("Tahu Baso", "15",null, null, "Makanan Ringan",R.drawable.tahu_bakso),
      
          // Main Course
          MenuItem("Chicken Katsu", "25", null, null, "Makanan Berat",R.drawable.chicken_katsu),
          MenuItem("Chicken Sambal Matah", "25", null, null, "Makanan Berat",R.drawable.chicken_sambel_matah),
          MenuItem("Chicken Blackpepper", "25", null, null, "Makanan Berat",R.drawable.chicken_blackpaper),
          MenuItem("Nasi Goreng Ayam", "20", null, null,"Makanan Berat",R.drawable.nasi_goreng)
      )
  
     
  4. MenuItemCard.kt:
     ~~~kt
      package com.example.josparcoffee.ui.component
      
      import androidx.compose.foundation.Image
      import androidx.compose.foundation.background
      import androidx.compose.foundation.layout.*
      import androidx.compose.foundation.shape.RoundedCornerShape
      import androidx.compose.material3.*
      import androidx.compose.runtime.Composable
      import androidx.compose.ui.Modifier
      import androidx.compose.ui.unit.dp
      import androidx.compose.ui.layout.ContentScale
      import androidx.compose.ui.res.painterResource
      import androidx.compose.ui.Alignment
      import androidx.compose.ui.graphics.Color
      import androidx.compose.ui.text.font.FontWeight
      import com.example.josparcoffee.R
      import com.example.josparcoffee.data.MenuItem
      
      @Composable
      fun MenuItemCard(item: MenuItem) {
          Card(
              modifier = Modifier
                  .fillMaxWidth()
                  .padding(vertical = 6.dp),
              shape = RoundedCornerShape(16.dp),
              elevation = CardDefaults.cardElevation(4.dp)
          ) {
              Row(
                  modifier = Modifier
                      .background(Color(0xFFF5F5F5))
                      .padding(12.dp),
                  verticalAlignment = Alignment.CenterVertically
              ) {
      
                  Image(
                      painter = painterResource(id = item.imageRes),
                      contentDescription = item.name,
                      modifier = Modifier.size(70.dp),
                      contentScale = ContentScale.Crop
                  )
      
                  Spacer(modifier = Modifier.width(12.dp))
      
                  Column(modifier = Modifier.weight(1f)) {
                      Text(item.name, fontWeight = FontWeight.Bold)
                  }
      
                  Column(horizontalAlignment = Alignment.End) {
                      item.priceHot?.let {
                          Text("Hot: $it.k")
                      }
                      item.priceIce?.let {
                          Text("Ice: $it.k")
                      }
                      item.price?.let {
                          Text("$it.k")
                      }
                  }
              }
          }
      }


5. HomeScreen.kt:
   ~~~kt
   package com.example.josparcoffee.ui.screen.home
    
   import androidx.compose.foundation.Image
   import androidx.compose.foundation.background
   import androidx.compose.foundation.layout.*
   import androidx.compose.material3.*
   import androidx.compose.runtime.Composable
   import androidx.compose.ui.Alignment
   import androidx.compose.ui.Modifier
   import androidx.compose.ui.graphics.Color
   import androidx.compose.ui.layout.ContentScale
   import androidx.compose.ui.res.painterResource
   import androidx.compose.ui.unit.dp
   import androidx.navigation.NavController
   import com.example.josparcoffee.R
    
   @Composable
   fun HomeScreen(navController: NavController) {

        Box(modifier = Modifier.fillMaxSize()) {
    
            // Background Image
            Image(
                painter = painterResource(id = R.drawable.background_home),
                contentDescription = null,
                contentScale = ContentScale.Crop,
                modifier = Modifier.fillMaxSize()
            )
    
            // Overlay biar teks kebaca
            Box(
                modifier = Modifier
                    .fillMaxSize()
                    .background(Color.Black.copy(alpha = 0.4f))
            )
    
            // Content
            Column(
                modifier = Modifier
                    .fillMaxSize()
                    .padding(16.dp),
                verticalArrangement = Arrangement.Center,
                horizontalAlignment = Alignment.CenterHorizontally
            ) {
    
                Text(
                    "Selamat Datang di",
                    color = Color.White
                )
    
                Text(
                    "Jospar Coffee",
                    color = Color.White,
                    style = MaterialTheme.typography.headlineLarge
                )
    
                Spacer(modifier = Modifier.height(20.dp))
    
                Text(
                    "Ngopi santai, kerja santuy ",
                    color = Color.White
                )
    
                Spacer(modifier = Modifier.height(40.dp))
    
                Button(
                    onClick = { navController.navigate("menu") },
                    modifier = Modifier.fillMaxWidth(0.7f)
                ) {
                    Text("Lihat Menu")
                }
    
                Spacer(modifier = Modifier.height(10.dp))
    
                OutlinedButton(
                    onClick = { navController.navigate("profile") },
                    modifier = Modifier.fillMaxWidth(0.7f)
                ) {
                    Text("Profile Coffee")
                }
            }
        }
    }


6. MenuScreen.kt:
   ~~~kt
    package com.example.josparcoffee.ui.screen.menu
    
    import androidx.compose.foundation.layout.*
    import androidx.compose.foundation.lazy.LazyColumn
    import androidx.compose.foundation.lazy.items
    import androidx.compose.material3.*
    import androidx.compose.runtime.Composable
    import androidx.compose.ui.Modifier
    import androidx.compose.ui.text.font.FontWeight
    import androidx.compose.ui.unit.dp
    import androidx.navigation.NavController
    import com.example.josparcoffee.data.MenuItem
    import com.example.josparcoffee.data.menuList
    import com.example.josparcoffee.ui.component.MenuItemCard
    
    @OptIn(ExperimentalMaterial3Api::class)
    @Composable
    fun MenuScreen(navController: NavController) {
    
        val groupedMenu: Map<String, List<MenuItem>> =
            menuList.groupBy { it.category.toString() }
    
        Scaffold(
            topBar = {
                TopAppBar(
                    title = { Text("Menu Coffee") }
                )
            }
        ) { padding ->
    
            LazyColumn(
                modifier = Modifier
                    .fillMaxSize()
                    .padding(padding)
                    .padding(16.dp)
            ) {
    
                groupedMenu.forEach { (category, items) ->
    
                    // CATEGORY TITLE
                    item {
                        Text(
                            text = category,
                            style = MaterialTheme.typography.titleLarge,
                            fontWeight = FontWeight.Bold,
                            modifier = Modifier.padding(vertical = 12.dp)
                        )
                        Divider()
                    }
    
                    // LIST MENU PER CATEGORY
                    items(items) { item ->
                        MenuItemCard(item)
                    }
                }
            }
        }
    }

   
7. ProfileScreen.kt:
   ~~~kt
    package com.example.josparcoffee.ui.screen.profile
    
    import androidx.compose.foundation.layout.*
    import androidx.compose.material3.*
    import androidx.compose.runtime.Composable
    import androidx.compose.ui.Alignment
    import androidx.compose.ui.Modifier
    import androidx.compose.ui.text.style.TextAlign
    import androidx.compose.ui.unit.dp
    import androidx.compose.ui.unit.sp
    
    @Composable
    fun ProfileScreen() {
    
        Column(
            modifier = Modifier.fillMaxSize(),
            verticalArrangement = Arrangement.Center,
            horizontalAlignment = Alignment.CenterHorizontally
        ) {
    
            Text("Jospar Coffee", style = MaterialTheme.typography.headlineMedium)
    
            Spacer(modifier = Modifier.height(10.dp))
    
            Text("Ngopi santai, kerja santuy")
    
            Spacer(modifier = Modifier.height(10.dp))
    
            Text("Since 2026")
    
            Text(
                "Lebih dari sekadar kopi. Jospar Coffee adalah tempat untuk berbagi cerita, ide, dan momen santai.",
                style = MaterialTheme.typography.bodyMedium,
                textAlign = TextAlign.Center,
                modifier = Modifier
                    .padding(horizontal = 24.dp, vertical = 12.dp)
            )
    
    
        }
    }


8. Theme.kt:
   ~~~kt
    package com.example.josparcoffee.ui.theme
    
    import android.app.Activity
    import android.os.Build
    import androidx.compose.foundation.isSystemInDarkTheme
    import androidx.compose.material3.MaterialTheme
    import androidx.compose.material3.darkColorScheme
    import androidx.compose.material3.dynamicDarkColorScheme
    import androidx.compose.material3.dynamicLightColorScheme
    import androidx.compose.material3.lightColorScheme
    import androidx.compose.runtime.Composable
    import androidx.compose.ui.platform.LocalContext
    
    private val DarkColorScheme = darkColorScheme(
        primary = Purple80,
        secondary = PurpleGrey80,
        tertiary = Pink80
    )
    
    private val LightColorScheme = lightColorScheme(
        primary = Purple40,
        secondary = PurpleGrey40,
        tertiary = Pink40
    
        /* Other default colors to override
        background = Color(0xFFFFFBFE),
        surface = Color(0xFFFFFBFE),
        onPrimary = Color.White,
        onSecondary = Color.White,
        onTertiary = Color.White,
        onBackground = Color(0xFF1C1B1F),
        onSurface = Color(0xFF1C1B1F),
        */
    )
    
    @Composable
    fun JosparCoffeeTheme(
        darkTheme: Boolean = isSystemInDarkTheme(),
        // Dynamic color is available on Android 12+
        dynamicColor: Boolean = true,
        content: @Composable () -> Unit
    ) {
        val colorScheme = when {
            dynamicColor && Build.VERSION.SDK_INT >= Build.VERSION_CODES.S -> {
                val context = LocalContext.current
                if (darkTheme) dynamicDarkColorScheme(context) else dynamicLightColorScheme(context)
            }
    
            darkTheme -> DarkColorScheme
            else -> LightColorScheme
        }
    
        MaterialTheme(
            colorScheme = colorScheme,
            typography = Typography,
            content = content
        )
    
    }


9. DetailScreen.kt:
   ~~~kt
    package com.example.josparcoffee.ui.screen.detail
    
    import com.example.josparcoffee.R
    import androidx.compose.foundation.Image
    import androidx.compose.foundation.layout.*
    import androidx.compose.material3.*
    import androidx.compose.material3.TopAppBar
    import androidx.compose.material3.Text
    import androidx.compose.runtime.Composable
    import androidx.compose.ui.Alignment
    import androidx.compose.ui.Modifier
    import androidx.compose.ui.modifier.modifierLocalOf
    import androidx.compose.ui.res.painterResource
    import androidx.compose.ui.unit.dp
    
    @OptIn(ExperimentalMaterial3Api::class)
    @Composable
    fun DetailScreen(name: String, price: String) {
    
        Scaffold(
            topBar = {
                TopAppBar(title = { Text("Detail Menu") })
            }
        ) { padding ->
    
            Column(
                modifier = Modifier
                    .fillMaxSize()
                    .padding(padding),
                horizontalAlignment = Alignment.CenterHorizontally,
                verticalArrangement = Arrangement.Center
            ) {
    
                Text(name, style = MaterialTheme.typography.headlineMedium)
    
                Spacer(modifier = Modifier.height(12.dp))
    
                Text("Harga: Rp $price.000")
    
                Spacer(modifier = Modifier.height(20.dp))
    
                Button(onClick = {}) {
                    Text("Order")
                }
            }
        }
    }


10. Build.gradle.kts (:app):
    ~~~kts
    plugins {
    alias(libs.plugins.android.application)
    alias(libs.plugins.kotlin.compose)
    }
    
    android {
        namespace = "com.example.josparcoffee"
        compileSdk {
            version = release(36) {
                minorApiLevel = 1
            }
        }
    
        defaultConfig {
            applicationId = "com.example.josparcoffee"
            minSdk = 24
            targetSdk = 36
            versionCode = 1
            versionName = "1.0"
    
            testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"
        }
    
        buildTypes {
            release {
                isMinifyEnabled = false
                proguardFiles(
                    getDefaultProguardFile("proguard-android-optimize.txt"),
                    "proguard-rules.pro"
                )
            }
        }
        compileOptions {
            sourceCompatibility = JavaVersion.VERSION_11
            targetCompatibility = JavaVersion.VERSION_11
        }
        buildFeatures {
            compose = true
        }
    }
    
    dependencies {
        implementation("androidx.navigation:navigation-compose:2.7.7")
        implementation(libs.androidx.core.ktx)
        implementation(libs.androidx.lifecycle.runtime.ktx)
        implementation(libs.androidx.activity.compose)
        implementation(platform(libs.androidx.compose.bom))
        implementation(libs.androidx.compose.ui)
        implementation(libs.androidx.compose.ui.graphics)
        implementation(libs.androidx.compose.ui.tooling.preview)
        implementation(libs.androidx.compose.material3)
        implementation("androidx.compose.material3:material3")
        implementation("androidx.compose.material3:material3:1.2.1")
        implementation(libs.androidx.compose.foundation)
        testImplementation(libs.junit)
        androidTestImplementation(libs.androidx.junit)
        androidTestImplementation(libs.androidx.espresso.core)
        androidTestImplementation(platform(libs.androidx.compose.bom))
        androidTestImplementation(libs.androidx.compose.ui.test.junit4)
        debugImplementation(libs.androidx.compose.ui.tooling)
        debugImplementation(libs.androidx.compose.ui.test.manifest)
    }
