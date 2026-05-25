# Tugas Praktikum 9: Data Persistence 1

## Kelompok 5:
1. Azfa Rahma Putra Susanto (L0324008)
2. Hammam Ibnu Adi'Abdillah (L0324015)
3. Indra Fata Azhari L0324017)

Jadi dari project sebelumnya ada beberapa perubahan yang banyak merubah struktur dari project kami.

## Source Code yang digunakan:

###
1. AndroidManifest.xml
   ~~~xml
   <?xml version="1.0" encoding="utf-8"?>
   <manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <uses-permission android:name="android.permission.INTERNET"/>
    <application
        android:usesCleartextTraffic="true"
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.JOSPAR">
        <activity
            android:name=".MainActivity"
            android:exported="true"
            android:label="@string/app_name"
            android:theme="@style/Theme.JOSPAR">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>
   </manifest>
3. MenuRepoditory.kt
   ~~~kt
   package com.example.jospar.data

   import com.example.jospar.R
   import com.example.jospar.model.MenuItem

   object MenuRepository{

    val menuList = listOf(

        // COFFEE

        MenuItem(
            id = 1,
            name = "Cappuccino",
            description = "Rich espresso with creamy milk foam.",
            priceHot = "22",
            priceIce = "20",
            category = "Coffee",
            imageRes = R.drawable.cappuccino,
            rating = 4.8
        ),

        MenuItem(
            id = 2,
            name = "Americano",
            description = "Bold espresso with smooth finish.",
            priceHot = "18",
            priceIce = "17",
            category = "Coffee",
            imageRes = R.drawable.americano,
            rating = 4.6
        ),

        MenuItem(
            id = 3,
            name = "Mochaccino",
            description = "Chocolate espresso with creamy texture.",
            priceHot = "22",
            priceIce = "20",
            category = "Coffee",
            imageRes = R.drawable.mochaccino,
            rating = 4.7
        ),

        MenuItem(
            id = 4,
            name = "Caramel Latte",
            description = "Sweet caramel blended with espresso.",
            priceHot = "20",
            priceIce = "20",
            category = "Coffee",
            imageRes = R.drawable.caramel_latte,
            rating = 4.9
        ),

        MenuItem(
            id = 5,
            name = "Vanilla Latte",
            description = "Smooth vanilla latte with fresh milk.",
            priceHot = "20",
            priceIce = "20",
            category = "Coffee",
            imageRes = R.drawable.vanilla_latte,
            rating = 4.7
        ),

        // MILK

        MenuItem(
            id = 6,
            name = "Chocolate",
            description = "Creamy chocolate drink.",
            priceHot = "19",
            priceIce = "17",
            category = "Milk",
            imageRes = R.drawable.chocolate,
            rating = 4.5
        ),

        MenuItem(
            id = 7,
            name = "Matcha",
            description = "Premium japanese matcha latte.",
            priceHot = "23",
            priceIce = "22",
            category = "Milk",
            imageRes = R.drawable.matcha,
            rating = 4.8
        ),

        MenuItem(
            id = 8,
            name = "Milo Dino Favorito",
            description = "Sweet milo with crunchy topping.",
            priceHot = "19",
            priceIce = "18",
            category = "Milk",
            imageRes = R.drawable.milo,
            rating = 4.6
        ),

        MenuItem(
            id = 9,
            name = "Red Velvet",
            description = "Creamy red velvet signature drink.",
            priceHot = "19",
            priceIce = "17",
            category = "Milk",
            imageRes = R.drawable.redvelvet,
            rating = 4.7
        ),

        // TEA

        MenuItem(
            id = 10,
            name = "Jasmine Tea",
            description = "Refreshing jasmine tea.",
            priceHot = "20",
            priceIce = "18",
            category = "Tea",
            imageRes = R.drawable.japanese_tea,
            rating = 4.4
        ),

        MenuItem(
            id = 11,
            name = "Lemon Tea",
            description = "Fresh lemon with iced tea.",
            price = "18",
            priceIce = "18",
            category = "Tea",
            imageRes = R.drawable.lemon_tea,
            rating = 4.5
        ),

        MenuItem(
            id = 12,
            name = "Thai Tea",
            description = "Authentic thai tea flavor.",
            price = "18",
            priceIce = "18",
            category = "Tea",
            imageRes = R.drawable.thai_tea,
            rating = 4.6
        ),

        MenuItem(
            id = 13,
            name = "Lychee Tea",
            description = "Sweet lychee infused tea.",
            price = "18",
            priceIce = "18",
            category = "Tea",
            imageRes = R.drawable.lychee_tea,
            rating = 4.5
        ),

        // SNACK

        MenuItem(
            id = 14,
            name = "French Fries",
            description = "Crispy french fries.",
            price = "15",
            category = "Snack",
            imageRes = R.drawable.french_fries,
            rating = 4.3
        ),

        MenuItem(
            id = 15,
            name = "Tahu Baso",
            description = "Savory tahu baso snack.",
            price = "15",
            category = "Snack",
            imageRes = R.drawable.tahu_bakso,
            rating = 4.4
        ),

        // MAIN COURSE

        MenuItem(
            id = 16,
            name = "Chicken Katsu",
            description = "Crispy chicken katsu with rice.",
            price = "25",
            category = "Main Course",
            imageRes = R.drawable.chicken_katsu,
            rating = 4.8
        ),

        MenuItem(
            id = 17,
            name = "Chicken Sambal Matah",
            description = "Spicy sambal matah chicken.",
            price = "25",
            category = "Main Course",
            imageRes = R.drawable.chicken_sambel_matah,
            rating = 4.9
        ),

        MenuItem(
            id = 18,
            name = "Chicken Blackpepper",
            description = "Blackpepper chicken special.",
            price = "25",
            category = "Main Course",
            imageRes = R.drawable.chicken_blackpaper,
            rating = 4.7
        ),

        MenuItem(
            id = 19,
            name = "Nasi Goreng Ayam",
            description = "Indonesian fried rice with chicken.",
            price = "20",
            category = "Main Course",
            imageRes = R.drawable.nasi_goreng,
            rating = 4.6
        )
    )
   }
   
5. OrderPreferences.kt
   ~~~kt
   package com.example.jospar.data

   import android.content.Context
   import androidx.datastore.preferences.core.booleanPreferencesKey
   import androidx.datastore.preferences.core.edit
   import androidx.datastore.preferences.preferencesDataStore
   import kotlinx.coroutines.flow.Flow
   import kotlinx.coroutines.flow.map

   private val Context.dataStore by preferencesDataStore(

    name = "order_prefs"
   )

   class OrderPreferences(

    private val context: Context

   ) {

    companion object {

        val HAS_ORDER = booleanPreferencesKey(

            "has_order"
        )
    }

    suspend fun saveOrderStatus(

        hasOrder: Boolean

    ) {

        context.dataStore.edit { preferences ->

            preferences[HAS_ORDER] = hasOrder
        }
    }

    val orderStatus: Flow<Boolean> =

        context.dataStore.data.map { preferences ->

            preferences[HAS_ORDER] ?: false
        }
   }
   
7. Cartitem.kt
   ~~~kt
   package com.example.jospar.model

   import androidx.compose.runtime.getValue
   import androidx.compose.runtime.mutableIntStateOf
   import androidx.compose.runtime.setValue

   class CartItem(

    val menu: MenuItem,

    val selectedType: String?,

    quantity: Int
   ) {

    var quantity by mutableIntStateOf(quantity)
   }
   
9. MenuItem.kt
    ~~~kt
   package com.example.jospar.model

   data class MenuItem(

    val id: Int,

    val name: String,

    val description: String,

    val price: String? = null,

    val priceHot: String? = null,

    val priceIce: String? = null,

    val category: String,

    val imageRes: Int,

    val rating: Double,

    val favorite: Boolean = false
   )
    
11. AppNavigation.kt
    ~~~kt
     package com.example.jospar.navigation

     import androidx.compose.runtime.Composable
     import androidx.navigation.NavType
     import androidx.navigation.compose.NavHost
     import androidx.navigation.compose.composable
     import androidx.navigation.compose.rememberNavController
     import androidx.navigation.navArgument
     import androidx.lifecycle.viewmodel.compose.viewModel
     import com.example.jospar.viewmodel.MenuViewModel
     import com.example.jospar.ui.screen.cart.CartScreen
     import com.example.jospar.ui.screen.detail.DetailScreen
     import com.example.jospar.ui.screen.home.HomeScreen
     import com.example.jospar.ui.screen.splash.SplashScreen
     import com.example.jospar.ui.screen.checkout.CheckoutScreen
     import com.example.jospar.ui.screen.tracking.TrackingScreen
     import com.example.jospar.ui.screen.payment.PaymentSuccessScreen
   
   
     @Composable
     fun AppNavigation(
   
       viewModel: MenuViewModel
     ) {

       val navController = rememberNavController()
       val menuViewModel: MenuViewModel = viewModel()

       NavHost(
   
           navController = navController,
   
           startDestination = "splash"
   
       ) {

           composable("splash") {
   
               SplashScreen(navController)
           }
   
           composable("home") {
   
               HomeScreen(
   
                   navController = navController,
   
                   viewModel = menuViewModel
               )
           }
   
           composable("cart") {
   
               CartScreen(
   
                   navController = navController,
   
                   viewModel = menuViewModel
               )
           }
   
           composable(
   
               route = "detail/{menuId}",
   
               arguments = listOf(
   
                   navArgument("menuId") {
   
                       type = NavType.IntType
                   }
               )
   
           ) { backStackEntry ->
   
               val menuId = backStackEntry.arguments
                   ?.getInt("menuId") ?: 0
   
               DetailScreen(
   
                   navController = navController,
                   menuId = menuId,
   
                   viewModel = menuViewModel
               )
           }
   
           composable("checkout") {
   
               CheckoutScreen(
   
                   navController = navController,
                   viewModel = menuViewModel
               )
           }
   
           composable("tracking") {
   
               TrackingScreen(
   
                   navController = navController,
                   viewModel = menuViewModel
               )
           }
   
           composable(
   
               route = "payment/{snapToken}"
   
           ) { backStackEntry ->
   
               val snapToken =
                   backStackEntry.arguments
                       ?.getString("snapToken") ?: ""
   
           }
   
           composable("payment_success") {
   
               PaymentSuccessScreen(navController)
           }
   
           composable("splash") {
   
               SplashScreen(navController)
           }
       }
    }
    
13. ApiService.kt
    ~~~kt
    package com.example.jospar.network

    import okhttp3.ResponseBody
    import retrofit2.Response
    import retrofit2.http.GET
    import retrofit2.http.Query
   
    interface ApiService {

          @GET("create_transaction.php")
          suspend fun createTransaction(
      
            @Query("amount")
            amount: Int,
      
            @Query("items")
            items: String
      
          ): Response<ResponseBody>
      }
    
15. RetrofitInstance.kt
    ~~~kt
    package com.example.jospar.network

    import retrofit2.Retrofit
    import retrofit2.converter.gson.GsonConverterFactory
      
      object RetrofitInstance {
      
          private const val BASE_URL =
              "http://10.0.2.2/jospar_backend/"
      
          val api: ApiService by lazy {
      
              Retrofit.Builder()
                  .baseUrl(BASE_URL)
                  .addConverterFactory(
                      GsonConverterFactory.create()
                  )
                  .build()
                  .create(ApiService::class.java)
          }
      }
    
17. BottomBar.kt
    ~~~kt
    package com.example.jospar.ui.component

    import android.widget.Toast
    import androidx.compose.ui.platform.LocalContext
    import androidx.compose.foundation.layout.height
    import androidx.compose.material.icons.Icons
    import androidx.compose.material.icons.filled.Home
    import androidx.compose.material.icons.filled.List
    import androidx.compose.material.icons.filled.ShoppingCart
    import androidx.compose.material3.*
    import androidx.compose.runtime.Composable
    import androidx.compose.ui.Modifier
    import androidx.compose.ui.unit.dp
    import androidx.navigation.NavController
    import com.example.jospar.viewmodel.MenuViewModel
      
    @Composable
    fun BottomBar(
      
          navController: NavController,
      
          currentRoute: String?,
      
          viewModel: MenuViewModel
      
    ) {
      
          val context = LocalContext.current
      
      
          NavigationBar(
      
              modifier = Modifier.height(56.dp),
      
    ) {
      
              NavigationBarItem(
      
                  selected = currentRoute == "home",
      
                  onClick = {
      
                      navController.navigate("home")
                  },
      
                  alwaysShowLabel = false,
      
                  icon = {
      
                      Icon(
      
                          imageVector = Icons.Default.Home,
      
                          contentDescription = "Home"
                      )
                  }
              )
      
              NavigationBarItem(
      
                  selected = currentRoute == "cart",
      
                  onClick = {
      
                      navController.navigate("cart")
                  },
      
                  alwaysShowLabel = false,
      
                  icon = {
      
                      BadgedBox(
      
                          badge = {
      
                              if (viewModel.cartItems.isNotEmpty()) {
      
                                  Badge {
      
                                      Text(
                                          text = viewModel.cartItems.size.toString()
                                      )
                                  }
                              }
                          }
      
                      ) {
      
                          Icon(
      
                              imageVector = Icons.Default.ShoppingCart,
      
                              contentDescription = "Cart"
                          )
                      }
                  }
              )
      
              NavigationBarItem(
      
                  selected = currentRoute == "tracking",
      
                  onClick = {
      
                      if (viewModel.hasActiveOrder) {
      
                          navController.navigate("tracking")
      
                      } else {
      
                          Toast.makeText(
      
                              context,
      
                              "Tidak ada tracking order, lakukan order dulu ☕",
      
                              Toast.LENGTH_SHORT
      
                          ).show()
                      }
                  },
      
                  alwaysShowLabel = false,
      
                  icon = {
      
                      Icon(
      
                          imageVector = Icons.Default.List,
      
                          contentDescription = "Tracking"
                      )
                  }
              )
          }
      }
19. MenuCard.kt
20. CartScreen.kt
21. CheckoutScreen.kt
22. DetailScreen.kt
23. HomeScreen.kt
24. PaymentSuccessScreen.kt
25. SplashScreen.kt
26. SuccessScreen.kt
27. TrackingScreen.kt
28. Color.kt
29. Theme.kt
30. Type.kt
31. MenuViewModel.kt
32. MainActivity.kt
