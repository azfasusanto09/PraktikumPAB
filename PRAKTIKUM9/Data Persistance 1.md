# Tugas Praktikum 9: Data Persistence 1

## Kelompok 5:
1. Azfa Rahma Putra Susanto (L0324008)
2. Hammam Ibnu Adi'Abdillah (L0324015)
3. Indra Fata Azhari L0324017)

Jadi dari project sebelumnya ada beberapa perubahan yang banyak merubah struktur dari project kami.

## Source Code yang digunakan:

###
1. com.example.josparcoffee/data/Cart.kt
   ~~~kt
    package com.example.josparcoffee.data
    
    import androidx.compose.runtime.mutableStateListOf
    import androidx.compose.runtime.mutableStateOf
    import androidx.compose.runtime.getValue
    import androidx.compose.runtime.setValue
    
    class CartItem(
        val item: MenuItem,
        val variant: String,
        quantity: Int = 1
    ) {
        var quantity by mutableStateOf(quantity)
    }
    
    object CartManager {
        val cartItems = mutableStateListOf<CartItem>()
    
        fun addToCart(item: MenuItem, variant: String) {
            val existing = cartItems.find {
                it.item.name == item.name && it.variant == variant
            }
    
            if (existing != null) {
                existing.quantity++
            } else {
                cartItems.add(CartItem(item, variant))
            }
        }
    
        fun removeItem(cartItem: CartItem) {
            cartItems.remove(cartItem)
        }
    
        fun increase(cartItem: CartItem) {
            cartItem.quantity++
        }
    
        fun decrease(cartItem: CartItem) {
            if (cartItem.quantity >1) {
                cartItem.quantity--
            } else {
                cartItems.remove(cartItem)
            }
        }
    
        fun getTotal(): Int {
            return cartItems.sumOf {
                val price = when (it.variant) {
                    "Hot" -> it.item.priceHot?.toIntOrNull() ?: 0
                    "Ice" -> it.item.priceIce?.toIntOrNull() ?: 0
                    else -> it.item.price?.toIntOrNull() ?: 0
                }
                price * it.quantity
            }
        }
    }

   
2. com.example.josparcoffee/data/Coffee.kt
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
        MenuItem("Jasmine Tea", null ,"18", "18", "Tea",R.drawable.japanese_tea),
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

  
3. com.example.josparcoffee/navigation/AppNavigation.kt
   ~~~kt   
    package com.example.josparcoffee.navigation
    
    import androidx.compose.runtime.*
    import androidx.compose.runtime.mutableStateListOf
    import androidx.compose.runtime.staticCompositionLocalOf
    import com.example.josparcoffee.data.MenuItem
    import com.example.josparcoffee.ui.screen.home.HomeScreen
    import com.example.josparcoffee.ui.screen.menu.MenuScreen
    import com.example.josparcoffee.ui.screen.profile.ProfileScreen
    import com.example.josparcoffee.ui.screen.detail.DetailScreen
    import com.example.josparcoffee.ui.screen.cart.CartScreen
    import com.example.josparcoffee.ui.screen.checkout.CheckoutScreen
    
    sealed class Routes {
        object Home : Routes()
        object Menu : Routes()
        object Profile : Routes()
        object Cart : Routes()
        object Checkout : Routes()
        data class Detail(val item: MenuItem) : Routes()
    }
    
    val LocalBackStack = staticCompositionLocalOf<MutableList<Routes>> {
        error("BackStack belum ada")
    }
    
    @Composable
    fun AppNavigation() {
        val backStack = remember {
            mutableStateListOf<Routes>(Routes.Home)
        }
    
        CompositionLocalProvider(LocalBackStack provides backStack) {
            NavDisplay()
        }
    }
    
    @Composable
    fun NavDisplay() {
        val backStack = LocalBackStack.current
        val current = backStack.last()
    
        when (current) {
            is Routes.Home -> HomeScreen()
            is Routes.Menu -> MenuScreen()
            is Routes.Profile -> ProfileScreen()
            is Routes.Cart -> CartScreen()
            is Routes.Detail -> DetailScreen(item = current.item)
            is Routes.Checkout -> CheckoutScreen()
        }
    }

   
4. com.example.josparcoffee/ui/component/MenuItemCard.kt
   ~~~kt
    package com.example.josparcoffee.ui.component
    
    import androidx.compose.foundation.Image
    import androidx.compose.foundation.clickable
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
    import com.example.josparcoffee.data.MenuItem
    
    @Composable
    fun MenuItemCard(
        item: MenuItem,
        onClick: () -> Unit
    ) {
        Card(
            modifier = Modifier
                .fillMaxWidth()
                .padding(vertical = 6.dp)
                .clickable { onClick() },
            shape = RoundedCornerShape(16.dp)
        ) {
            Row(
                modifier = Modifier.padding(12.dp),
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
                    item.priceHot?.let { Text("Hot: $it.k") }
                    item.priceIce?.let { Text("Ice: $it.k") }
                    item.price?.let { Text("$it.k") }
                }
            }
        }
    }


5. com.example.josparcoffee/ui/screen/cart/CartScreen.kt
   ~~~kt
    package com.example.josparcoffee.ui.screen.cart
    
    import androidx.compose.foundation.layout.*
    import androidx.compose.foundation.lazy.*
    import androidx.compose.material.icons.Icons
    import androidx.compose.material.icons.filled.ArrowBack
    import androidx.compose.material3.*
    import androidx.compose.runtime.*
    import androidx.compose.ui.Modifier
    import androidx.compose.ui.unit.dp
    import com.example.josparcoffee.data.*
    import com.example.josparcoffee.navigation.*
    
    @OptIn(ExperimentalMaterial3Api::class)
    @Composable
    fun CartScreen() {
    
        var selectedItem by remember { mutableStateOf<CartItem?>(null) }
        var showDialog by remember { mutableStateOf(false) }
    
        val backStack = LocalBackStack.current
        val cartItems = CartManager.cartItems
    
        Scaffold(
            topBar = {
                TopAppBar(
                    title = { Text("Keranjang") },
                    navigationIcon = {
                        IconButton(onClick = {
                            backStack.removeLastOrNull()
                        }) {
                            Icon(Icons.Default.ArrowBack, null)
                        }
                    }
                )
            }
        ) { padding ->
    
            Column(
                modifier = Modifier
                    .fillMaxSize()
                    .padding(padding)
            ) {
    
                // LIST ITEM
                LazyColumn(
                    modifier = Modifier
                        .weight(1f)
                        .padding(horizontal = 8.dp)
                ) {
                    items(cartItems) { cartItem ->
    
                        val price = when (cartItem.variant) {
                            "Hot" -> cartItem.item.priceHot
                            "Ice" -> cartItem.item.priceIce
                            else -> cartItem.item.price
                        }?.toIntOrNull() ?: 0
    
                        Card(
                            modifier = Modifier
                                .fillMaxWidth()
                                .padding(vertical = 6.dp),
                            elevation = CardDefaults.cardElevation(4.dp)
                        ) {
                            Column(modifier = Modifier.padding(12.dp)) {
    
                                Text(
                                    text = cartItem.item.name,
                                    style = MaterialTheme.typography.titleMedium
                                )
    
                                Text("Tipe: ${cartItem.variant}")
                                Text("Harga: Rp $price.000")
                                Text("Qty: ${cartItem.quantity}")
                                Text("Subtotal: Rp ${price * cartItem.quantity}.000")
    
                                Spacer(modifier = Modifier.height(8.dp))
    
                                Row {
    
                                    Button(onClick = {
                                        CartManager.increase(cartItem)
                                    }) {
                                        Text("+")
                                    }
    
                                    Spacer(modifier = Modifier.width(8.dp))
    
                                    Button(onClick = {
                                        CartManager.decrease(cartItem)
                                    }) {
                                        Text("-")
                                    }
    
                                    Spacer(modifier = Modifier.width(8.dp))
    
                                    Button(onClick = {
                                        selectedItem = cartItem
                                        showDialog = true
                                    }) {
                                        Text("Hapus")
                                    }
                                }
                            }
                        }
                    }
                }
    
                // CHECKOUT 
                Card(
                    modifier = Modifier
                        .fillMaxWidth()
                        .padding(16.dp),
                    elevation = CardDefaults.cardElevation(8.dp)
                ) {
                    Column(modifier = Modifier.padding(16.dp)) {
    
                        Text(
                            "Total: Rp ${CartManager.getTotal()}.000",
                            style = MaterialTheme.typography.titleLarge
                        )
    
                        Spacer(modifier = Modifier.height(8.dp))
    
                        Button(
                            onClick = {
                                backStack.add(Routes.Checkout)
                            },
                            modifier = Modifier.fillMaxWidth()
                        ) {
                            Text("Checkout")
                        }
                    }
                }
            }
        }
    
        // ALERT DIALOG
        if (showDialog && selectedItem != null) {
            AlertDialog(
                onDismissRequest = { showDialog = false },
                title = { Text("Hapus Item") },
                text = { Text("Yakin mau hapus dari keranjang?") },
                confirmButton = {
                    Button(onClick = {
                        CartManager.removeItem(selectedItem!!)
                        showDialog = false
                    }) {
                        Text("Hapus")
                    }
                },
                dismissButton = {
                    OutlinedButton(onClick = {
                        showDialog = false
                    }) {
                        Text("Batal")
                    }
                }
            )
        }
    }


6. com.example.josparcoffee/ui/screen/detail/DetailScreen.kt
   ~~~kt
    package com.example.josparcoffee.ui.screen.detail
    
    
    import androidx.compose.animation.core.animateFloatAsState
    import androidx.compose.animation.core.tween
    import androidx.compose.foundation.Image
    import androidx.compose.foundation.clickable
    import androidx.compose.foundation.layout.*
    import androidx.compose.material.icons.Icons
    import androidx.compose.material.icons.filled.ArrowBack
    import androidx.compose.material3.*
    import androidx.compose.material3.ModalBottomSheet
    import androidx.compose.material3.rememberModalBottomSheetState
    import androidx.compose.runtime.*
    import androidx.compose.ui.Alignment
    import androidx.compose.ui.Modifier
    import androidx.compose.ui.res.painterResource
    import androidx.compose.ui.unit.dp
    import kotlinx.coroutines.launch
    import com.example.josparcoffee.data.MenuItem
    import com.example.josparcoffee.data.CartManager
    import com.example.josparcoffee.navigation.LocalBackStack
    
    @OptIn(ExperimentalMaterial3Api::class)
    @Composable
    fun DetailScreen(item: MenuItem) {
    
        // STATE
        var showSheet by remember { mutableStateOf(false) }
    
        val snackbarHostState = remember { SnackbarHostState() }
        val scope = rememberCoroutineScope()
        val sheetState = rememberModalBottomSheetState()
    
        val backStack = LocalBackStack.current
    
        val cartItems = CartManager.cartItems
        val isInCart = cartItems.any { it.item.name == item.name }
    
        val scale by animateFloatAsState(
            targetValue = if (isInCart) 1.1f else 1f,
            animationSpec = tween(300),
            label = ""
        )
    
        // UI
        Scaffold(
            snackbarHost = { SnackbarHost(snackbarHostState) },
            topBar = {
                TopAppBar(
                    title = { Text("Detail Menu") },
                    navigationIcon = {
                        IconButton(onClick = {
                            backStack.removeLastOrNull()
                        }) {
                            Icon(Icons.Default.ArrowBack, contentDescription = null)
                        }
                    }
                )
            }
        ) { padding ->
    
            Column(
                modifier = Modifier
                    .fillMaxSize()
                    .padding(padding)
                    .padding(16.dp),
                horizontalAlignment = Alignment.CenterHorizontally
            ) {
    
                // IMAGE
                Image(
                    painter = painterResource(id = item.imageRes),
                    contentDescription = item.name,
                    modifier = Modifier.size(200.dp)
                )
    
                Spacer(modifier = Modifier.height(16.dp))
    
                // NAME
                Text(
                    text = item.name,
                    style = MaterialTheme.typography.headlineMedium
                )
    
                Spacer(modifier = Modifier.height(8.dp))
    
                // PRICE
                item.priceHot?.let { Text("Hot: Rp $it.000") }
                item.priceIce?.let { Text("Ice: Rp $it.000") }
                item.price?.let { Text("Rp $it.000") }
    
                Spacer(modifier = Modifier.height(24.dp))
    
                // BUTTON
                Button(
                    onClick = {
                        if (item.priceHot != null && item.priceIce != null) {
                            showSheet = true
                        } else {
                            CartManager.addToCart(item, "-")
    
                            scope.launch {
                                snackbarHostState.showSnackbar("Menu ditambahkan ke keranjang")
                            }
                        }
                    }
                ) {
                    Text("Tambah ke Keranjang")
                }
            }
        }
    
        // MODERN BOTTOM SHEET
        if (showSheet) {
            ModalBottomSheet(
                onDismissRequest = { showSheet = false },
                sheetState = sheetState
            ) {
    
                Column(
                    modifier = Modifier
                        .fillMaxWidth()
                        .padding(16.dp)
                ) {
    
                    Text(
                        text = "Pilih Varian ",
                        style = MaterialTheme.typography.titleLarge
                    )
    
                    Spacer(modifier = Modifier.height(16.dp))
    
                    // HOT
                    Card(
                        modifier = Modifier
                            .fillMaxWidth()
                            .padding(vertical = 6.dp)
                            .clickable {
                                CartManager.addToCart(item, "Hot")
                                showSheet = false
    
                                scope.launch {
                                    snackbarHostState.showSnackbar("Hot ditambahkan ke keranjang")
                                }
                            }
                    ) {
                        Row(
                            modifier = Modifier
                                .fillMaxWidth()
                                .padding(16.dp),
                            horizontalArrangement = Arrangement.SpaceBetween
                        ) {
                            Text("Hot")
                            Text("Rp ${item.priceHot ?: "-"}.000")
                        }
                    }
    
                    // ICE
                    Card(
                        modifier = Modifier
                            .fillMaxWidth()
                            .padding(vertical = 6.dp)
                            .clickable {
                                CartManager.addToCart(item, "Ice")
                                showSheet = false
    
                                scope.launch {
                                    snackbarHostState.showSnackbar("Ice ditambahkan ke keranjang")
                                }
                            }
                    ) {
                        Row(
                            modifier = Modifier
                                .fillMaxWidth()
                                .padding(16.dp),
                            horizontalArrangement = Arrangement.SpaceBetween
                        ) {
                            Text("Ice")
                            Text("Rp ${item.priceIce ?: "-"}.000")
                        }
                    }
    
                    Spacer(modifier = Modifier.height(20.dp))
                }
            }
        }
    }


7. com.example.josparcoffee/ui/screen/home/HomeScreen.kt
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
    import com.example.josparcoffee.R
    import com.example.josparcoffee.navigation.*
    
    
    @Composable
    fun HomeScreen() {
    
        val backStack =  LocalBackStack.current
    
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
    
                Button(onClick = { backStack.add(Routes.Menu) }) {
                    Text("Lihat Menu")
                }
    
                OutlinedButton(onClick = { backStack.add(Routes.Profile) }) {
                    Text("Profile Coffee")
                }
            }
        }
    }


8. com.example.josparcoffee/ui/screen/menu/MenuScreen.kt
   ~~~kt
    package com.example.josparcoffee.ui.screen.menu
    
    import androidx.compose.foundation.layout.*
    import androidx.compose.foundation.lazy.LazyColumn
    import androidx.compose.foundation.lazy.items
    import androidx.compose.material.icons.Icons
    import androidx.compose.material.icons.filled.ShoppingCart
    import androidx.compose.material3.*
    import androidx.compose.runtime.Composable
    import androidx.compose.ui.Modifier
    import androidx.compose.ui.unit.dp
    import com.example.josparcoffee.data.menuList
    import com.example.josparcoffee.navigation.*
    import com.example.josparcoffee.ui.component.MenuItemCard
    
    @OptIn(ExperimentalMaterial3Api::class)
    @Composable
    fun MenuScreen() {
    
        val backStack = LocalBackStack.current
        val groupedMenu = menuList.groupBy { it.category.toString() }
    
        Scaffold(
            topBar = {
                TopAppBar(title = { Text("Menu Coffee") })
            },
            floatingActionButton = {
                FloatingActionButton(onClick = {
                    backStack.add(Routes.Cart)
                }) {
                    Icon(Icons.Default.ShoppingCart, contentDescription = "Cart")
                }
            }
        ) { padding ->
    
            LazyColumn(
                modifier = Modifier
                    .fillMaxSize()
                    .padding(padding)
                    .padding(16.dp)
            ) {
    
                groupedMenu.forEach { (category, items) ->
    
                    item {
                        Text(category, style = MaterialTheme.typography.titleLarge)
                        Divider()
                    }
    
                    items(items) { item ->
                        MenuItemCard(
                            item = item,
                            onClick = {
                                backStack.add(Routes.Detail(item))
                            }
                        )
                    }
                }
            }
        }
    }


9. com.example.josparcoffee/ui/screen/profile/ProfileScreen.kt
    ~~~kt
    package com.example.josparcoffee.ui.screen.profile
    
    import androidx.compose.foundation.layout.*
    import androidx.compose.material3.*
    import androidx.compose.runtime.Composable
    import androidx.compose.ui.Alignment
    import androidx.compose.ui.Modifier
    import androidx.compose.ui.text.style.TextAlign
    import androidx.compose.ui.unit.dp
    import com.example.josparcoffee.navigation.LocalBackStack
    
    @Composable
    fun ProfileScreen() {
    
        val backStack = LocalBackStack.current
    
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
    
            Button(onClick = {
                backStack.removeLastOrNull()
            }) {
                Text("Kembali")
            }
        }
    }


10. com.example.josparcoffee/theme/Color.kt
    ~~~kt
    package com.example.josparcoffee.ui.theme
    
    import androidx.compose.ui.graphics.Color
    
    val Purple80 = Color(0xFFD0BCFF)
    val PurpleGrey80 = Color(0xFFCCC2DC)
    val Pink80 = Color(0xFFEFB8C8)
    
    val Purple40 = Color(0xFF6650a4)
    val PurpleGrey40 = Color(0xFF625b71)
    val Pink40 = Color(0xFF7D5260)


11. com.example.josparcoffee/theme/Theme.kt
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


12. com.example.josparcoffee/theme/Type.kt
    ~~~kt
    package com.example.josparcoffee.ui.theme
    
    import androidx.compose.material3.Typography
    import androidx.compose.ui.text.TextStyle
    import androidx.compose.ui.text.font.FontFamily
    import androidx.compose.ui.text.font.FontWeight
    import androidx.compose.ui.unit.sp
    
    // Set of Material typography styles to start with
    val Typography = Typography(
        bodyLarge = TextStyle(
            fontFamily = FontFamily.Default,
            fontWeight = FontWeight.Normal,
            fontSize = 16.sp,
            lineHeight = 24.sp,
            letterSpacing = 0.5.sp
        )
        /* Other default text styles to override
        titleLarge = TextStyle(
            fontFamily = FontFamily.Default,
            fontWeight = FontWeight.Normal,
            fontSize = 22.sp,
            lineHeight = 28.sp,
            letterSpacing = 0.sp
        ),
        labelSmall = TextStyle(
            fontFamily = FontFamily.Default,
            fontWeight = FontWeight.Medium,
            fontSize = 11.sp,
            lineHeight = 16.sp,
            letterSpacing = 0.5.sp
        )
        */
    )


13. com.example.josparcoffee/MainActivity.kt
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


14. com.example.josparcoffee/ui/screen/checkout/CheckoutScreen.kt
    ~~~kt
      package com.example.josparcoffee.ui.screen.checkout
      
      import androidx.compose.foundation.layout.*
      import androidx.compose.foundation.lazy.LazyColumn
      import androidx.compose.foundation.lazy.items
      import androidx.compose.material.icons.Icons
      import androidx.compose.material.icons.filled.ArrowBack
      import androidx.compose.material3.*
      import androidx.compose.runtime.*
      import androidx.compose.ui.Modifier
      import androidx.compose.ui.unit.dp
      import com.example.josparcoffee.data.CartManager
      import com.example.josparcoffee.navigation.*
      
      @OptIn(ExperimentalMaterial3Api::class)
      @Composable
      fun CheckoutScreen() {
      
          val backStack = LocalBackStack.current
          val cartItems = CartManager.cartItems
      
          var showSuccess by remember { mutableStateOf(false) }
      
          Scaffold(
              topBar = {
                  TopAppBar(
                      title = { Text("Checkout") },
                      navigationIcon = {
                          IconButton(onClick = {
                              backStack.removeLastOrNull()
                          }) {
                              Icon(Icons.Default.ArrowBack, null)
                          }
                      }
                  )
              }
          ) { padding ->
      
              Column(
                  modifier = Modifier
                      .fillMaxSize()
                      .padding(padding)
              ) {
      
                  // TITLE
                  Text(
                      text = "Ringkasan Pesanan",
                      style = MaterialTheme.typography.headlineSmall,
                      modifier = Modifier.padding(16.dp)
                  )
      
                  // LIST ITEM
                  LazyColumn(
                      modifier = Modifier
                          .weight(1f)
                          .padding(horizontal = 8.dp)
                  ) {
                      items(cartItems) { cartItem ->
      
                          val price = when (cartItem.variant) {
                              "Hot" -> cartItem.item.priceHot
                              "Ice" -> cartItem.item.priceIce
                              else -> cartItem.item.price
                          }?.toIntOrNull() ?: 0
      
                          Card(
                              modifier = Modifier
                                  .fillMaxWidth()
                                  .padding(vertical = 6.dp),
                              elevation = CardDefaults.cardElevation(4.dp)
                          ) {
                              Column(modifier = Modifier.padding(12.dp)) {
      
                                  Text(
                                      text = cartItem.item.name,
                                      style = MaterialTheme.typography.titleMedium
                                  )
      
                                  Spacer(modifier = Modifier.height(4.dp))
      
                                  Text("Tipe: ${cartItem.variant}")
                                  Text("Harga: Rp $price.000")
                                  Text("Qty: ${cartItem.quantity}")
      
                                  Spacer(modifier = Modifier.height(6.dp))
      
                                  Divider()
      
                                  Spacer(modifier = Modifier.height(6.dp))
      
                                  Text(
                                      text = "Subtotal: Rp ${price * cartItem.quantity}.000",
                                      style = MaterialTheme.typography.bodyMedium
                                  )
                              }
                          }
                      }
                  }
      
                  // TOTAL + BUTTON
                  Card(
                      modifier = Modifier
                          .fillMaxWidth()
                          .padding(16.dp),
                      elevation = CardDefaults.cardElevation(8.dp)
                  ) {
                      Column(modifier = Modifier.padding(16.dp)) {
      
                          Text(
                              text = "Total Pembayaran",
                              style = MaterialTheme.typography.labelLarge
                          )
      
                          Spacer(modifier = Modifier.height(4.dp))
      
                          Text(
                              text = "Rp ${CartManager.getTotal()}.000",
                              style = MaterialTheme.typography.headlineSmall
                          )
      
                          Spacer(modifier = Modifier.height(12.dp))
      
                          Button(
                              onClick = {
                                  showSuccess = true
                                  CartManager.cartItems.clear()
                              },
                              modifier = Modifier.fillMaxWidth()
                          ) {
                              Text("Bayar Sekarang")
                          }
                      }
                  }
              }
          }
      
          // DIALOG
          if (showSuccess) {
              AlertDialog(
                  onDismissRequest = { showSuccess = false },
                  title = { Text("Pembayaran Berhasil") },
                  text = { Text("Terima kasih sudah memesan ☕") },
                  confirmButton = {
                      Button(onClick = {
                          showSuccess = false
                          backStack.clear()
                          backStack.add(Routes.Home)
                      }) {
                          Text("Kembali ke Home")
                      }
                  }
              )
          }
      }
