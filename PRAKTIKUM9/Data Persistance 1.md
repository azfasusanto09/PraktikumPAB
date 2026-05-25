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
   
2. MenuRepoditory.kt
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
   
3. OrderPreferences.kt
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
   
4. CartItem.kt
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
   
5. MenuItem.kt
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
    
6. AppNavigation.kt
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
    
7. ApiService.kt
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
    
8. RetrofitInstance.kt
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
    
9. BottomBar.kt
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
    
10. MenuCard.kt
    ~~~kt
    package com.example.jospar.ui.component

      import androidx.compose.foundation.Image
      import androidx.compose.foundation.background
      import androidx.compose.foundation.clickable
      import androidx.compose.foundation.layout.*
      import androidx.compose.foundation.shape.RoundedCornerShape
      import androidx.compose.material3.*
      import androidx.compose.material.icons.Icons
      import androidx.compose.material.icons.filled.Add
      import androidx.compose.runtime.Composable
      import androidx.compose.ui.Alignment
      import androidx.compose.ui.Modifier
      import androidx.compose.ui.graphics.Brush
      import androidx.compose.ui.layout.ContentScale
      import androidx.compose.ui.res.painterResource
      import androidx.compose.ui.text.font.FontWeight
      import androidx.compose.ui.unit.dp
      import com.example.jospar.model.MenuItem
      
      @Composable
      fun MenuCard(
      
          menu: MenuItem,
      
          onClick: () -> Unit
      
      ) {
      
          Card(
      
              modifier = Modifier
                  .fillMaxWidth()
                  .height(200.dp)
                  .clickable {
      
                      onClick()
                  },
      
              shape = RoundedCornerShape(24.dp),
      
              elevation = CardDefaults.cardElevation(
      
                  defaultElevation = 8.dp
              )
      
          ) {
      
              Box {
      
                  Image(
      
                      painter = painterResource(id = menu.imageRes),
      
                      contentDescription = menu.name,
      
                      modifier = Modifier.fillMaxSize(),
      
                      contentScale = ContentScale.FillBounds
                  )
      
                  Box(
      
                      modifier = Modifier
                          .fillMaxSize()
                          .background(
      
                              Brush.verticalGradient(
      
                                  colors = listOf(
      
                                      androidx.compose.ui.graphics.Color.Transparent,
      
                                      androidx.compose.ui.graphics.Color.Black.copy(alpha = 0.85f)
                                  )
                              )
                          )
                  )
      
                  Column(
      
                      modifier = Modifier
                          .align(Alignment.BottomStart)
                          .padding(16.dp)
      
                  ) {
      
                      Text(
      
                          text = menu.name,
      
                          style = MaterialTheme.typography.titleLarge,
      
                          color = androidx.compose.ui.graphics.Color.White,
      
                          fontWeight = FontWeight.Bold
                      )
      
                      Spacer(modifier = Modifier.height(4.dp))
      
                      Text(
      
                          text = menu.category,
      
                          color = androidx.compose.ui.graphics.Color.LightGray
                      )
      
                      Spacer(modifier = Modifier.height(8.dp))
      
                      val price = menu.price
                          ?: menu.priceIce
                          ?: menu.priceHot
                          ?: "0"
      
                      Text(
      
                          text = "Rp ${price}.000",
      
                          style = MaterialTheme.typography.titleMedium,
      
                          color = MaterialTheme.colorScheme.primary,
      
                          fontWeight = FontWeight.Bold
                      )
                  }
      
                  FloatingActionButton(
      
                      onClick = {
      
                          onClick()
                      },
      
                      modifier = Modifier
                          .align(Alignment.BottomEnd)
                          .padding(16.dp),
      
                      containerColor = MaterialTheme.colorScheme.primary
      
                  ) {
      
                      Icon(
      
                          imageVector = Icons.Default.Add,
      
                          contentDescription = "Add"
                      )
                  }
              }
          }
      }
    
11. CartScreen.kt
    ~~~kt
    package com.example.jospar.ui.screen.cart

      import androidx.compose.foundation.Image
      import androidx.compose.foundation.layout.*
      import androidx.compose.foundation.lazy.LazyColumn
      import androidx.compose.foundation.lazy.items
      import androidx.compose.material3.*
      import androidx.compose.material.icons.Icons
      import androidx.compose.material.icons.filled.ArrowBack
      import androidx.compose.material3.Icon
      import androidx.compose.runtime.Composable
      import androidx.compose.ui.Alignment
      import androidx.compose.ui.Modifier
      import androidx.compose.ui.layout.ContentScale
      import androidx.compose.ui.res.painterResource
      import androidx.compose.ui.text.font.FontWeight
      import androidx.compose.ui.unit.dp
      import androidx.navigation.NavController
      import com.example.jospar.viewmodel.MenuViewModel
      
      @OptIn(ExperimentalMaterial3Api::class)
      @Composable
      fun CartScreen(
      
          navController: NavController,
      
          viewModel: MenuViewModel
      
      ) {
      
          val cartItems = viewModel.cartItems
      
          Scaffold(
      
              topBar = {
      
      
                  TopAppBar(
      
                      title = {
      
                          Text("Cart 🛒")
                      },
      
                      navigationIcon = {
      
                          IconButton(
      
                              onClick = {
      
                                  navController.navigateUp()
                              }
      
                          ) {
      
                              Icon(
      
                                  imageVector = Icons.Default.ArrowBack,
      
                                  contentDescription = "Back"
                              )
                          }
                      }
                  )
              }
      
          ) { padding ->
      
              if (cartItems.isEmpty()) {
      
                  Box(
      
                      modifier = Modifier
                          .padding(padding)
                          .fillMaxSize(),
      
                      contentAlignment = Alignment.Center
      
                      ) {
      
                      Text(
      
                          text = "KERANJANG KOSONG",
                          style = MaterialTheme.typography.titleMedium
                      )
                  }
      
              } else {
      
                  if (cartItems.isEmpty()) {
      
                      Box(
      
                          modifier = Modifier
                              .padding(padding)
                              .fillMaxSize(),
      
                          contentAlignment = Alignment.Center
      
                      ) {
      
                          Column(
      
                              horizontalAlignment = Alignment.CenterHorizontally
      
                          ) {
      
                              Text(
      
                                  text = "🛒",
      
                                  style = MaterialTheme.typography.displayMedium
                              )
      
                              Spacer(modifier = Modifier.height(12.dp))
      
                              Text(
      
                                  text = "Keranjangmu Masih Kosong",
      
                                  style = MaterialTheme.typography.titleMedium
                              )
                          }
                      }
      
                  } else {
      
                      Column(
      
                          modifier = Modifier
                              .padding(padding)
                              .fillMaxSize()
                              .padding(16.dp)
      
                      ) {
      
                          LazyColumn(
      
                              modifier = Modifier.weight(1f),
      
                              verticalArrangement = Arrangement.spacedBy(16.dp)
      
                          ) {
      
                              items(cartItems) { cartItem ->
      
                                  Card {
      
                                      Row(
      
                                          modifier = Modifier.padding(16.dp)
      
                                      ) {
      
                                          Image(
      
                                              painter = painterResource(
                                                  id = cartItem.menu.imageRes
                                              ),
      
                                              contentDescription = cartItem.menu.name,
      
                                              modifier = Modifier.size(90.dp),
      
                                              contentScale = ContentScale.Crop
                                          )
      
                                          Spacer(
                                              modifier = Modifier.width(16.dp)
                                          )
      
                                          Column(
      
                                              modifier = Modifier.weight(1f)
      
                                          ) {
      
                                              Text(
      
                                                  text = cartItem.menu.name,
      
                                                  fontWeight = FontWeight.Bold
                                              )
      
                                              cartItem.selectedType?.let {
      
                                                  Text(text = it)
                                              }
      
                                              Row(
      
                                                  horizontalArrangement = Arrangement.spacedBy(12.dp),
      
                                                  verticalAlignment = Alignment.CenterVertically
      
                                              ) {
      
                                                  Button(
      
                                                      onClick = {
      
                                                          viewModel.decreaseQuantity(cartItem)
                                                      },
      
                                                      contentPadding = PaddingValues(0.dp),
      
                                                      modifier = Modifier.size(36.dp)
      
                                                  ) {
      
                                                      Text("-")
                                                  }
      
                                                  Text(
      
                                                      text = cartItem.quantity.toString(),
      
                                                      style = MaterialTheme.typography.titleMedium
                                                  )
      
                                                  Button(
      
                                                      onClick = {
      
                                                          viewModel.increaseQuantity(cartItem)
                                                      },
      
                                                      contentPadding = PaddingValues(0.dp),
      
                                                      modifier = Modifier.size(36.dp)
      
                                                  ) {
      
                                                      Text("+")
                                                  }
                                              }
      
                                              Spacer(
                                                  modifier = Modifier.height(8.dp)
                                              )
      
                                              val price = when (cartItem.selectedType) {
      
                                                  "Hot" -> cartItem.menu.priceHot
      
                                                  "Ice" -> cartItem.menu.priceIce
      
                                                  else -> cartItem.menu.price
      
                                              } ?: "0"
      
                                              val subtotal =
                                                  price.toInt() * cartItem.quantity
      
                                              Text(
                                                  text = "Rp ${subtotal}.000"
                                              )
                                          }
      
                                          TextButton(
      
                                              onClick = {
      
                                                  viewModel.removeFromCart(cartItem)
                                              }
      
                                          ) {
      
                                              Text("Remove")
                                          }
                                      }
                                  }
                              }
                          }
      
                          Spacer(modifier = Modifier.height(20.dp))
      
                          val totalPrice = cartItems.sumOf { cartItem ->
      
                              val price = when (cartItem.selectedType) {
      
                                  "Hot" -> cartItem.menu.priceHot
      
                                  "Ice" -> cartItem.menu.priceIce
      
                                  else -> cartItem.menu.price
      
                              } ?: "0"
      
                              price.toInt() * cartItem.quantity
                          }
      
                          Card(
      
                              modifier = Modifier.fillMaxWidth()
      
                          ) {
      
                              Row(
      
                                  modifier = Modifier
                                      .fillMaxWidth()
                                      .padding(20.dp),
      
                                  horizontalArrangement = Arrangement.SpaceBetween
      
                              ) {
      
                                  Text(
      
                                      text = "Total Payment",
      
                                      style = MaterialTheme.typography.titleMedium,
      
                                      fontWeight = FontWeight.Bold
                                  )
      
                                  Text(
      
                                      text = "Rp ${totalPrice}.000",
      
                                      style = MaterialTheme.typography.titleMedium,
      
                                      fontWeight = FontWeight.Bold
                                  )
                              }
                          }
      
                          Spacer(modifier = Modifier.height(20.dp))
      
                          Button(
      
                              onClick = {
      
                                  navController.navigate("checkout")
                              },
      
                              modifier = Modifier.fillMaxWidth()
      
                          ) {
      
                              Text("Checkout")
                          }
                      }
                  }
              }
          }
      }
    
12. CheckoutScreen.kt
    ~~~kt
    package com.example.jospar.ui.screen.checkout

      import androidx.compose.foundation.layout.*
      import androidx.compose.foundation.lazy.LazyColumn
      import androidx.compose.foundation.lazy.items
      import androidx.compose.material.icons.Icons
      import androidx.compose.material.icons.filled.ArrowBack
      import androidx.compose.material.icons.filled.CreditCard
      import androidx.compose.material3.*
      import androidx.compose.runtime.*
      import androidx.compose.ui.Modifier
      import androidx.compose.ui.graphics.Color
      import androidx.compose.ui.text.font.FontWeight
      import androidx.compose.ui.unit.dp
      import androidx.navigation.NavController
      import androidx.compose.ui.platform.LocalContext
      import com.example.jospar.viewmodel.MenuViewModel
      
      @OptIn(ExperimentalMaterial3Api::class)
      @Composable
      fun CheckoutScreen(
      
          navController: NavController,
      
          viewModel: MenuViewModel
      
      ) {
          val context = LocalContext.current
      
          val cartItems = viewModel.cartItems
      
          val totalPrice = cartItems.sumOf { cartItem ->
      
              val price = when (cartItem.selectedType) {
      
                  "Hot" -> cartItem.menu.priceHot
      
                  "Ice" -> cartItem.menu.priceIce
      
                  else -> cartItem.menu.price
      
              } ?: "0"
      
              price.toInt() * cartItem.quantity
          }
      
          Scaffold(
      
              topBar = {
      
                  TopAppBar(
      
                      title = {
      
                          Text("Checkout")
                      },
      
                      navigationIcon = {
      
                          IconButton(
      
                              onClick = {
      
                                  navController.navigateUp()
                              }
      
                          ) {
      
                              Icon(
      
                                  imageVector = Icons.Default.ArrowBack,
      
                                  contentDescription = "Back"
                              )
                          }
                      }
                  )
              }
      
          ) { padding ->
      
              Column(
      
                  modifier = Modifier
                      .padding(padding)
                      .fillMaxSize()
                      .padding(16.dp)
      
              ) {
      
                  LazyColumn(
      
                      modifier = Modifier.weight(1f),
      
                      verticalArrangement = Arrangement.spacedBy(16.dp)
      
                  ) {
      
                      item {
      
                          Text(
      
                              text = "Order Summary",
      
                              style = MaterialTheme.typography.titleLarge,
      
                              fontWeight = FontWeight.Bold
                          )
                      }
      
                      items(cartItems) { cartItem ->
      
                          Card(
      
                              colors = CardDefaults.cardColors(
      
                                  containerColor = Color(0xFF2D1B16)
                              )
      
                          ) {
      
                              Row(
      
                                  modifier = Modifier
                                      .fillMaxWidth()
                                      .padding(16.dp),
      
                                  horizontalArrangement = Arrangement.SpaceBetween
      
                              ) {
      
                                  Column {
      
                                      Text(
      
                                          text = cartItem.menu.name,
      
                                          color = Color.White,
      
                                          fontWeight = FontWeight.Bold
                                      )
      
                                      cartItem.selectedType?.let {
      
                                          Text(
      
                                              text = it,
      
                                              color = Color.LightGray
                                          )
                                      }
      
                                      Text(
      
                                          text = "Qty ${cartItem.quantity}",
      
                                          color = Color.LightGray
                                      )
                                  }
      
                                  val price = when (cartItem.selectedType) {
      
                                      "Hot" -> cartItem.menu.priceHot
      
                                      "Ice" -> cartItem.menu.priceIce
      
                                      else -> cartItem.menu.price
      
                                  } ?: "0"
      
                                  Text(
      
                                      text = "Rp ${price.toInt() * cartItem.quantity}.000",
      
                                      color = Color(0xFFD7A16A),
      
                                      fontWeight = FontWeight.Bold
                                  )
                              }
                          }
                      }
      
                      item {
      
                          Spacer(modifier = Modifier.height(12.dp))
      
                          Text(
      
                              text = "Payment Method",
      
                              style = MaterialTheme.typography.titleLarge,
      
                              fontWeight = FontWeight.Bold
                          )
                      }
      
                      item {
      
                          Card(
      
                              colors = CardDefaults.cardColors(
      
                                  containerColor = Color(0xFF3E2723)
                              )
      
                          ) {
      
                              Row(
      
                                  modifier = Modifier
                                      .fillMaxWidth()
                                      .padding(20.dp),
      
                                  horizontalArrangement = Arrangement.spacedBy(16.dp)
      
                              ) {
      
                                  Icon(
      
                                      imageVector = Icons.Default.CreditCard,
      
                                      contentDescription = null,
      
                                      tint = Color.White
                                  )
      
                                  Text(
      
                                      text = "Midtrans Payment Gateway",
      
                                      color = Color.White
                                  )
                              }
                          }
                      }
                  }
      
                  Card(
      
                      colors = CardDefaults.cardColors(
      
                          containerColor = Color(0xFF4E342E)
                      )
      
                  ) {
      
                      Row(
      
                          modifier = Modifier
                              .fillMaxWidth()
                              .padding(20.dp),
      
                          horizontalArrangement = Arrangement.SpaceBetween
      
                      ) {
      
                          Text(
      
                              text = "Total Payment",
      
                              color = Color.White,
      
                              fontWeight = FontWeight.Bold
                          )
      
                          Text(
      
                              text = "Rp ${totalPrice}.000",
      
                              color = Color(0xFFD7A16A),
      
                              fontWeight = FontWeight.Bold
                          )
                      }
                  }
      
                  Spacer(modifier = Modifier.height(20.dp))
      
                  Button(
      
                      onClick = {
                          val itemsJson = cartItems.joinToString("|"){
                              "${it.menu.name},${it.quantity}"
                          }
      
                          viewModel.createTransaction (
                              totalPrice * 1000,
                              itemsJson
                          ){ token ->
      
                              if (token != null) {
      
                                  val paymentUrl =
                                      "https://app.sandbox.midtrans.com/snap/v2/vtweb/$token"
      
                                  val intent = android.content.Intent(
      
                                      android.content.Intent.ACTION_VIEW,
      
                                      android.net.Uri.parse(paymentUrl)
                                  )
      
                                  context.startActivity(intent)
      
                                  viewModel.checkout()
                                  viewModel.clearCart()
                                  navController.navigate("success")
                              }
                          }
                      },
      
                      modifier = Modifier
                          .fillMaxWidth()
                          .height(58.dp),
      
                      colors = ButtonDefaults.buttonColors(
      
                          containerColor = Color(0xFFD7A16A)
                      )
      
                  ) {
      
                      Text(
      
                          text = "Pay Now",
      
                          color = Color.White,
      
                          style = MaterialTheme.typography.titleMedium
                      )
                  }
              }
          }
      }
    
13. DetailScreen.kt
    ~~~kt
    package com.example.jospar.ui.screen.detail

      import androidx.compose.foundation.Image
      import androidx.compose.foundation.layout.*
      import androidx.compose.foundation.shape.RoundedCornerShape
      import androidx.compose.material3.*
      import androidx.compose.material.icons.Icons
      import androidx.compose.material.icons.filled.ArrowBack
      import androidx.compose.material3.Icon
      import androidx.compose.runtime.*
      import androidx.compose.ui.Modifier
      import androidx.compose.ui.layout.ContentScale
      import androidx.compose.ui.res.painterResource
      import androidx.compose.ui.text.font.FontWeight
      import androidx.compose.ui.unit.dp
      import androidx.navigation.NavController
      import com.example.jospar.viewmodel.MenuViewModel
      import kotlinx.coroutines.launch
      
      @OptIn(ExperimentalMaterial3Api::class)
      @Composable
      fun DetailScreen(
      
          navController: NavController,
      
          menuId: Int,
      
          viewModel: MenuViewModel
      
      ) {
      
          val menu = viewModel.menuList.find {
      
              it.id == menuId
          }
      
          var quantity by remember {
      
              mutableStateOf(1)
          }
      
          val snackbarHostState = remember {
      
              SnackbarHostState()
          }
      
          val scope = rememberCoroutineScope()
      
          var selectedType by remember {
      
              mutableStateOf<String?>(null)
          }
      
          LaunchedEffect(menu) {
      
              if (menu?.priceIce != null) {
      
                  selectedType = "Ice"
      
              } else if (menu?.priceHot != null) {
      
                  selectedType = "Hot"
              }
          }
      
          Scaffold(
      
              snackbarHost = {
      
                  SnackbarHost(hostState = snackbarHostState)
              },
      
              topBar = {
      
                  TopAppBar(
      
                      title = {
      
                          Text(
                              text = menu?.name ?: "Detail"
                          )
                      },
      
                      navigationIcon = {
      
                          IconButton(
      
                              onClick = {
      
                                  navController.navigateUp()
                              }
      
                          ) {
      
                              Icon(
      
                                  imageVector = Icons.Default.ArrowBack,
      
                                  contentDescription = "Back"
                              )
                          }
                      }
                  )
              }
      
          ) { padding ->
      
              Column(
      
                  modifier = Modifier
                      .padding(padding)
                      .fillMaxSize()
                      .padding(16.dp)
      
              ) {
      
                  Image(
      
                      painter = painterResource(
                          id = menu?.imageRes ?: 0
                      ),
      
                      contentDescription = menu?.name,
      
                      modifier = Modifier
                          .fillMaxWidth()
                          .height(260.dp),
      
                      contentScale = ContentScale.Crop
                  )
      
                  Spacer(modifier = Modifier.height(20.dp))
      
                  Text(
      
                      text = menu?.name ?: "",
      
                      style = MaterialTheme.typography.headlineSmall,
      
                      fontWeight = FontWeight.Bold
                  )
      
                  Spacer(modifier = Modifier.height(10.dp))
      
                  Text(
                      text = menu?.description ?: ""
                  )
      
                  Spacer(modifier = Modifier.height(20.dp))
      
                  Text(text = "⭐ ${menu?.rating}")
      
                      if (menu?.priceHot != null || menu?.priceIce != null) {
      
                          Text(
      
                              text = "Select Type",
      
                              fontWeight = FontWeight.Bold
                          )
      
                          Spacer(modifier = Modifier.height(12.dp))
      
                          Row(
      
                              horizontalArrangement = Arrangement.spacedBy(12.dp)
      
                          ) {
      
                              if (menu.priceHot != null) {
      
                                  FilterChip(
      
                                      selected = selectedType == "Hot",
      
                                      onClick = {
      
                                          selectedType = "Hot"
                                      },
      
                                      label = {
      
                                          Text("Hot")
                                      }
                                  )
                              }
      
                              if (menu.priceIce != null) {
      
                                  FilterChip(
      
                                      selected = selectedType == "Ice",
      
                                      onClick = {
      
                                          selectedType = "Ice"
                                      },
      
                                      label = {
      
                                          Text("Ice")
                                      }
                                  )
                              }
                          }
      
                          Spacer(modifier = Modifier.height(20.dp))
                      }
      
                  Spacer(modifier = Modifier.height(20.dp))
      
                  Text(
      
                      text = "Quantity",
      
                      fontWeight = FontWeight.Bold
                  )
      
                  Spacer(modifier = Modifier.height(12.dp))
      
                  Row(
      
                      horizontalArrangement = Arrangement.spacedBy(12.dp)
      
                  ) {
      
                      Button(
      
                          onClick = {
      
                              if (quantity > 1) {
                                  quantity--
                              }
                          }
      
                      ) {
      
                          Text("-")
                      }
      
                      Text(
      
                          text = quantity.toString(),
      
                          style = MaterialTheme.typography.titleLarge
                      )
      
                      Button(
      
                          onClick = {
      
                              quantity++
                          }
      
                      ) {
      
                          Text("+")
                      }
                  }
      
                  Spacer(modifier = Modifier.height(30.dp))
      
                  Button(
      
                      onClick = {
      
                          menu?.let {
      
                              viewModel.addToCart(
      
                                  it,
      
                                  selectedType = selectedType,
      
                                  quantity
                              )
                          }
      
                          scope.launch {
      
                              snackbarHostState.showSnackbar(
      
                                  "Ditambahkan ke Keranjang"
      
                              )
      
                              kotlinx.coroutines.delay(100)
                              navController.popBackStack()
                          }
      
                      },
      
                      modifier = Modifier.fillMaxWidth(),
      
                      shape = RoundedCornerShape(16.dp)
      
                  ) {
      
                      Text("Ditambahkan ke Keranjang")
                  }
              }
          }
      }
    
14. HomeScreen.kt
    ~~~kt
    package com.example.jospar.ui.screen.home

      import androidx.compose.foundation.layout.*
      import androidx.compose.foundation.lazy.LazyColumn
      import androidx.compose.foundation.lazy.LazyRow
      import androidx.compose.foundation.lazy.items
      import androidx.compose.material3.*
      import androidx.compose.runtime.*
      import androidx.compose.ui.Modifier
      import androidx.compose.ui.text.font.FontWeight
      import androidx.compose.ui.unit.dp
      import androidx.navigation.NavController
      import androidx.navigation.compose.currentBackStackEntryAsState
      import androidx.compose.foundation.Image
      import androidx.compose.ui.layout.ContentScale
      import androidx.compose.ui.res.painterResource
      import androidx.compose.foundation.Image
      import androidx.compose.ui.graphics.Color
      import androidx.compose.ui.res.painterResource
      import com.example.jospar.R
      import com.example.jospar.ui.component.BottomBar
      import com.example.jospar.ui.component.MenuCard
      import com.example.jospar.viewmodel.MenuViewModel
      
      @OptIn(ExperimentalMaterial3Api::class)
      @Composable
      fun HomeScreen(
      
          navController: NavController,
      
          viewModel: MenuViewModel
      
      ) {
      
          val menuList = viewModel.menuList
      
          var selectedCategory by remember {
              mutableStateOf("All")
          }
      
          val filteredMenu = if (selectedCategory == "All") {
      
              menuList
      
          } else {
      
              menuList.filter {
      
                  it.category == selectedCategory
              }
          }
      
          val categories = listOf(
      
              "All",
              "Coffee",
              "Milk",
              "Tea",
              "Snack",
              "Main Course"
          )
      
          val navBackStackEntry by navController.currentBackStackEntryAsState()
      
          val currentRoute = navBackStackEntry?.destination?.route
      
          Scaffold(
      
              bottomBar = {
      
                  BottomBar(
      
                      navController = navController,
      
                      currentRoute = currentRoute,
      
                      viewModel = viewModel
                  )
              }
      
          ) { padding ->
              Box(
      
                  modifier = Modifier.fillMaxSize()
      
              ) {
      
                  Image(
      
                      painter = painterResource(id = R.drawable.bg_coffee),
      
                      contentDescription = null,
      
                      modifier = Modifier.fillMaxSize(),
      
                      contentScale = ContentScale.Crop,
      
                      alpha = 0.15f
                  )
      
                  LazyColumn(
      
                      modifier = Modifier
                          .padding(padding)
                          .fillMaxSize()
                          .padding(16.dp),
      
                      verticalArrangement = Arrangement.spacedBy(16.dp)
      
                  ) {
      
                      if (viewModel.hasActiveOrder) {
      
                          item {
      
                              Card(
      
                                  colors = CardDefaults.cardColors(
      
                                      containerColor = Color(0xFF3E2723)
                                  )
      
                              ) {
      
                                  Column(
      
                                      modifier = Modifier.padding(16.dp)
      
                                  ) {
      
                                      Text(
      
                                          text = "Lihat Status Ordermu",
      
                                          fontWeight = FontWeight.Bold
                                      )
      
                                      Spacer(modifier = Modifier.height(8.dp))
      
                                      Button(
      
                                          onClick = {
      
                                              navController.navigate("tracking")
                                          }
      
                                      ) {
      
                                          Text("Lihat")
                                      }
                                  }
                              }
                          }
                      }
      
                      item {
      
                          LazyRow(
      
                              horizontalArrangement = Arrangement.spacedBy(12.dp)
      
                          ) {
      
                              items(categories) { category ->
      
                                  FilterChip(
      
                                      selected = selectedCategory == category,
      
                                      onClick = {
      
                                          selectedCategory = category
                                      },
      
                                      label = {
      
                                          Text(category)
                                      }
                                  )
                              }
                          }
                      }
      
                      items(filteredMenu) { menu ->
      
                          MenuCard(
      
                              menu = menu,
      
                              onClick = {
      
                                  navController.navigate(
                                      "detail/${menu.id}"
                                  )
                              }
                          )
                      }
                  }
              }
          }
      }
    
15. PaymentSuccessScreen.kt
    ~~~kt
    package com.example.jospar.ui.screen.payment

      import androidx.compose.foundation.layout.*
      import androidx.compose.material3.*
      import androidx.compose.runtime.Composable
      import androidx.compose.ui.Alignment
      import androidx.compose.ui.Modifier
      import androidx.compose.ui.graphics.Color
      import androidx.compose.ui.text.font.FontWeight
      import androidx.compose.ui.unit.dp
      import androidx.navigation.NavController
      
      @Composable
      fun PaymentSuccessScreen(
      
          navController: NavController
      
      ) {
      
          Column(
      
              modifier = Modifier
                  .fillMaxSize()
                  .padding(24.dp),
      
              horizontalAlignment = Alignment.CenterHorizontally,
      
              verticalArrangement = Arrangement.Center
      
          ) {
      
              Text(
      
                  text = "✅",
      
                  style = MaterialTheme.typography.displayLarge
              )
      
              Spacer(modifier = Modifier.height(20.dp))
      
              Text(
      
                  text = "Payment Success",
      
                  style = MaterialTheme.typography.headlineMedium,
      
                  fontWeight = FontWeight.Bold
              )
      
              Spacer(modifier = Modifier.height(12.dp))
      
              Text(
      
                  text = "Your order is being processed ☕",
      
                  color = Color.Gray
              )
      
              Spacer(modifier = Modifier.height(32.dp))
      
              Button(
      
                  onClick = {
      
                      navController.navigate("tracking")
                  },
      
                  modifier = Modifier.fillMaxWidth()
      
              ) {
      
                  Text("Track Order")
              }
          }
      }
    
16. SplashScreen.kt
    ~~~kt
    package com.example.jospar.ui.screen.splash

      import androidx.compose.animation.core.*
      import androidx.compose.foundation.background
      import androidx.compose.foundation.layout.*
      import androidx.compose.material3.MaterialTheme
      import androidx.compose.material3.Text
      import androidx.compose.runtime.*
      import androidx.compose.ui.Alignment
      import androidx.compose.ui.Modifier
      import androidx.compose.ui.draw.alpha
      import androidx.compose.ui.graphics.Brush
      import androidx.compose.ui.graphics.Color
      import androidx.compose.ui.text.font.FontWeight
      import androidx.compose.ui.unit.dp
      import androidx.navigation.NavController
      import kotlinx.coroutines.delay
      
      @Composable
      fun SplashScreen(
      
          navController: NavController
      
      ) {
      
          var startAnimation by remember {
      
              mutableStateOf(false)
          }
      
          val alphaAnim by animateFloatAsState(
      
              targetValue = if (startAnimation) 1f else 0f,
      
              animationSpec = tween(
                  durationMillis = 1800
              ),
      
              label = ""
          )
      
          LaunchedEffect(Unit) {
      
              startAnimation = true
      
              delay(2500)
      
              navController.navigate("home") {
      
                  popUpTo("splash") {
      
                      inclusive = true
                  }
              }
          }
      
          Box(
      
              modifier = Modifier
                  .fillMaxSize()
                  .background(
      
                      brush = Brush.verticalGradient(
      
                          colors = listOf(
      
                              Color(0xFF2D1B16),
      
                              Color(0xFF4E342E)
                          )
                      )
                  ),
      
              contentAlignment = Alignment.Center
      
          ) {
      
              Column(
      
                  horizontalAlignment = Alignment.CenterHorizontally,
      
                  modifier = Modifier.alpha(alphaAnim)
      
              ) {
      
                  Text(
      
                      text = "☕",
      
                      style = MaterialTheme.typography.displayLarge
                  )
      
                  Spacer(modifier = Modifier.height(20.dp))
      
                  Text(
      
                      text = "JOSPAR COFFEE",
      
                      style = MaterialTheme.typography.headlineLarge,
      
                      color = Color.White,
      
                      fontWeight = FontWeight.Bold
                  )
      
                  Spacer(modifier = Modifier.height(10.dp))
      
                  Text(
      
                      text = "Brewing Happiness",
      
                      color = Color(0xFFD7A16A)
                  )
              }
          }
      }
    
17. SuccessScreen.kt
    ~~~kt
    package com.example.jospar.ui.screen.success

      import androidx.compose.foundation.layout.*
      import androidx.compose.material3.*
      import androidx.compose.runtime.Composable
      import androidx.compose.runtime.LaunchedEffect
      import androidx.compose.ui.Alignment
      import androidx.compose.ui.Modifier
      import androidx.compose.ui.text.font.FontWeight
      import androidx.compose.ui.unit.dp
      import androidx.navigation.NavController
      import com.example.jospar.viewmodel.MenuViewModel
      
      
      
      @Composable
      fun SuccessScreen(
      
          navController: NavController,
      
          viewModel: MenuViewModel
      
      ) {
          LaunchedEffect(Unit) {
      
              viewModel.clearCart()
          }
      
          Column(
      
              modifier = Modifier
                  .fillMaxSize()
                  .padding(24.dp),
      
              verticalArrangement = Arrangement.Center,
      
              horizontalAlignment = Alignment.CenterHorizontally
      
          ) {
      
              Text(
      
                  text = "🎉",
      
                  style = MaterialTheme.typography.displayLarge
              )
      
              Spacer(modifier = Modifier.height(24.dp))
      
              Text(
      
                  text = "Order Success!",
      
                  style = MaterialTheme.typography.headlineMedium,
      
                  fontWeight = FontWeight.Bold
              )
      
              Spacer(modifier = Modifier.height(12.dp))
      
              Text(
      
                  text = "Pesanan kamu sedang diproses"
              )
      
              Spacer(modifier = Modifier.height(32.dp))
      
              Button(
      
                  onClick = {
      
                      navController.navigate("tracking")
                  },
      
                  modifier = Modifier.fillMaxWidth()
      
              ) {
      
                  Text("Track Order")
              }
      
              Spacer(modifier = Modifier.height(12.dp))
      
              OutlinedButton(
      
                  onClick = {
      
                      navController.navigate("home") {
      
                          popUpTo("home") {
      
                              inclusive = true
                          }
                      }
                  },
      
                  modifier = Modifier.fillMaxWidth()
      
              ) {
      
                  Text("Back To Home")
              }
          }
      }
    
18. TrackingScreen.kt
    ~~~kt
    package com.example.jospar.ui.screen.tracking

      import androidx.compose.foundation.layout.*
      import androidx.compose.foundation.layout.Arrangement
      import androidx.compose.material.icons.Icons
      import androidx.compose.material.icons.filled.ArrowBack
      import androidx.compose.material3.*
      import androidx.compose.runtime.*
      import androidx.compose.ui.Modifier
      import androidx.compose.ui.text.font.FontWeight
      import androidx.compose.ui.unit.dp
      import androidx.navigation.NavController
      import androidx.compose.material.icons.filled.CheckCircle
      import androidx.compose.material.icons.filled.Coffee
      import androidx.compose.material.icons.filled.DoneAll
      import androidx.compose.ui.graphics.Color
      import com.example.jospar.viewmodel.MenuViewModel
      import kotlinx.coroutines.delay
      
      @OptIn(ExperimentalMaterial3Api::class)
      @Composable
      fun TrackingScreen(
      
          navController: NavController,
          viewModel: MenuViewModel
      
      ) {
      
          if (!viewModel.hasActiveOrder) {
      
              LaunchedEffect(Unit) {
      
                  navController.navigate("home")
              }
      
              return
          }
      
          var status by remember {
      
              mutableStateOf("Pesanan Diterima")
          }
      
          LaunchedEffect(Unit) {
      
              delay(4000)
      
              status = "Sedang Dibuat"
      
              delay(4000)
      
              status = "Siap Diambil"
      
              viewModel.finishOrder()
          }
      
          Scaffold(
      
              topBar = {
      
                  TopAppBar(
      
                      title = {
      
                          Text("Order Tracking")
                      },
      
                      navigationIcon = {
      
                          IconButton(
      
                              onClick = {
      
                                  navController.navigateUp()
                              }
      
                          ) {
      
                              Icon(
      
                                  imageVector = Icons.Default.ArrowBack,
      
                                  contentDescription = "Back"
                              )
                          }
                      }
                  )
              }
      
          ) { padding ->
      
              Column(
      
                  modifier = Modifier
                      .padding(padding)
                      .fillMaxSize()
                      .padding(24.dp),
      
                  verticalArrangement = Arrangement.Top
      
              ) {
      
      
                  Spacer(modifier = Modifier.height(40.dp))
      
                  TrackingItem(
      
                      title = "Order Received",
      
                      active = true,
      
                      completed = true,
      
                      icon = {
      
                          Icon(
      
                              imageVector = Icons.Default.CheckCircle,
      
                              contentDescription = null,
      
                              tint = Color(0xFFD7A16A)
                          )
                      }
                  )
      
                  TrackingLine()
      
                  TrackingItem(
      
                      title = "Brewing Coffee",
      
                      active = status == "Sedang Dibuat" || status == "Siap Diambil",
      
                      completed = status == "Siap Diambil",
      
                      icon = {
      
                          Icon(
      
                              imageVector = Icons.Default.Coffee,
      
                              contentDescription = null,
      
                              tint = if (
                                  status == "Sedang Dibuat" ||
                                  status == "Siap Diambil"
                              ) {
                                  Color(0xFFD7A16A)
                              } else {
                                  Color.Gray
                              }
                          )
                      }
                  )
      
                  TrackingLine()
      
                  TrackingItem(
      
                      title = "Ready To Pick Up",
      
                      active = status == "Siap Diambil",
      
                      completed = status == "Siap Diambil",
      
                      icon = {
      
                          Icon(
      
                              imageVector = Icons.Default.DoneAll,
      
                              contentDescription = null,
      
                              tint = if (status == "Siap Diambil") {
      
                                  Color(0xFFD7A16A)
      
                              } else {
      
                                  Color.Gray
                              }
                          )
                      }
                  )
              }
          }
      }
      
      @Composable
      fun TrackingItem(
      
          title: String,
      
          active: Boolean,
      
          completed: Boolean,
      
          icon: @Composable () -> Unit
      
      ) {
      
          Row(
      
              horizontalArrangement = Arrangement.spacedBy(16.dp)
      
          ) {
      
              Card(
      
                  colors = CardDefaults.cardColors(
      
                      containerColor = if (active) {
      
                          Color(0xFF3E2723)
      
                      } else {
      
                          Color.DarkGray
                      }
                  )
      
              ) {
      
                  Box(
      
                      modifier = Modifier.padding(16.dp)
      
                  ) {
      
                      icon()
                  }
              }
      
              Column {
      
                  Text(
      
                      text = title,
      
                      fontWeight = FontWeight.Bold
                  )
      
                  Text(
      
                      text = when {
      
                          completed -> "Completed"
      
                          active -> "In Progress"
      
                          else -> "Waiting"
                      }
                  )
              }
          }
      }
      
      @Composable
      fun TrackingLine() {
      
          Box(
      
              modifier = Modifier
                  .padding(start = 20.dp)
                  .width(2.dp)
                  .height(40.dp)
          ) {
      
              Divider(
      
                  thickness = 2.dp,
      
                  color = Color.Gray
              )
          }
      }

19. Color.kt
    ~~~kt
    package com.example.jospar.ui.theme

      import androidx.compose.ui.graphics.Color
      
      val EspressoBlack = Color(0xFF0F0B09)
      
      val CoffeeDark = Color(0xFF1B1411)
      
      val CoffeeCard = Color(0xFF2A211D)
      
      val Caramel = Color(0xFFC68B59)
      
      val LatteBrown = Color(0xFFD7B08A)
      
      val Cream = Color(0xFFF6E7D8)
      
      val SoftWhite = Color(0xFFF8F5F2)
      
      val SuccessGreen = Color(0xFF4CAF50)
      
      val ErrorRed = Color(0xFFE53935)
      
      val BorderColor = Color(0xFF4A3B33)
    
20. Theme.kt
    ~~~kt
    package com.example.jospar.ui.theme

      import android.os.Build
      import androidx.compose.material3.*
      import androidx.compose.runtime.Composable
      import androidx.compose.ui.platform.LocalContext
      
      private val DarkColorScheme = darkColorScheme(
      
          primary = Caramel,
          secondary = LatteBrown,
          tertiary = Cream,
      
          background = CoffeeDark,
          surface = CoffeeCard,
      
          onPrimary = SoftWhite,
          onSecondary = SoftWhite,
          onTertiary = EspressoBlack,
      
          onBackground = SoftWhite,
          onSurface = SoftWhite
      )
      
      @Composable
      fun JosparCoffeeTheme(
          darkTheme: Boolean = true,
          dynamicColor: Boolean = false,
          content: @Composable () -> Unit
      ) {
      
          val colorScheme = when {
      
              dynamicColor && Build.VERSION.SDK_INT >= Build.VERSION_CODES.S -> {
      
                  val context = LocalContext.current
      
                  if (darkTheme)
                      dynamicDarkColorScheme(context)
                  else
                      dynamicLightColorScheme(context)
              }
      
              else -> DarkColorScheme
          }
      
          MaterialTheme(
              colorScheme = colorScheme,
              typography = Typography,
              content = content
          )
      }

21. Type.kt
    ~~~kt
    package com.example.jospar.ui.theme

      import androidx.compose.material3.Typography
      import androidx.compose.ui.text.TextStyle
      import androidx.compose.ui.text.font.FontFamily
      import androidx.compose.ui.text.font.FontWeight
      import androidx.compose.ui.unit.sp
      
      val Typography = Typography(
      
          headlineLarge = TextStyle(
              fontFamily = FontFamily.SansSerif,
              fontWeight = FontWeight.Bold,
              fontSize = 32.sp
          ),
      
          headlineMedium = TextStyle(
              fontFamily = FontFamily.SansSerif,
              fontWeight = FontWeight.Bold,
              fontSize = 26.sp
          ),
      
          headlineSmall = TextStyle(
              fontFamily = FontFamily.SansSerif,
              fontWeight = FontWeight.SemiBold,
              fontSize = 22.sp
          ),
      
          titleLarge = TextStyle(
              fontFamily = FontFamily.SansSerif,
              fontWeight = FontWeight.Bold,
              fontSize = 20.sp
          ),
      
          titleMedium = TextStyle(
              fontFamily = FontFamily.SansSerif,
              fontWeight = FontWeight.SemiBold,
              fontSize = 18.sp
          ),
      
          bodyLarge = TextStyle(
              fontFamily = FontFamily.SansSerif,
              fontWeight = FontWeight.Normal,
              fontSize = 16.sp
          ),
      
          bodyMedium = TextStyle(
              fontFamily = FontFamily.SansSerif,
              fontWeight = FontWeight.Normal,
              fontSize = 14.sp
          ),
      
          labelLarge = TextStyle(
              fontFamily = FontFamily.SansSerif,
              fontWeight = FontWeight.Bold,
              fontSize = 14.sp
          )
      )
    
22. MenuViewModel.kt
    ~~~kt
    package com.example.jospar.viewmodel

      import androidx.compose.runtime.mutableStateListOf
      import androidx.compose.runtime.mutableStateOf
      import androidx.lifecycle.ViewModel
      import androidx.compose.runtime.getValue
      import androidx.compose.runtime.setValue
      import androidx.lifecycle.viewModelScope
      import com.example.jospar.data.MenuRepository
      import com.example.jospar.model.MenuItem
      import com.example.jospar.model.CartItem
      import com.example.jospar.network.RetrofitInstance
      import com.example.jospar.data.OrderPreferences
      import kotlinx.coroutines.launch
      
      class MenuViewModel : ViewModel() {
      
          val menuList = MenuRepository.menuList
      
          var cartItems = mutableStateListOf<CartItem>()
              private set
      
          var hasActiveOrder by mutableStateOf(false)
      
          lateinit var orderPreferences: OrderPreferences
      
      
          fun addToCart(
      
              menu: MenuItem,
      
              selectedType: String?,
      
              quantity: Int
      
              ) {
      
              val exitingItem = cartItems.find {
      
                  it.menu.id == menu.id &&
                          it.selectedType == selectedType
              }
      
              if (exitingItem != null) {
      
                  exitingItem.quantity += quantity
      
              } else {
      
                  cartItems.add(
      
                      CartItem(
                          menu = menu,
                          selectedType = selectedType,
                          quantity = quantity
                      )
                  )
              }
          }
      
      
      
          fun removeFromCart(cartItem: CartItem) {
      
              cartItems.remove(cartItem)
          }
      
          fun increaseQuantity(cartItem: CartItem) {
      
              cartItem.quantity++
          }
      
          fun decreaseQuantity(cartItem: CartItem) {
      
              if (cartItem.quantity > 1) {
      
                  cartItem.quantity--
      
              } else {
      
                  cartItems.remove(cartItem)
              }
          }
      
          fun checkout() {
      
              hasActiveOrder = true
              cartItems.clear()
              viewModelScope.launch {
                  orderPreferences.saveOrderStatus(true)
              }
          }
      
          fun finishOrder () {
      
              hasActiveOrder = false
              viewModelScope.launch {
                  orderPreferences.saveOrderStatus(false)
              }
      
          }
      
          fun createTransaction(
      
              totalAmount: Int,
              itemsJson: String,
              onResult: (String?) -> Unit
          ) {
      
              viewModelScope.launch {
      
                  try {
      
                      val response =
                          RetrofitInstance.api.createTransaction(
                              totalAmount,
                              itemsJson
                          )
      
                      println("RESPONSE = ${response.body()}")
      
                      if (response.isSuccessful) {
      
                          onResult(response.body()?.string())
      
                      } else {
      
                          println("ERROR CODE = ${response.code()}")
      
                          onResult(null)
                      }
      
                  } catch (e: Exception) {
      
                      e.printStackTrace()
      
                      println("ERROR = ${e.message}")
      
                      onResult(null)
                  }
              }
          }
      
          fun clearCart() {
      
              cartItems.clear()
          }
      }

23. MainActivity.kt
    ~~~kt
    package com.example.jospar

      import android.os.Bundle
      import androidx.activity.ComponentActivity
      import androidx.activity.compose.setContent
      import androidx.compose.material3.MaterialTheme
      import androidx.compose.material3.Surface
      import androidx.lifecycle.viewmodel.compose.viewModel
      import androidx.lifecycle.lifecycleScope
      import kotlinx.coroutines.launch
      import com.example.jospar.navigation.AppNavigation
      import com.example.jospar.ui.theme.JosparCoffeeTheme
      import com.example.jospar.viewmodel.MenuViewModel
      import com.example.jospar.data.OrderPreferences
      
      class MainActivity : ComponentActivity() {
      
          override fun onCreate(savedInstanceState: Bundle?) {
              super.onCreate(savedInstanceState)
      
              setContent {
      
                  val viewModel: MenuViewModel = viewModel()
      
                  viewModel.orderPreferences =
      
                      OrderPreferences(this)
      
                  lifecycleScope.launch {
      
                      viewModel.orderPreferences.orderStatus.collect {
      
                          viewModel.hasActiveOrder = it
                      }
                  }
      
                  JosparCoffeeTheme {
      
                      Surface(
                          color = MaterialTheme.colorScheme.background
                      ) {
      
                          AppNavigation(viewModel)
                      }
                  }
              }
          }
      }
